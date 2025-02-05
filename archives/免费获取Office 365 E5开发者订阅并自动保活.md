# 免费获取Office 365 E5开发者订阅并自动保活

## 前言

曾经，Office 365开发者试用订阅（简称E3）的有效期仅为一年，一年后所有数据都会丢失。现在，微软推出了新版订阅，**有效期为90天**，并且可以**自动续订**。以下是官方教程链接：

[官方教程](https://docs.microsoft.com/en-us/office/developer-program/office-365-developer-program)

> - 包括 25 个用于开发目的的用户许可证
> - 访问核心 Microsoft 365 工作负载和功能（不包括 Windows）
> - 所有 Office 365 应用，包括 SharePoint、OneDrive、Outlook/Exchange、Teams、Planner、Word、Excel、PowerPoint 等
> - Office 365 高级威胁防护
> - Power BI 高级分析
> - 用于合规性和信息保护的企业移动性 + 安全性 (EMS)
> - 用于构建高级标识和访问管理解决方案的 Azure Active Directory

👉 [WildCard | 一分钟注册，轻松订阅海外线上服务](https://bbtdd.com/WildCard)

## 快速开始

1. **登录Office开发人员中心**  
   首先，进入[Office开发人员中心](https://developer.microsoft.com/zh-cn/office)，登录你的微软账号，然后点击“立即加入”。

   

2. **开通Office开发者账号**  
   开通Office开发者账号，并完善个人信息。

     
   

3. **设置订阅**  
   进入个人中心，点击“设置订阅”。

   

4. **填写订阅信息**  
   填写开发者订阅的相关信息。（请注意，此处需要网络环境支持，否则无法接收验证码）

   

5. **添加许可证**  
   注册完成后，需要为你的账号添加许可证，否则无法使用。

   

6. **管理许可证**  
   点击“Go to subscription”进入后台，依次选择：管理 -> 用户 -> 活跃用户 -> 点击用户名 -> 许可证和用户，添加好许可证后点击“应用”。

   

7. **扩大OneDrive容量**  
   在[OneDrive管理](https://admin.onedrive.com/)中，找到储存设置，扩大你的OneDrive容量。

   

## 保活方法

为了确保订阅的续订，许多用户采取了调用API的方法来保活，主要集中在对OneDrive和Outlook API的使用上。以下是两种常见的保活方法：

1. **基于Rclone的OneDrive API调用**  
   通过Rclone挂载OneDrive并使用自建API触发续订。

2. **基于onemanager的OneDrive API调用**  
   使用onemanager搭建OneDrive管理工具，实现API调用。

后续将详细介绍这些保活方法，敬请期待。

👉 [WildCard | 一分钟注册，轻松订阅海外线上服务](https://bbtdd.com/WildCard)

听说通过调用Outlook的API，已经过期的账户在两天内会自动续期。如果你对此感兴趣，不妨试试这些方法！