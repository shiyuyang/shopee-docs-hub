# Shopee Entrega Direta（Shopee 直接配送）

> 来源: [Shopee Open Platform](https://open.shopee.com/developer-guide/290)
> 分类: API Best Practices

## 什么是 Shopee 直接配送渠道？

- 此渠道允许（并要求）卖家进行更快速的配送，例如当日达或次日达；
- 卖家可以自行配送或雇佣快递员配送订单；
- 配送时间由截单时间（由卖家设定）决定，即购买确认的时间（例如，下午 3 点前支付的订单当日送达，下午 3 点后支付的订单次日送达）；
- 当 Shopee Entrega Direta 启用时，卖家将始终有 2 个可用渠道，因为 Shopee Entrega Direta 目前仅服务于 SP 城市。


*注意：此渠道将根据 Shopee 商务团队制定的规则，向选定的卖家开放。更多详情请参阅相关**文章**。*

## OpenAPI 变更

1 - 订单识别（新物流渠道）：

- v2.order.get_order_detail API，"shipping_carrier" 参数："Shopee Entrega Direta"


2 - 卖家可用渠道识别及商品创建：

- v2.logistics.get_channel_list，参数 "logistic_channel_id"：90022


3 - 订单截止时间 (ship_by_date)：

- 由于订单配送截止时间由付款确认时间决定，因此必须确保卖家能够通过 v2.order.get_order_detail API 的 "ship_by_date" 参数获取截止时间。


4 - 商品创建：

- 此渠道永远不会是卖家唯一的可用渠道，因此在创建商品并识别可用渠道时，务必列出所有可用的渠道（例如 Shopee Direct Delivery 和 Standard Delivery）。
- 尝试仅使用一个活跃的物流渠道（即 Shopee Direct Delivery）创建商品将无法实现；


## 物流 HUB

对于帮助卖家管理其物流渠道订单的合作伙伴和物流 HUB（例如 Tracken、Log Manager），以下是集成所需的主要 API 和流程：


1 - 在 Shopee 开放平台创建账户和 APP：

- 要访问卖家的 API 和订单数据，您需要在开放平台创建一个账户。
- 账户创建后，创建一个 APP（建议选择 ERP System 类型以访问所有 OpenAPI 功能），并在开始调用 API 之前将卖家连接到您的账户；
- 这些流程在以下文章中有更详细的说明：
 - 开发者账户注册
 - App 管理
 - 授权与认证


2 - 推荐的 API 和 Webhook (Push)：

- v2.order.get_order_list - 用于识别订单；
- v2.order.get_order_detail API - 用于获取订单详情，是查看订单物流渠道的唯一方式（通过 "shipping_channel" 参数，将返回 "Shopee Entrega Direta"）；
- v2.logistics.get_tracking_number API - 用于识别订单运单号；
- v2.logistics.ceate_shipping_document - 用于创建面单（注意，卖家的 ERP 可能已经调用此接口，可能无需重复调用）；
- v2.logistics.get_shipping_document_result - 用于检查面单是否已成功创建并可下载；
- v2.logistics.download_shipping_document API - 用于下载运单面单；
- order_status_push - 用于在新订单创建或订单状态更新时接收通知；
- order_tracking_push - 用于在运单号已创建时接收通知；
- shipping_document_status_push - 用于在面单准备就绪可供下载时接收通知；


以下是关于 Shopee 订单流程的更多文章链接：

- OpenAPI Logistics API Step by Step
- API Call Flows

## FAQ：

1 - 所有卖家都可以使用 Shopee Entrega Direta 渠道吗？


A：只有托管卖家可以访问该渠道，更多信息请联系您的客户经理。


2 - 使用 Shopee Entrega Direta 渠道是否必须发送发票？


A：该渠道要求正常发送发票、安排发货和生成面单。


3 - v2.order.get_order_detail API 中的数据脱敏，为什么会发生这种情况？


A：a) 买家数据是敏感数据，仅在订单处于 READY_TO_SHIP 和 TO_RETURN 状态时提供。


b) 如果在 APP 级别未填写 IP 白名单（来自开放平台 Console），数据可能会被脱敏；填写后，数据将自动可用（前提是处于正确的状态）。


有关 OpenAPI 的其他问题，您可以在 OP Ticketing Platform 上提交 ticket。
