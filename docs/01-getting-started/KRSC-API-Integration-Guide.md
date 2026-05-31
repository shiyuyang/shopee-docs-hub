# KRSC API 集成指南

> 来源: [Shopee Open Platform](https://open.shopee.com/developer-guide/29)
> 分类: Getting Started

## 1. 什么是 KRSC

KRSC 的全称是韩国卖家中心 (Korean Seller Center)。它是面向韩国跨境卖家的卖家中心。卖家可以通过它管理多个店铺的产品、订单和营销。有关 KRSC 的基本操作指南和介绍，请点击此处。

重要提示：升级到 KRSC 的 KRCB 卖家和 KRCB 店铺的管理 ERP 开发者 (ISV) 需要注意，产品 API 需要替换其他 API。您需要开发的 API 包括全球产品 API (Global Product API) 和商家 API (Merchant API)。并确保您已使用 V2.0 店铺授权。

如果未集成 KRSC API - 全球产品 API 和商家 API，升级到 KRSC 的店铺将无法通过 API 调用产品列表相关模块。

FAQ：


Q：如何判断一个店铺是否已升级到 KRSC？


A：您可以查询 v2.shop.get_shop_info API，如果 API 返回参数 merchant_id，然后查询 v2.merchant.get_merchant_info，merchant_region=KR，则表示该店铺已升级到 KRSC。


Q：如果我的系统没有产品相关功能，即不包含产品创建和产品更新功能，是否需要做一些调整？


A：不需要，例如订单相关 API，API 调用流程没有变化。

## 2. 如何集成 KRSC API
### 2.1 注册成为开发者（如果您已有开发者账户，可跳过此步骤）


a. 点击 "Sign up" 并阅读 "Agreement"，通过电子邮件注册 Shopee 开放平台账户。`https://open.shopee.com/`


![图片](https://open.shopee.com/opservice/api/v1/image/download/?image_id=07DNyyfCiU9Ua3QSELO5rrCrGiGREHeTKPWY%2Fkw7%2FlgAhjfyQ4qbef0gTUCzmSJAUzOph5HMQ%2B5lz73IOs%2BZWQ%3D%3D&image_type=png)


![图片](https://open.shopee.com/opservice/api/v1/image/download/?image_id=BVs0FCmQ%2B1zwxPsYrUatW6Pjzm5QEIdLUNMuB%2B2DPPjBEqyMNuLz4wZAFFvOC5dj3wzkRDJc1Fk43qX5QIdhhg%3D%3D&image_type=png)


b. 您将收到一封验证邮件，请验证您的电子邮件并设置密码。


![图片](https://open.shopee.com/opservice/api/v1/image/download/?image_id=BAQ1eWOJR6mWBitGCpYucjrV4Gy32V6Mhrd6zFw4jNpw2SnjMfb2edrYAmqX6bFnmpsrdRTQ7jAFoCgLiNaMZg%3D%3D&image_type=png)


c. 使用您的账户登录。


![图片](https://open.shopee.com/opservice/api/v1/image/download/?image_id=xkNBehrdYmvsiqY16RwrOvm%2FZYhmJ3Swg4Ev%2BH4kS6BofNHitA3OuUkDmB%2FmO6i47Rw4M5NX60gRPXiIjq4PXA%3D%3D&image_type=png)

### 2.2 完善账户信息（如果您已有已获批的开发者账户，可跳过此步骤）


a. 请参考此文章了解您的开发者账户类型。登录开放平台 >> Console >> App List >> 选择开发者类型 >> 添加


*不同类型的开发者将拥有不同类型的应用。详情请参阅 App 管理页面。


b. 根据您选择的开发者类型填写相应的资料。信息需要由 Shopee 平台审核。

### 2.3 创建应用


要调用 Shopee OpenAPI，您需要先创建一个应用。开发者资料获批后即可创建应用。


**注意**


*原始 APP 类型不支持 V2.0 API，如果您现有的应用是原始类型，请根据此公告完成应用升级。


*对于其他类型的应用，请根据此文章检查 API 权限。


如果您没有应用，可以通过以下路径创建


**路径：**开放平台 >> Console >> App List >> + Create App >> 填写信息 >> Submit

### 2.4 上线应用


您必须确保您的应用状态为在线。点击 "Go-Live" 请求使用生产环境 API。


开放平台 >> Console >> App List >> 选择要上线的 APP >> 点击 Go live >> 填写信息 >> Submit


![图片](https://open.shopee.com/opservice/api/v1/image/download/?image_id=1bRneJcp7OTLdjQ82C7VENn4FpvXw2%2FiWNE%2BsGrbXbnENjzi1aGeSXZFjsZhzMiaDL6W%2Fjkc9Ih40BDl6OF3IQ%3D%3D&image_type=png)


APP 将在 24 小时后自动完成审核，APP 状态将变为 Online 状态，开发者将获得生产环境的 Live Partner id 和 Partner Key。

### 2.5 开始 API 测试


a. 在 KRSC Sandbox 准备就绪之前，KRSC 开发者可以使用 CNSC Sandbox 测试 API，因为其功能与 KRSC 类似。


1) 开始测试前，您应在 Console 上创建一个中国商家


![图片](https://open.shopee.com/opservice/api/v1/image/download/?image_id=ZeLHVtU8WelqVJRdsbQqeuKEbyAhzLKxIPxqn9L5FfRwKNKhatrh1jYdi2NyZx%2FqvCH7qUQhBk9rNDSGsqOu5g%3D%3D&image_type=png)


2）登录 `https://seller.test-stable.shopee.cn`。请注意，otp 是 123456。


***注意：如有需要，请使用谷歌翻译翻译为英语或韩语。*


![图片](https://open.shopee.com/opservice/api/v1/image/download/?image_id=Z%2FuyR1WrCBnGHeY3KSevD%2FZY%2BH2%2FLhsbp1HO%2BzDsq%2B%2B3QK0MP%2BidCH%2FJvp5g%2BY%2F9emVg4GHbCDcYkIjcWZO5tw%3D%3D&image_type=png)


![图片](https://open.shopee.com/opservice/api/v1/image/download/?image_id=JvSqNkMgwzqnIzsM4REnYXr%2BCOCMIzw1XejYrJ1NIDDcU%2FJcapOHkEr0BEQY%2FFmyM4prk1EiAz%2B4a6IUtupjYA%3D%3D&image_type=png)


3) 登录后设置货币。


***注意：在 CNSC sandbox 中测试时，仅支持 CNY 货币。在实际的 KRSC（生产环境）中，货币选项为 USD 或 KRW。*


![图片](https://open.shopee.com/opservice/api/v1/image/download/?image_id=8oXXnc6F8lniaGfCFYR7hNaHZyjalfZAEvc6vDRREH%2FVv3Qu7ejFENdvxVvyGo7ndSYuwfdxGhbFCE5gkTe52A%3D%3D&image_type=png)


4) 设置市场汇率。如果您设置的数字错误，系统会提示正确的数字范围，如截图所示。


![图片](https://open.shopee.com/opservice/api/v1/image/download/?image_id=fh01dA9MXGyppU17dMjT7YdJc9qG1wR26fgseQwQgIqpM%2FZd7pzgorwcIcIUR34dNq6%2BWEmjqZOqauDatrq5Bg%3D%3D&image_type=png)


5) 然后，您可以在商家设置页面将界面语言设置为英语。


![图片](https://open.shopee.com/opservice/api/v1/image/download/?image_id=6qhJCHNH7nYqIV2wKsFRbMofALZdOYKnFweDBLDYNXz8Cp4QUDgSYiPeOEIdAutZGGXxdyHHL96mrpv4%2BAqcGA%3D%3D&image_type=png)


6) 查看 Global SKU 页面。请完成设置并点击按钮 "Start to upgrade to Global SKU"


![图片](https://open.shopee.com/opservice/api/v1/image/download/?image_id=okLn69TBiWNkRCHNG8OXHY1GUvbCFTFJkgfucjIIEznOD8BU3c3%2FRhr64aNoFptIc1W09SXD8KdYav0QEGigHw%3D%3D&image_type=png)


![图片](https://open.shopee.com/opservice/api/v1/image/download/?image_id=xNF2eZI3wGgvOdQTYFxS5WA3OklnuIIha8pBbbxCW%2BvMBkWB5CYycsNUbvaxW41tZNIxCj5I7olFIZSgJD1Qug%3D%3D&image_type=png)


然后您可以开始测试开放 API。更多详情请参阅 Sandbox Testing 文章。


b. 当卖家登录 KRSC 并完成每个店铺的产品升级后，`v2.shop.get_shop_info` 将返回 mtsku_upgraded_status:UPGRADED


c. 测试全局产品 API 和商家 API。您可以从此处查看 API 调用流程

### 2.6 商家与店铺授权

因为店铺账户升级到 KRSC 后，多个店铺将归属于商家，您可以通过此 FAQ 了解更多关于商家和店铺之间的关系。因此，为了正常调用 GlobalProduct API，请重新授权您的店铺，并在授权时切换到子账户页面。


![图片](https://open.shopee.com/opservice/api/v1/image/download/?image_id=3yR0asw1jvtA3%2F9oYcUWNIji3AdXQqe5t14vyZGkRaB9GmdCLhUT4NJEMGmPyyaGVI4Kr2cJZLRLMlFg2EQKBg%3D%3D&image_type=png)


请使用您的主账户进行授权。子账户无法完成授权。主账户的格式为 ***.main


账户成功登录后，您将看到授权页面，先勾选您要授权的店铺，然后勾选 Auth Merchant。如果不勾选 Auth Merchant，您将无法调用相关的 Global Product API 或获取商家信息。如果某些店铺未被勾选，则无法通过 API 将产品发布到相关店铺。因此，请确保您勾选了您管理的完整的商家和店铺。


![图片](https://open.shopee.com/opservice/api/v1/image/download/?image_id=Tl0U8usumC9hZgPO94%2FG9W5Gs4WGeeCddgO9c31Re0ftxnprH8jSRzVOPCB%2Bw%2F%2B5Tztu9Tnqcpn2JCSCHIucfA%3D%3D&image_type=png)


授权成功后，回调地址将返回 main_account_id 而非 shop id。稍后将使用 Main_account_id 获取 AccessToken。


然后请根据此文档刷新令牌


通过 GetAccesstoken API，您将获得当时已成功授权的所有商家 ID 和店铺 ID 的列表。


请注意，每个商家和每个店铺的令牌是独立的，您需要分别存储。当您完成授权时，您获得的初始 refresh token 和 access_token 可以由当前授权的商家 ID 和店铺 ID 共享，然后您调用 RefreshAccessToken API，不同的商家 ID 或不同的店铺 ID 将返回不同的 refresh token 和 access_token，因此请分别保存它们的令牌。


如果您想获取商家 ID 和店铺 ID 之间的关系，请调用 get_shop_list_by_merchant API。您可以通过调用 get_merchant_info 获取每个商家的信息，并通过调用 get_shop_info 获取每个店铺的信息。

## 3. 总结


1）创建应用或使用现有应用时，请确保您的应用类型可以调用 v2.0 GlobalProduct API。


2）店铺需要卖家重新授权，以便为卖家提供 KRSC 产品相关 API 服务。


3）必须确保 APP 状态为 Online，以便卖家用户可以在生产环境中使用 KRSC API。在开放平台 Console 中点击 Go Live 并提交信息。APP 将在 24 小时后自动获批。


4）卖家需要登录 KRSC 并完成相关设置，KRSC 产品升级才能成功。只有当产品成功升级后，才能正常调用 Global Product API。


5）您可以从此处了解更多 KRSC API FAQ：KRSC API FAQ


#### 如果本文档未涵盖任何技术连接问题，请通过 ticket 系统联系 Shopee 开放平台。
