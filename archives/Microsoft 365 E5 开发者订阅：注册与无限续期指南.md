# Microsoft 365 E5 开发者订阅：注册与无限续期指南

![Microsoft 365 E5 订阅](https://bbtdd.com/wp-content/uploads/img/15848700519.webp)

Microsoft 365 E5 开发者订阅以其丰富的功能著称，每个 E5 账号可开通 25 个子账号，免费享用 Office 套件和 5TB OneDrive 云存储。本指南将详细介绍 E5 订阅的注册与续期方法，助你实现“无限白嫖”。

## Microsoft 365 E5 订阅的注册流程

由于 Office 365 已更名为 Microsoft 365，注册流程和界面有所更新。以下是当前的注册步骤：

1. **访问注册入口**  
   前往 [Microsoft 365 开发人员计划](https://developer.microsoft.com/zh-cn/microsoft-365/dev-program) 页面。

2. **准备注册材料**  
   - 一个未注册过开发者订阅的微软账号。  
   - 一个未注册过开发者订阅的手机号（+86 即可）。  

3. **选择数据中心**  
   注册时，建议将国家/地区设置为“Singapore”，以便享受更快的访问速度。

注册完成后，即可获得 90 天的 E5 订阅。

## 创建子账号

1. **登录管理页面**  
   访问 [Microsoft 管理页面](https://admin.microsoft.com/)，使用 E5 订阅的管理员账号登录（格式为“[email protected]”）。

2. **查看域名**  
   如果忘记域名，可在 [Microsoft 365 个人资料页面](https://developer.microsoft.com/zh-cn/microsoft-365/profile) 查看。

3. **创建子账号**  
   在“用户管理”选项卡中创建子账号，并勾选“Microsoft 365 E5 开发者”许可证。

## 将 OneDrive 存储升级至 5TB

1. **访问 OneDrive 管理页面**  
   登录 [OneDrive 企业版控制台](https://admin.onedrive.com/)。

2. **修改存储限制**  
   点击右上角设置图标，找到“OneDrive 存储限制”，将其修改为 5120GB。此设置对所有子账号生效。

## 使用 Azure API 实现续签

1. **注册应用**  
   登录 Azure 门户，进入“应用注册”页面，点击“+ 新注册”。填写应用名称，选择“任何组织目录中的帐户和个人 Microsoft 帐户”作为账户类型。

2. **配置身份验证**  
   在“身份验证”选项卡中，添加“移动和桌面应用程序”平台，并保存“应用程序 ID”。

3. **禁用安全默认值**  
   进入“管理安全默认值”页面，将其禁用，以避免挂机脚本掉线。

## 续签软件推荐

- **PC 端：M365 E5 Renew Plus**  
  下载地址：https://e5renew.com/  
  功能稳定，推荐使用。

- **Docker 端：Microsoft 365 E5 Renew X**  
  提供 x86 和 arm 版本的镜像，适合不同设备。

将子账号和应用 ID 填入续签软件后，即可开始运行。建议 7x24 小时挂机，确保订阅续签成功。

👉 [野卡 | 一分钟注册，轻松订阅海外线上服务](https://bbtdd.com/yeka)

## 注意事项

- 挂机程序在订阅剩余 30 天时尝试续签，但成功率并非 100%。  
- 建议不要在 E5 账号中存放重要数据，并做好多备份。

通过以上步骤，你可以轻松注册并长期维持 Microsoft 365 E5 开发者订阅。Happy coding！