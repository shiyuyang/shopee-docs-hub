# CNSC API 对接用户手册

> 来源: [Shopee Open Platform](https://open.shopee.com/developer-guide/28)
> 分类: Getting Started

## **1. 初识 CNSC**


CNSC 全称中国卖家中心，是为中国跨境卖家(包括香港地区卖家)定制的卖家后台，卖家可以通过它管理多个店铺的商品、订单、营销等。CNSC 的基本操作指南与介绍，请访问这里。


对接 CNSC 集中关注的接口均为**商品管理**相关，需要开发的接口包含`v2.media_space`及 GlobalProduct 下所有接口。


(注意：店铺升级为 CNSC 账号，并不意味着只需要对接 v2.media_space 及 GlobalProduct 接口，您仍然需要对接 v2.product 相关接口获取/更新产品相关信息）


**FAQ:**


**怎么判断我司是否需要对接 CNSC？**


**如果不做对接，CNSC 店铺还能继续使用我司提供的服务吗？**

1. 如果贵司服务方向非商品管理相关，也不涉及上文提到的接口，那么在绑定贵司 ERP 的卖家进入 CNSC 后，卖家仍可继续使用贵司的服务。
1. 如果贵司服务方向为商品管理相关，且在绑定贵司 ERP 的卖家进入 CNSC 后，贵司未做任何开发， 那么卖家需要转而寻找其他支持 CNSC 接口的 ERP 来管理商品。

![图片](https://open.shopee.com/opservice/api/v1/image/download/?image_id=eTOXQX%2BTXg7YxsThPm9sHdjsGaWrWg5GOZFYprkQ7dsPXCJcSfzEbEkbKROosAE%2FtyXbmStN%2Bn8sjMltnzgq6A%3D%3D&image_type=png)

## **2. 准备对接**
### **2.1 注册成为开发者（已有开发者账号可跳过）**


a.点击“Sign up”并阅读”Agreement”,通过邮箱去注册 Shopee Open Paltform 账号`https://open.shopee.com/`


![图片](https://open.shopee.com/opservice/api/v1/image/download/?image_id=boPoCRpI5zvJRMJem%2Fy%2Bqia1vHkAR1cfMUT17V2b5d733O5C0lAqINuCFc8nau%2FRB3J8CQwmqr3ddw8bNS4LqQ%3D%3D&image_type=png)


注意：一旦注册，账户邮箱不可更改。


b.您将会收到一封验证邮件，请验证您的邮箱并设置密码。


![图片](https://open.shopee.com/opservice/api/v1/image/download/?image_id=ko0pD1WlqcGUVmAwy7AL%2FAFdGI94JKqEhn%2BgBv4Gn2mwV4s85dFh%2Bii3AoYgqF9EGGMQtKs93Qok0SGenECVdQ%3D%3D&image_type=png)


c.使用您的账号登录。


![图片](https://open.shopee.com/opservice/api/v1/image/download/?image_id=eclMWm1EtCLtz%2Bxq%2B8eTEI7u3Jr%2FRDfLWMP%2F36N7b93o3a0euMqL07C%2FMlI0gUSRth%2FowGg2QE2o7vPNhh9CfA%3D%3D&image_type=png)

### **2.2  完善账户信息 （开发者资料审核已通过可跳过）**


a.请参阅本文，了解您属于哪种类型的开发者账户。


登录 Open Platform >> Console >> App List >> 选择开发者类型 >> Add


*针对开发者填写的资料内容，开发者会被分为不同的开发者类型，而不同的开发者类型，可以创建的 App 类型不同，具体请参考 App management 页面


b.根据您选择的开发者类型，完善相应的资料。资料需要通过 Shopee 平台的审核，审核通过后，才能正式成为开发者。


*提交资料后请联系您的客户经理/招商经理协助推进资料审核。

### **2.3 创建 APP**


调用 Shopee OpenAPI 需要先创建 App，通过 APP 维度调用 OpenAPI。当开发者资料被平台审核通过后，即可创建 APP。


支持 CNSC 接口的 APP, APP 类型对应支持的接口范围请参考相关链接


*Original APP type 不支持2.0接口，即不支持2.0接口中包含的 CNSC 接口。请根据这个指引完成 app 的升级。`https://open.shopee.com/announcements/553`


*第三方系统可创建“ERP system”/“Product management”类型的 APP, 自主研发系统可创建“seller in-house system”类型的 APP，均可实现 CNSC 接口的调用。


如果您的开发者账号中没有以上类型的 APP，请通过以下路径创建。路径：Open Platform >> Console >> App List >> + Create App >> 填写资料 >> Submit

### **2.4 APP 上线**


在完成测试，确定可以服务 Live 环境的店铺之前，您必须确保您的 APP 已经 Go live。开发者在 Sandbox 环境完成 OpenAPI 的测试后，需要申请 App 上线，审核通过后，开发者可以获取 Live 环境的 partner_id 与 key。


a.在您完成测试并准备好后，单击“Go -Live”来请求 Live 环境的凭证。


Open Platform >> Console >> App List >> 选择需要上线的 APP >> 点击 Go live >> 填写资料>> Submit


![图片](https://open.shopee.com/opservice/api/v1/image/download/?image_id=gPJB00XX0HbdYPVLUx4P5r%2F3vA5xHVvE3DSnrgObdOm6UIrxxg2omkKxDxNaBpAH%2B9lXONd5vWYjOJ%2BNJ0C5XA%3D%3D&image_type=png)


b.Shopee OpenPlatform 将验证您在测试 API 调用表现，并在**24小时内自动完成**审核。Shopee 审核通过后，APP 状态将变为 Live 状态，开发者将获取 Live 环境的 PartnerID 和 Key。

### **2.5 开始测试**


1) 创建测试店铺


路径：Open Platform >> Console >> Tools >>Test account >>  Create China Merchant Account


至多可创建 3个 Merchant,每个 merchant 下至多9个 shop。


![图片](https://open.shopee.com/opservice/api/v1/image/download/?image_id=a0FF5u3oaCGgWh0CQ6myfjBa9V%2FLQX3Q1FDSIcBj2CTfDCOER1jb7x14NZVjJ9HX4xFLJc6hHIh6dnqA%2BIjysg%3D%3D&image_type=png)


**注意：测试账号登录 CNSC 的验证码都是123456**


创建完成后，可进入参照页面中的 Merchant Login URL 登录主账号，完成主账号和店铺的授权，并设置各个站点的汇率换算以及调价百分比，以利后续接口调试顺利进行，详细教程参考卖家学习中心：必做基础设置


（登录 CNSC-->点击全球商品菜单-->完成弹窗设置-->点击确定）


![图片](https://open.shopee.com/opservice/api/v1/image/download/?image_id=E7HUePQohELzjGzjRQsadp2oyJ2IFQeyk5B8H4w1q4aPGgHBB6zSA2M1%2BjIyIo5%2FZOQEnT9XZqHswSJAub4ABQ%3D%3D&image_type=png)


b.将您的测试店铺绑定到测试 partner id。


授权链接拼接方式


卖家端授权方式


c.逐一测试`v2.media_space`及 GlobalProduct 下所有接口

### ****
## **3. 汇总**


1）创建 APP 时，以确保您的 APP type 可调用 v2.0 product 相关接口。


2）测试开始前，请登录 CNSC 后台完成主账号和店铺的授权，并设置各个站点的汇率换算以及调价百分比，以利后续接口调试顺利进行。


3）测试完成后，需要确保 APP 状态为 Live，卖家用户才能接入服务。


      点击 Go Live 后，APP 会在24小时内自动完成审核。


4）新创建的 APP 需要获得卖家授权，才能为卖家提供 CNSC 相关接口服务。


5）【请特别关注】 常见 CNSC 接口相关问题


更多 CNSC 相关问题，请在`https://shopee.cn/edu/home`输入关键字 CNSC 详细了解。

![图片](https://open.shopee.com/opservice/api/v1/image/download/?image_id=AVoaUNh9sjK5Ya6Sh9OIQ5nCAEhmokc%2FwXVJmcyx9BSEewCLatoyYY8wFND5UKqtUwXtpOkXUiMJGo2NdrhW0Q%3D%3D&image_type=png)


如有任何本手册未能覆盖的技术对接问题，请联系通过工单系统联系 Shopee Open Platform。


