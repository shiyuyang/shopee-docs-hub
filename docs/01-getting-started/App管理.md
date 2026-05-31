# App 管理

> 来源: [Shopee Open Platform](https://open.shopee.com/developer-guide/14)
> 分类: Getting Started


当您的开发者账号审核通过之后，您可以在控制台创建新的 App。

## App 类型


Shopee 开放平台有以下类型的 App，您可以通过您应用的需要创建合适的 App 类型：

-**ERP System**: 您是 Shopee 卖家的技术服务商，您的应用管理关键业务流程。
-**Product Management**: 您的应用旨在仅管理与商品相关的流程。
-**Order Management**: 您的应用旨在仅管理与订单和履行相关的流程。
-**Accounting and Finance**: 您的应用旨在仅管理订单对账流程。
-**Marketing**:您的应用旨在仅管理与营销活动相关的流程
-**Seller In-house System**: 您自己作为 Shopee 卖家使用的应用程序。
-**Customer Service**: 您的应用仅用于管理与客户服务相关的流程。


不同类型的开发者账号，可以创建的 App category 不一样。

| App 类型 |**开发者账号类型**|
| --- | --- |
|**Third-party Partner Platform (ISV)**|**Registered Business Seller**|**Individual Seller**|**Individual Third Party***|
|**ERP System**| ✓ | | | |
|**Product Management**| ✓ | | | ✓ |
|**Order Management**| ✓ | | | ✓ |
|**Accounting and Finance**| ✓ | | | ✓ |
|**Marketing**| ✓ | | | |
|**Customer Service**| | | | |
|**Seller In House System**| | ✓ | ✓ | |


*请注意 Individual Third Party 是我们旧的开发者类型，我们将不再支持，开发者也无法再创建。目前只有 Third-party Partner Platform(ISV) / Registered Business Seller / Individual Seller 三种类型。


*另外如果您原来注册的开发者类型是 Registered Business Seller / Individual Seller，但是您的团队已经壮大并开始服务了第三方卖家，您可以将开发者类型更改为 Third-party Partner Platform，一旦升级审核通过，您之前创建的 App 将会自动从 Seller In-house System 类型变更为 ERP System 类型。更多操作指引请查看 FAQ。


不同类型的 App 有不同的 API 权限和推送服务的权限，您可以根据需要创建不同类型的 App。

| App 类型 | API 权限列表 |
| --- | --- |
| ERP System | 所有的 API 除了 Chat 和 Ads 模块 API |
| Seller In-house System | 所有的 API 包括 Chat 模块 API |
| Product Management | 点击查看 API 列表 |
| Order Management | 点击查看 API 列表 |
| Accounting and Finance | 点击查看 API 列表 |
| Marketing | 点击查看 API 列表 |
| Customer Service | 点击查看 API 列表 |
| Ads Service | 点击查看 API 列表 |


注意：


*可以通过这里了解更多 App 消息推送服务权限列表。


*目前新创建的 App 都只有 V2.0 API 的权限，无法再调用 V1.0 API，您将在 App 详情页中看到 App Permission 的注明：


![图片](https://open.shopee.com/opservice/api/v1/image/download/?image_id=qGvLmpk1dZ%2FOkMB4EaVcHVa1Jf3Fh%2BErV0QyAeZ0aOws%2BGKYZIA5bSglQ3iXBQ0Y8kmzceRfqrxVb55SordlwQ%3D%3D&image_type=png)

## 创建 App


1.进入控制台，点击创建 App，进入创建页后，提交相关信息。App name / App Description / App logo 信息您都可以自定义填写。


![图片](https://open.shopee.com/opservice/api/v1/image/download/?image_id=9jpXuffGmGDFRjflp%2B1Xr%2Be67sF7Y8KB8%2BdIswqz5WxrEUs05rDEa1gMgH3KlMcoPBXVGxpUgmbJrdg%2Ftf5f6A%3D%3D&image_type=png)


![图片](https://open.shopee.com/opservice/api/v1/image/download/?image_id=3hgBqdB%2BbBmXuq5rNdubrzeXFs2eHNu9TWOh2tYkDJ0k3Hlv5%2FdLSoTmAiuFO9hKsDyrexrlzS%2BE5ou%2BOGHWAg%3D%3D&image_type=png)


创建成功之后，您将会获得到一个 Test partner_id 和 Test key, 他们只能沙箱环境上给您测试使用，不能用于生产环境，当您测试完成后，您可以将 App 提交上线。

## 提交 App 上线


进入控制台，选择并点击您要上线的 App，就能在 App 详情页面查看到上线（Go Live) 按钮。


![图片](https://open.shopee.com/opservice/api/v1/image/download/?image_id=JlP7Fx1OUllKbKoSbbyZSgL6aG2VM89Jd5kB%2FmA57UYRsI7Tz%2FuSkqellYnvQjizDTV%2FtnUCYiEzHpIzslAF%2Fg%3D%3D&image_type=png)


![图片](https://open.shopee.com/opservice/api/v1/image/download/?image_id=50F95TgxcCRH8w%2F%2FdKD7iv%2FCqAytaiOkiZYRfpM1QSFAeDBUn1m%2FwX4HvXYK47%2F9j%2BWpAmWuMHagr7EbXJuLtQ%3D%3D&image_type=png)


请填写相关信息，提交后，您的 App 将会在24小时完成审核，随后您将会获取到这个 App 对应的 Live partner_id 和 Live key，可用于生产环境。


![图片](https://open.shopee.com/opservice/api/v1/image/download/?image_id=%2BSZrEENAFDIVggqf%2BlKS34XwK3HCShprAl7WZpqHKUaH9UStYV9CC9Dkiwr9FEhNZw0GVV%2BaZ0pcTWXoGLN8Mw%3D%3D&image_type=png)


当您准备就绪，将您的系统切换生产环境只需要完成这些步骤：


1.切换使用 Live partner_id Live key 完成授权；


2.切换使用生产环境的 API 路径，生产环境 API 路径可以每个 API 文档中找到，例如：


![图片](https://open.shopee.com/opservice/api/v1/image/download/?image_id=Rz0X0oq5e36eINAZw%2BSU1U0tKoDadKYGTPmDCfzKo%2B6kSGwbPfMip%2B1ew1d%2BTX3ngx%2FBIzEWkfwU93x5FzyDHQ%3D%3D&image_type=png)


注意：`https://openplatform.shopee.cn/` 为中国大陆开发者开放


            `https://partner.shopeemobile.com/` 为本土开发者开放


请根据您调用 Open API 服务器所在地，选择正确的域名；


*3.（选做）如果您需要订阅 Push 服务，请注意打开生产环境的 Push 服务开关；


*4.（选做）如果您需要添加 Shopee Open API 和消息推送的 IP 地址作为您系统访问的白名单，请调用生产环境`v2.public.get_shopee_ip_ranges`接口获取。

## App 状态说明

| 状态 | 说明 | 正式环境限制 |
| --- | --- | --- |
| Developing | App 开发中 | 1.无法授权正式环境店铺2.无法调用正式环境接口 |
| Online | App 在线中 | 1.可以授权正式环境店铺2.可以调用正式环境接口 |
| New App authorizations restricted | App 限制授权中 | 1.无法授权正式环境店铺2.存量授权关系不影响3.可以调用正式环境接口 |
| API calls restricted | App 限制接口调用中 | 1.无法授权正式环境店铺2.存量授权关系不影响3.不能调用正式环境接口 |
| Suspended | App 离线中 | 1.无法授权正式环境店铺2.存量授权关系解绑3.不能调用正式环境接口 |


*平台会检测开发者的行为，如果违反了平台相关政策，我们将可能您的 App 状态更新为 New App authorizations restricted / API calls restricted / Suspended, 当 App 状态被更新时，您将会收到相关邮件通知，您也可以通过控制台看到相关原因。


*不管是什么状态的 App, 开发者都可以用 Test partner_id 和 Test Key 正常使用沙箱环境进行店铺授权和调用接口。

## 重置 App key


如果您发现您的 partner key 发生了泄漏或者基于安全考虑想更换 partner key, 您可以进入 App 编辑页面，选择将您的 App key 重置。


![图片](https://open.shopee.com/opservice/api/v1/image/download/?image_id=3OeU7ejyR8XcU5C3dCwt2aeQtInmeS%2F1xU3xN%2Fo78E11CpOLq2NMiz2bwQbDql72TB5h0hRTCoetfb9Zad9JOA%3D%3D&image_type=png)


点击 Reset 按钮并点击 Submit，完成重置。


![图片](https://open.shopee.com/opservice/api/v1/image/download/?image_id=L8Jr8nwi6ItIl%2F6mO0JeJrgGzLEop34yzQN%2B2CaSLAFVzqxtwQq9XVw1DLeNxv1ZW7%2FdCHR5KNFzFcdNT1I5lA%3D%3D&image_type=png)

## 删除 App


如果您不再需要某个 App, 您可以选择删除 App, 但是注意删除 App 后之前您获取到的 partner_id 和 key 都将失效，历史绑定过的店铺也将全部解绑，请慎重操作。


![图片](https://open.shopee.com/opservice/api/v1/image/download/?image_id=34ys46baUtBAzrQVDsJoPL%2Br2QjNdCOgy3tCJf8F6og8M7iS59G7w6QoFXtwbPzKEBNfhN9BdBplsv3FlXcDCA%3D%3D&image_type=png)

## 常见问题


问: 我最多能创建多少个 App?


答：我们支持最多创建10个 App。


问：一个 App 可以授权多个市场的店铺吗？


答：可以。


问：一个 App 授权店铺是否有上限？


答：目前我们没有设置上限。


问：支持加快 App 上线的审核进程吗？


答：不支持，请您准备对接生产环境时，将 App 提前24小时上线。


问：如果我系统使用的是动态 IP 地址，我需要如何填 IT 资产？


答：我们推荐使用静态 IP，如果您仍然使用动态 IP，我们会定期让您提供 IT 资产信息供平台进行安全审核，您可以选择”IP 地址不可用”的选项，并备注原因。


![图片](https://open.shopee.com/opservice/api/v1/image/download/?image_id=kLZPSLzJFc8br4gBNkyzkHage3iPMJrm%2FgWmEvCU8jQmnF4GbnoTBMcKoU7ZUIsvCcVvp7pS3rxtZ1ukDu1ObA%3D%3D&image_type=png)


问：我什么时候需要更新 IT 资产？


答：只要您的静态 IP 地址发生了变化，请您在控制台更新您的 IT 资产。


问：我的 IT 资产 IP 地址超过文本框限制的字符数，该如何填写？


答：您可以选择”IP 地址不可用”的选项，备注原因，并提交此表单：`https://shopeeregionalops.typeform.com/to/TLAcHECK?typeform-source=open.shopee.com`


![图片](https://open.shopee.com/opservice/api/v1/image/download/?image_id=614RYPhT1WLeNTr1WB%2FaPQyPQezoyslO%2Frw1ld2LqnY%2FxXIvBFZLfJVRERHVweR2Tw%2FGlE5Zf1TGiXEyotfCBA%3D%3D&image_type=png)

