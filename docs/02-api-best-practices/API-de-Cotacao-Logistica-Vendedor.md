# API de Cotacao (卖家物流报价)

> 来源: [Shopee Open Platform](https://open.shopee.com/developer-guide/286)
> 分类: API Best Practices

## 什么是卖家物流渠道

此渠道允许卖家使用自己的物流进行报价和订单发货。

- 运费报价基于卖家提供的报价 URL 进行。
- 运费和配送时效由卖家自行提供。
- 订单追踪得到简化，卖家负责通过 OpenAPI 发送"已发货"、"已送达"或"配送失败"等事件。


***注意：**此渠道将提供给特定卖家，这些卖家的产品因尺寸和重量不受 Shopee 自有物流支持，具体规则由 Shopee 商务团队制定。*

## 运费报价 URL

此工具允许卖家向 Shopee 发送预估的运费和时效，这些信息将在购买时显示给买家。卖家要使用此功能，需要满足预先设定的认证要求。


**卖家可以选择直接与 Shopee 集成以连接其报价 URL，或通过集成商-HUB 连接。**

## 认证/集成要求

与其他类型的集成不同，报价 API 和订单状态更新（卖家物流渠道）的集成需要 Shopee 团队评估和批准后方可开始运营。要获得 Shopee 团队的批准，需要满足以下条件：

- 遵守运费报价 API 合同：
 - 通过 HTTP POST 方法配置并提供 URL。
 - 每个请求 (request) 只能包含一个卖家的一个商品。
 - URL 没有特定的结构，提供配置灵活性。
- 报价请求和响应的标准 payload（以及使用 Shopee URL 进行验证）
- 响应时间限制为 400ms。
- 通过卖家中心直接注册应急运费表。
- 错误监控（并开发所需的消息提示）
- 开发状态更新 API ("update_tracking_status")；
 -***注意：**上述要求必须由卖家的"自有系统"或其 ERP/HUB/集成方案满足。需要强调的是，如果没有这些，订单将被取消，因为无法通过卖家中心手动完成流程。*
 -***注意 2：**所有开发报价 API 的人也必须开发状态更新 API；*
 -***注意 3：**Seller Logistics APP 仅用于报价 URL，要使用任何 API，需要创建第二个 APP；*
- 通过 ticket 从 Shopee 团队获得确认和批准邮件（涵盖上述所有标准）。


要进行上述集成和测试，还需要：


a) 在开放平台创建新的 Seller Logistic APP 并将卖家授权到此 APP


b) 拥有一个能够调用 OpenAPI 进行状态更新的 APP（并将卖家授权到此 APP）


***完成所有这些步骤后，需要创建至少 2 个测试订单，这些订单需要经历到已送达和已取消状态，以便 HUB 获准成为一个经过批准的渠道。**

## 创建 Seller Logistics APP 并授权卖家

一旦您的开放平台账户处于激活状态，下一步是创建一个仅用于将您的报价 URL 连接到 Shopee 及其相关卖家 (shop_id) 的 APP。


请按以下步骤操作：


1. 登录开放平台并进入 "Console" 选项卡：


![图片](https://open.shopee.com/opservice/api/v1/image/download/?image_id=8dhYhblm%2FlT3sEGKh5synM1mGE7qxTcXnRgX2qr%2B1miAs7MhkfJsLepUtX9XcStrTyRmX8aOWC4yvGKBV5i8xw%3D%3D&image_type=png)


2. 在 "App List" 中点击 "+ Add new APP"：


![图片](https://open.shopee.com/opservice/api/v1/image/download/?image_id=BtBro5U%2BNrU9jHhAb9RpFjJ5GmTfZqPTiLaPOlBFOyv9S%2F0Zf7azJkPoAco%2FHbK%2FTQgZ6r1%2FKdLXgGAQeQ0e4g%3D%3D&image_type=png)


3. 选择 "App Category" 为 "Seller Logistics"：


![图片](https://open.shopee.com/opservice/api/v1/image/download/?image_id=Sv5yW4Y%2F8xvWECI296njkyyMjHqfNJaml2ZchYPSi5ic5qHWFrc1mw82SkGGdApJMehI7pUOwUA8xZHDQ%2Bjg7A%3D%3D&image_type=png)


4. 在 "App Description" 中输入将在生产环境 (Live) 和测试环境 (Test) 中使用的 URL，然后点击 "Submit"。


*如果只有一个 URL 也没有问题；


![图片](https://open.shopee.com/opservice/api/v1/image/download/?image_id=SDzAxRWWV3Jw3M0LHU1vrMW%2Fgu%2BpMgu%2F5UN5AuvACe1nV1%2BsWSaUR4C5KdjUgBUn3jXkuceu8fFoAIr8jxLSPg%3D%3D&image_type=png)


5. APP 即创建完成，然后继续进行 "Go-Live" 请求，APP 将在最多 24 小时内可在生产环境中使用。


![图片](https://open.shopee.com/opservice/api/v1/image/download/?image_id=i%2BNnpU4d3%2Fg81BlB643wC1WpAsWxeqG7xK11%2BryzeFpzTWPYYVq3yxEvYPJzZ7V%2FaaV4Lxfc%2Fgl13VC6UOPDGg%3D%3D&image_type=png)


6. 只需在之前填写一些额外信息。


如果无法提供 "username" 和 "password"，可以按如下截图填写：


![图片](https://open.shopee.com/opservice/api/v1/image/download/?image_id=So38FJiibg0jTVT62sS8PvZkMtpb7PfayVf1b12SxUrLazGJdYSkQgPZZv9VLJ512Q22KMRKQzAyG8Pg3JgkKg%3D%3D&image_type=png)


7. "App IP" 填写您应用的主 IP（请注意，我们不会将访问仅限制于此 IP）。


"Other IT Assets Declaration" 按如下截图填写：


![图片](https://open.shopee.com/opservice/api/v1/image/download/?image_id=Jx8ukNF5yojqAm6sTTwJvtqVwqyHDDzmLg%2FpY7003hPkLDzXbxUrwBIZBStYDNxWmS0AITs8W9E2GlK3nWi2fQ%3D%3D&image_type=png)


提交 "Go-live" 请求 24 小时后，Live 环境下的 partner_id 将会释放，您将通过电子邮件收到通知。收到邮件后，下一步是：


1 - 在 OP Ticketing Platform 上提交 ticket，主题为 "Seller Logistics"，说明您计划连接报价 URL 的 shop_id（或哪些 Shop ID）。我们收到请求后，Shopee 团队将完成 URL 连接，并允许您继续卖家授权。


注意：每个 shop_id 在 Shopee 上只能连接一个 URL；


2 - 按照链接中的步骤（直到"使用店铺账户授权"的第 4 点）为您的卖家执行授权流程。


3 - 一旦 Shopee 团队回复您的 ticket，确认配置已完成并且您的卖家已完成授权流程，即可在生产环境中进行首次测试。


### 报价请求和响应的标准 payload
#### 请求参数 (query)


URL 请求参数：

| - | 示例 | HTTP 地址 |
| --- | --- | --- |
| URL | https://api.frete/ | ERP 或卖家提供的 URL |
| 名称 | 类型 | 示例 | 描述 |
| --- | --- | --- | --- |
| partner_id | int | 1 | 合作伙伴 ID，注册成功后分配。所有请求必填。 |
| timestamp | timestamp | 1610000000 | 请求的时间戳。所有请求必填。5 分钟后过期。 |
| sign | string | e318d3e932719916a9f9ebb57e2011961bd47abfa54a36e040d050d8931596e2 | 基于字符串 "{}{}{}"%(partner_id, api full path, timestamp) 和 partner_key 通过 HMAC-SHA256 算法生成的签名。更多详情：`https://open.shopee.com/documents?module=87&type=2&id=58&version=2` |


Body 请求参数：

| 名称 | 类型 | 必填 | 示例 | 描述 |
| --- | --- | --- | --- | --- |
| shop_id | int | True | 112345678 | 每个卖家的唯一标识符 |
| origin_zip_code | string | True | 12345000 | 卖家邮编（8 位数字，仅数字，无句点和连字符） |
| destination_zip_code | string | True | 12345000 | 买家邮编（8 位数字，仅数字，无句点和连字符） |
| items | array | True | - | 产品列表 |
| | item_id | int | True | 12345678 | Shopee 上的商品 ID |
| | sku | string | False | item_sku | 卖家在 Shopee 上注册的 SKU |
| | model_id | int | False | 12345678 | Shopee 上注册的模型 ID。***注意：**在 PDP 报价中，model_id 和 category_id 发送为零，但在结账页面正常发送*。 |
| | category_id | int | True | 12345678 | Shopee 上注册的商品类别。***注意：**在 PDP 报价中，model_id 和 category_id 发送为零，但在结账页面正常发送* |
| | quantity | int | True | 12345678 | 商品数量 |
| | price | float | False | 150.4 | 产品价格 |
| | dimensions | object | True | - | 产品尺寸 |
| | | length | int | True | 10 | 长度（厘米） |
| | | width | int | True | 10 | 宽度（厘米） |
| | | height | int | True | 10 | 高度（厘米） |
| | | weight | int | True | 100 | 重量（克） |


响应参数 / 报价响应（错误）：

| 名称 | 类型 | 必填 | 示例 | 描述 |
| --- | --- | --- | --- | --- |
| error | string | True | - | 卖家报价的标识符 |
| message | string | True | - | 买家邮编 |
| request_id | string | True | - | API 调用的标识符 |


响应参数 / 报价响应（成功）：

| 名称 | 类型 | 必填 | 示例 | 描述 |
| --- | --- | --- | --- | --- |
| quotation_id | int | True | 091234000 | 卖家报价的标识符 |
| destination_zip_code | string | True | 091234000 | 买家邮编 |
| packages | array | True | - | 包裹列表 |
| | dimensions | object | True | - | 产品尺寸 |
| | | length | int | True | 10 | 长度（厘米） |
| | | width | int | True | 10 | 宽度（厘米） |
| | | height | int | True | 10 | 高度（厘米） |
| | | weight | int | True | 100 | 重量（克） |
| | items | array | True | - | 产品列表 |
| | | item_id | int | True | 12345678 | Shopee 上的商品 ID |
| | | sku | string | False | sku_item | 卖家在 Shopee 上注册的 SKU |
| | | model_id | int | False | 12345678 | Shopee 上注册的模型 ID |
| | | category_id | int | False | 12345678 | Shopee 上注册的商品类别 |
| | | quantity_id | int | True | 2 | 商品数量 |
| | | price | int | True | 150.4 | 产品价格 |
| | | dimensions | object | True | - | 产品尺寸 |
| | | | length | int | True | 10 | 长度（厘米） |
| | | | width | int | True | 10 | 宽度（厘米） |
| | | | height | int | True | 10 | 高度（厘米） |
| | | | weight | int | True | 100 | 重量（克） |
| | quotations | array | True | - | 运费报价列表 |
| | | price | float | True | 150.4 | 显示给买家的运费金额 |
| | | handling_time | int | True | 20 | 订单准备时间（工作日）。必须始终大于或等于 1。此时间限制了卖家开具发票和组织发货的时间。 |
| | | shipping_time | int | True | 10 | 订单运输时间（工作日） |
| | | promise_time | int | True | 30 | 准备时间 + 运输时间的总和 |
| | | service_code | string | True | M1020 | 标识卖家上下文中的承运商的代码（该代码将返回在 get_order_detail API 的 "shipping_carrier" 参数中，例如："Logistica do Vendedor - M1020"。） |
#### 请求示例

```curl
curl --location 'https://api.frete/?partner_id=123456&sign=6b664c45535a544455524f6b565776706752784455784978574361444e795a4c&timestamp=1709843385' \--header 'Content-Type: application/json' \--data '{ "shop_id": 601216389, "origin_zip_code": "87952525", "destination_zip_code": "17036785", "items": [ { "item_id": 892569034, "model_id": 1, "sku": "", "category_id": 1, "quantity": 1, "price": 12.5, "dimensions": { "length": 1, "width": 1, "height": 1, "weight": 150 } } ]}'
```

#### 成功返回示例

- 使用 HTTP 状态码 200

```json
{ "quotation_id": 1709843321, "destination_zip_code": "17036785", "packages": [ { "dimensions": { "length": 35, "width": 90, "height": 114, "weight": 27300 }, "items": [ { "item_id": 892569034, "model_id": 1, "sku": "", "category_id": 1, "quantity": 1, "price": 12.5, "dimensions": { "length": 1, "width": 1, "height": 1, "weight": 150 } } ], "quotations": [ { "price": 93.55, "handling_time": 1, "shipping_time": 7, "promise_time": 8, "service_code": "50" } ] } ]}
```

#### 错误返回示例

- 使用 HTTP 状态码 403

```json
{ "request_id": "Id da requisicao", "error": "coluna Error", "message": "coluna Message"}
```

#### 错误表中未映射的错误的默认返回

- 使用 HTTP 状态码 500

```json
{ "request_id": "65e9e26dd9d2565e9e26dd9d64", "error": "Internal system error", "message": "internal system error"}
```

#### 预期返回代码
|**HTTP 状态码**|**Error**|**Message**|**触发应急方案**|
| --- | --- | --- | --- |
| 200 | success API call, error Empty | success API call, error Empty | False |
| 403 | error_partner_id | there is no partner_id in query | False |
| 403 | error_partner_id | partner_id is invalid | False |
| 403 | error_sign | there is no sign in query | False |
| 403 | error_sign | your sign is invalid | False |
| 403 | error_timestamp | there is no timestamp in query | False |
| 403 | error_timestamp | your timestamp is invalid | False |
| 403 | error_shop_id | there is no shop_id in body | False |
| 403 | error_shop_id | The shop_id is invalid | False |
| 403 | Invalid origin_zip_code | The origin_zip_code is invalid | False |
| 403 | invalid destination_zip_code | The destination_zip_code is invalid | False |
| 403 | error_destination_zip_code | No shipping channel is available. | False |
| 403 | Invalid item_id | The item_id is invalid | False |
| 403 | Invalid model_id | The model_id is invalid | False |
| 403 | Invalid sku | The sku is not valid | False |
| 403 | invalid category_id | The category_id is invalid | False |
| 403 | invalid quantity | The quantity is invalid | False |
| 403 | invalid price | The price is invalid | False |
| 403 | error_dimensions | The dimensions is invalid | False |
| 403 | error_length | The length is invalid | False |
| 403 | error_width | The width is invalid | False |
| 403 | error_height | The height is invalid | False |
| 403 | error_weight | The weight is invalid | False |
| 500 | Internal system error | internal system error | True |

#### 响应验证（使用 Shopee URL）
- 为确保响应格式符合预期，我们提供一个用于验证和告知所需更正的 URL。
- URL: "https://seller-quotation-api.uat.shps-br-services.com/validate_quotation_endpoint"
- 参数 "x-quotation-id" 中应填入将在 Shopee 注册的 URL。
- 以下是使用响应格式验证 URL 的示例 payload：

```json
curl --location 'https://seller-quotation-api.uat.shps-br-services.com/validate_quotation_endpoint' \--header 'api-key: 8a50d1d005d0649b5bdd9b13f0e871e0bd6439bd8e146577a6d51935a5ccea7c' \--header 'x-partner-id: 2007416' \--header 'x-quotation-api-url: https://api.cotacao/shopee' \--header 'x-sign: 658ABD0FD8D8525C0A87B0E360A5C518C2987E5B4A3D20542A4B11594E11CE53' \--header 'Content-Type: application/json' \--data '{ "shop_id": 549724933, "origin_zip_code": "16200850", "destination_zip_code": "16200850", "items": [ { "item_id": 10010394, "sku": "10010394", "model_id": 1, "category_id": 1, "quantity": 1, "price": 277.67, "dimensions": { "length": 1, "width": 1, "height": 1, "weight": 10 } } ]}'
```


- 无错误的响应（可通过 "validation_errors" 参数为空来识别："validation_errors:[]"）：

```json
{ "validation_errors": [], "details": { "called_api": "https://api.cotacao/shopee", "with_params": { "sign": "658ABD0FD8D8525C0A87B0E360A5C518C2987E5B4A3D20542A4B11594E11CE53", "partner_id": 2007416, "timestamp": 1713445311 }, "with_body": { "shop_id": 549724933, "origin_zip_code": "16200850", "destination_zip_code": "16200850", "items": [ { "item_id": 10010394, "model_id": 1, "sku": "10010394", "category_id": 1, "quantity": 1, "price": 277.67, "dimensions": { "length": 1, "width": 1, "height": 1, "weight": 10 } } ] }, "response_from_quotation_api": { "status_code": 200, "response_body": { "quotation_id": 617788888, "destination_zip_code": "16200850", "packages": [ { "dimensions": { "length": 1, "width": 1, "height": 1, "weight": 10 }, "items": [ { "item_id": 10010394, "sku": "10010394", "model_id": 1, "category_id": 1, "quantity": 1, "price": 277.67, "dimensions": { "length": 1, "width": 1, "height": 1, "weight": 10 } } ], "quotations": [ { "price": 34.9, "handling_time": 5, "shipping_time": 10, "promise_time": 20, "service_code": "2018605604" } ] } ] }, "method_called": "POST" } }}
```


- 包含需要更正的错误示例的响应：

```json
{ "validation_errors": "Input should be a valid string: ('error',)", "details": { "called_api": "https://api.cotacao/shopee": { "sign": "658ABD0FD8D8525C0A87B0E360A5C518C2987E5B4A3D20542A4B11594E11CE53", "partner_id": 2007416, "timestamp": 1713472133 }, "with_body": { "shop_id": 549724933, "origin_zip_code": "16200850", "destination_zip_code": "16200850", "items": [ { "item_id": 10010394, "model_id": 0, "sku": "10010394", "category_id": 1, "quantity": 1, "price": 277.67, "dimensions": { "length": 1, "width": 1, "height": 1, "weight": 10 } } ] }, "response_from_quotation_api": { "status_code": 403, "response_body": { "request_id": "17134721330005", "error": 403, "message": "there is no partner_id in query", "msger": "Nao foi possivel concluir sua solicitacao." }, "method_called": "POST" } }}
```


### 报价响应时间限制

- 考虑到结账是用户购买体验中最为关键的环节，确保为买家提供最佳体验至关重要。
- 响应时间限制为 1 秒。需要进行负载测试以确保满足此要求。
- 超过 1 秒的响应时间将不被允许，可能导致集成失败。因此，保持此参数的优化是为买家提供最佳体验的关键因素。
## 应急运费表

- 此功能旨在支持在通过 API 进行运费报价时出现问题时（超时或返回 500 的请求）计算运费。
### 应急运费金额设置

- 为使应急方案生效，卖家需要按照以下步骤注册运费金额并启用**卖家物流**渠道。
- 在卖家中心，访问**配送设置**并点击**渠道配置**按钮：

![图片](https://open.shopee.com/opservice/api/v1/image/download/?image_id=axLhajSfgEBV5VxcLQac2I4DJ819EKiVG4BaFBpeX7tyXMFC2yOiY%2FZBjpzXXh3sXL0w14jP4jGdv%2FBXysWqdw%3D%3D&image_type=png)

### 填写应急运费金额


接下来，将加载填写运费金额的页面。运费金额可以按州（单一金额）或按地区填写。

### 按州单一运费金额

1. 选择州
1. 填写运费金额字段
1. 点击保存

![图片](https://open.shopee.com/opservice/api/v1/image/download/?image_id=iqTvUj9g1dDUR6lK8Pwvg8k9uw%2Fq5EE7RaMwhoFeOlbziKeMF0U%2BO8VSx0R%2BeUrSgXDYT0TDrFeS%2F%2FBQIe%2BGgg%3D%3D&image_type=png)

### 按城市单一运费金额

1. 选择州
1. 禁用 *Flat rate for this area* 按钮
1. 取消勾选 *Select All Cities* 选项，选择您要填写运费金额的城市
1. 填写相应城市的 *Rate* 字段
1. 点击 *Salvar*

![图片](https://open.shopee.com/opservice/api/v1/image/download/?image_id=sZze5JgkTw23vTywAHTztpHkGHSM9rxVpFct3lL9NiVPSh5rmsN27ykkw4C88%2BpqFmPwPBpyKfaEKPsnrJ9OYw%3D%3D&image_type=png)

### 启用卖家物流渠道

![图片](https://open.shopee.com/opservice/api/v1/image/download/?image_id=GQqkuXNOHGSpwREwhv0g2lS9mxDBBwrUyEFQCb5OQVo05wb8tAC2k7w1Cs1Jd8b6XthNygVM2H4abUA0sYKzwg%3D%3D&image_type=png)

### 应急运费金额的配送时效

- 当应急运费表被触发时，配送时效将固定：
 - 最短时效：10 个自然日
 - 最长时效：20 个工作日
## 订单状态与追踪
### 开发状态更新 API：


订单状态和追踪的更新将通过追踪更新 API 进行，基于在 Shopee 上创建的订单号（订单 ID，也称为 OrderSN）。同时必须提供追踪号码。


要更新追踪号码和订单状态，应使用端点***v2.logistics.update_tracking_status (OpenAPI)***。可能的状态包括：

1. 订单已发货 (logistics_pickup_done)
 - URL 和追踪号码可以在订单状态更新为已发货时发送。
1. 订单已送达 (logistics_delivery_done)
 - 只有在订单已处于已发货状态时，才能接收已送达状态。
1. 配送失败 (logistics_delivery_failed)
 - 只有在订单已处于已发货状态时，才能接收配送失败状态。


***重要提示**：发送订单已送达或配送失败状态后，将不再允许更新状态，因为两者均为最终状态；*

**参数****tracking_number****和****tracking_url****应仅在状态更新为****logistics_pickup_done****时发送。**


*以下是 "/api/v2/logistics/update_tracking_status" 的文档链接。*

## 渠道订单流程和状态

![图片](https://open.shopee.com/opservice/api/v1/image/download/?image_id=HlNk8Kk68dG3rPlRrgb8OWB34bmSuKnrsCJ853GXcbyVIwQuLCgjCC%2Bodz65bQANuqyn3AQ1Y53h6LPXIVE3dg%3D%3D&image_type=png)


## 
## 渠道的佣金和运费规则

- 如果卖家参加了免运费计划，买家可享受的最高运费折扣为 R$ 20
- 卖家将共同承担提供给客户的折扣。

![图片](https://open.shopee.com/opservice/api/v1/image/download/?image_id=up740NiZdB4UHEVPAFbqCvpVwa056ylU1CFeHpzc6b3gvhCcXjSAUdGiVrz2ZZQzKEyODTGilTg%2FlmU7vWLR7Q%3D%3D&image_type=png)

## FAQ：


1 - 所有卖家都可以使用卖家物流渠道吗？


A：只有托管卖家可以访问该渠道，更多信息请联系您的客户经理。


2 - 如何在订单中识别报价？


A：订单成功使用报价创建后，"service_code" 参数将返回在 get_order_detail API 的 "shipping_carrier" 参数中。


示例 1：

- 发送的 "service_code"："Canal X"
- "shipping_carrier" 参数返回："Logistica do vendedor - Canal X"

示例 2：

- 应急运费表已激活。
- "shipping_carrier" 参数返回："Logistica do vendedor"


3 - 我可以使用 Seller Logistics APP 调用 OpenAPI 吗？


A：不能，此类 APP 仅用于报价 API（报价 URL）。


更多技术问题，请在 OP Ticketing Platform 上提交 ticket。


有关物流渠道访问的疑问，请点击链接。
