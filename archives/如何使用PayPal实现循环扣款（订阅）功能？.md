# 如何使用PayPal实现循环扣款（订阅）功能？

## 起因

在业务需求中，需要集成PayPal并实现循环扣款功能。经过查阅百度和Google，发现除了PayPal官网外，几乎没有相关的开发教程。因此，我花了几天时间深入研究，最终成功集成。在这里，我将分享如何使用PayPal的支付接口实现循环扣款功能。

## PayPal支付接口概览

PayPal目前提供多套接口，主要包括：

1. **Braintree**：通过Braintree实现Express Checkout；
2. **REST API**：创建App，通过REST API接口方式（现阶段的主流接口）；
3. **NVP/SOAP API**：旧接口方式，不推荐使用。

### Braintree接口

Braintree是PayPal收购的一家公司，除了支持PayPal支付外，还提供了升级计划、信用卡、客户信息管理等全套功能。虽然PayPal的REST接口也集成了大部分功能，但Braintree的Dashboard可以直接管理这些信息，使用更加方便。尤其是对于使用Laravel框架的开发者，Laravel的Cashier解决方案默认支持Braintree，因此我的首选是Braintree接口。然而，最终发现Braintree在国内并不支持，无奈只能放弃。

### REST API

REST API是顺应时代发展的产物。如果你之前用过OAuth 2.0和REST API，那么理解和使用这些接口不会有什么困难。

### 旧接口

除非REST API接口无法满足需求，比如政策限制，否则不推荐使用旧接口。全球都在向OAuth 2.0认证方式和REST API迁移，因此没必要逆势而行。

## REST API详细介绍

PayPal官方的API参考文档对其API和使用方式有较为详细的介绍。然而，直接调用这些API可能会比较繁琐，因此建议使用官方提供的[PayPal-PHP-SDK](https://github.com/paypal/PayPal-PHP-SDK)，并根据其Wiki作为起点。

在开始首个例子之前，请确保你已拥有Sandbox账号，并正确配置以下信息：

1. **Client ID**
2. **Client Secret**
3. **Webhook API**（必须是https开头且使用443端口，本地调试建议结合ngrok反向代理生成地址）
4. **Returnurl**（注意项同上）

完成Wiki中的首个例子后，理解接口分类有助于满足业务需求。以下是接口分类的简要介绍：

- **Payments**：一次性支付接口，不支持循环扣款。
- **Payouts**：未使用，忽略。
- **Authorization and Capture**：支持通过PayPal账号登录网站并获取相关信息。
- **Sale**：与商城相关，未使用，忽略。
- **Order**：与商城相关，未使用，忽略。
- **Billing Plan & Agreements**：升级计划和签约功能，即订阅功能，是实现循环扣款的关键。
- **Vault**：存储信用卡信息。
- **Payment Experience**：未使用，忽略。
- **Notifications**：处理Webhook信息，虽然重要但不涉及本文内容。
- **Invoice**：票据处理。
- **Identity**：认证处理，实现OAuth 2.0登录，获取token以请求其他API。

## 如何实现循环扣款

实现循环扣款分为以下四个步骤：

1. 创建升级计划并激活；
2. 创建订阅（创建Agreement），并跳转到PayPal网站等待用户同意；
3. 用户同意后，执行订阅；
4. 获取扣款账单。

### 创建升级计划

升级计划对应`Plan`类。以下是创建升级计划的代码示例：

php
$param = [
    "name" => "standard_monthly",
    "display_name" => "Standard Plan",
    "desc" => "Standard Plan for one month",
    "type" => "REGULAR",
    "frequency" => "MONTH",
    "frequency_interval" => 1,
    "cycles" => 0,
    "amount" => 20,
    "currency" => "USD"
];


### 创建订阅

创建订阅即创建`Agreement`。以下是创建订阅的代码示例：

php
$param = [
    'id' => 'P-26T36113JT475352643KGIHY', // 上一步创建Plan时生成的ID
    'name' => 'Standard', 
    'desc' => 'Standard Plan for one month'
];


### 用户同意后执行订阅

用户同意后，必须执行`Agreement`的`execute`方法才算完成真正的订阅。以下是代码片段：

php
public function onPay($request)
{
    $apiContext = $this->getApiContext();
    if ($request->has('success') && $request->success == 'true') {
        $token = $request->token;
        $agreement = new \PayPal\Api\Agreement();
        try {
            $agreement->execute($token, $apiContext);
        } catch(\Exception $e) {
            return null;
        }
        return $agreement;
    }
    return null;
}


### 获取交易记录

订阅后，可能不会立刻产生交易扣费的记录，如果为空则过几分钟再次尝试。以下是获取交易记录的代码片段：

php
public function transactions($id)
{
    $apiContext = $this->getApiContext();
    $params = ['start_date' => date('Y-m-d', strtotime('-15 years')), 'end_date' => date('Y-m-d', strtotime('+5 days'))];
    try {
        $result = Agreement::searchTransactions($id, $params, $apiContext);
    } catch(\Exception $e) {
        Log::error("get transactions failed" . $e->getMessage());
        return null;
    }
    return $result->getAgreementTransactionList();
}


## 需要注意的问题

在实现循环扣款功能时，有以下几点需要特别注意：

1. **国内Sandbox连接较慢**：国内使用Sandbox测试时连接特别慢，经常提示超时或出错，因此需要特别考虑执行中途用户关闭页面的情况。
2. **实现Webhook**：一定要实现Webhook，否则当用户在PayPal取消订阅时，你的网站将得不到通知。
3. **订阅的持续性**：订阅（Agreement）一旦产生，除非主动取消，否则将一直生效。因此如果你的网站设计了多个升级计划，切换升级计划时必须取消前一个计划。
4. **原子操作**：用户同意订阅到完成新订阅的整个过程应该是原子操作，同时耗时较长，因此建议将其放到队列中执行以提高体验。

👉 [WildCard | 一分钟注册，轻松订阅海外线上服务](https://bbtdd.com/WildCard)