# Instant Mart 集成指南

> 来源: [Shopee Open Platform](https://open.shopee.com/developer-guide/643)
> 分类: API Best Practices


本文档介绍在**Instant Mart**上的**产品上架、订单管理、收入报告以及 OpenAPI 集成/测试流程**。

## Instant Mart 项目说明
## 背景：

Instant Mart 是一种特殊的店铺结构，旨在支持同时经营中央管理和分支运营的零售商。在此模式下：

- 每个**Mart Shop（官方店铺）**充当总部，负责管理全局 SKU、创建商品以及查看财务报告。
- 多个**Outlets（分支店铺）**存在于 mart 下，代表各个门店。Outlets 负责处理日常运营，如管理订单、维护库存以及打包包裹供骑手取件。

通过开放 API 集成，Mart 零售商可以选择在**商家级别**（所有 outlet 共享）或在**outlet 级别**（每个分支独立）管理 SKU。


在集成开放 API 之前，零售商必须在**BDC 门户**中注册 mart 商家及其 outlet 店铺，确保它们被注册为**Instant Mart 店铺**。此设置允许开发者构建支持 Instant Mart 零售商完整运营流程的 API 解决方案。

## 1. Sandbox 测试账户设置
### 1.1 创建 Sandbox 测试账户


您可以首先访问 Shopee 开放平台 Console 的 Test Account 页面，选择 Mart&Outlet shops 模块创建测试店铺。


![图片](https://open.shopee.com/opservice/api/v1/image/download/?image_id=4TzCsTwtDQ7%2BbrHmBiv2wO74k7zl3ocgiObjIuqYeHHm6DP%2BF%2BY1BFilYTGbZ5kJyJk0ZnIJaPE2ymmpoKgxxQ%3D%3D&image_type=png)


*注意：Instant Mart sandbox 测试需要两步白名单：必须先启用 Sandbox V2，然后才能启用 Mart & Outlet Shop 白名单。*


## 2. 授权
### 2.1 店铺授权

在 App List 页面上找到测试 Partner_id：


![图片](https://open.shopee.com/opservice/api/v1/image/download/?image_id=yEKxhEtVO5NjTjcEj0vZW5ft8AW0c2LH%2Ff8lhCtV2kWT8MDAdMQjo6rDYXHYfE%2FCp2FNqzobx8b428sxRKCymA%3D%3D&image_type=png)


点击**Authorize** -> 使用 Mart 账户登录，同时完成 Mart 和 Outlet 店铺的授权。


![图片](https://open.shopee.com/opservice/api/v1/image/download/?image_id=%2F%2B3zcfqIRFEFtd%2FlWpYcj6N2hOfAkrxSbh2AzkqAhrvRlxlEhxot8OoMyjrzJyp1B6Ht3jk%2FzshoXEXDU1A%2FBQ%3D%3D&image_type=png)


![图片](https://open.shopee.com/opservice/api/v1/image/download/?image_id=U9N3Nqqn2Gq5NgqFeD54EbO9I%2B1ek9mYRf2wfGDDKhCnUAJjcPKaikkbSHf1FUm3iFEWMp4C%2BD23puxgY9%2BOjg%3D%3D&image_type=png)


更多信息请参考授权与认证文章。

## 3. 测试流程
### 3.1 开放 API 测试

使用 API 测试工具或 Postman 测试开放 API。


![图片](https://open.shopee.com/opservice/api/v1/image/download/?image_id=6z6B8dxwUHyrzbPC2KsRwYC8uH7I%2BE%2BoJ6hHhGIZYhMwcGdEscf3JfzpnzMLwvRQxAqw7a8QI0%2FSmOfLL2yNrA%3D%3D&image_type=png)


### 3.2 关键开放 API 功能


**ID Mart 项目所需的关键 API 功能：**

|**板块**|**子板块**|
| --- | --- |
| 产品 (Product) | 新 SKU 准备 |
| 创建新 SKU |
| 更新现有 SKU |
| 创建 SKU 变体 |
| 库存与价格管理 |
| 通用 SKU 管理 |
| 订单 (Order) | 获取订单列表与详情 |
| 取消订单 |
| 请求发货 |
| 生成运单号 |
| 生成航空运单 |
| 退货退款 (Return & Refund) | 获取退货列表与详情 |
| 接受退货/退款 |
| 争议退货/退款 |
| 财务 (Financials) | 获取托管详情 |
| 获取钱包交易 |
| 生成收入报表 |
| 生成收入报告 |
| 店铺设置 (Shop Setting) | 店铺资料更新 |
| 店铺营业时间 |
#### 3.2.1 Mart&Outlet 店铺关系

**检查关系**：v2.shop.get_shop_info 使用 **mart_shop_id** -> 返回该 Mart 下的所有 outlet 店铺 ID。使用 **outlet_shop_id** -> 返回对应的 Mart 店铺 ID。


3.2.1.1 使用 Mart 店铺调用 v2.shop.get_shop_info


使用 mart_shop_id 调用 v2.shop.get_shop_info 时，将返回该 Mart 店铺下的所有 Outlet 店铺 ID 列表。


响应示例：


{
    "auth_time": 1755082218,
    "error": "",
    "expire_time": 1786636799,
    "is_cb": false,
    "is_direct_shop": false,
    "is_main_shop": false,
    "is_mart_shop": true,
    "is_one_awb": false,
    "is_outlet_shop": false,
    "is_sip": false,
    "is_upgraded_cbsc": false,
    "linked_direct_shop_list": [],
    "linked_main_shop_id": 0,
    "merchant_id": null,
    "message": "",
    "outlet_shop_info_list": [
        {
            "outlet_shop_id": 225622030
        },
        {
            "outlet_shop_id": 225622031
        },
        {
            "outlet_shop_id": 225622032
        },
        {
            "outlet_shop_id": 225622033
        },
        {
            "outlet_shop_id": 225622034
        }
    ],
    "region": "TH",
    "request_id": "e3e3e7f33c4e6283bc127a54263d8c01",
    "shop_fulfillment_flag": "Others",
    "shop_name": "op_64564962416254514c64",
    "status": "NORMAL"
}


3.2.1.2 使用 Outlet 店铺调用 v2.shop.get_shop_info


使用 outlet_shop_id 调用 v2.shop.get_shop_info 时，将返回对应的 Mart 店铺 ID。


响应示例：


{
    "auth_time": 1755158035,
    "error": "",
    "expire_time": 1786723199,
    "is_cb": false,
    "is_direct_shop": false,
    "is_main_shop": false,
    "is_mart_shop": false,
    "is_one_awb": false,
    "is_outlet_shop": true,
    "is_sip": false,
    "is_upgraded_cbsc": false,
    "linked_direct_shop_list": [],
    "linked_main_shop_id": 0,
    "mart_shop_id": 225621997,
    "merchant_id": null,
    "message": "",
    "region": "TH",
    "request_id": "e3e3e7f33c4e97dc9f31cfda55db5101",
    "shop_fulfillment_flag": "Others",
    "shop_name": "op_51505343495178456857",
    "status": "NORMAL"
}


#### **3.2.2 产品管理**

![图片](https://open.shopee.com/opservice/api/v1/image/download/?image_id=fBmZsM7SsehtYieQ5xO6XkNZcVPvGWTiCnvysTgeRmsz9tNnfh5%2FnpetQRG4S7HMCPcczjn%2FKeR92pQ88%2BEFjA%3D%3D&image_type=png)


Mart SKU 和 Outlet SKU 的字段区分

|**模块**|**字段**|**MART SKU 管理**|**Outlet SKU 管理**|
| --- | --- | --- | --- |
| 基本信息 | title | Yes | No |
| video | Yes | No |
| image | Yes | No |
| status | Yes | Yes |
| category | Yes | No |
| 规格 | brand | Yes | No |
| attribute | Yes | No |
| size chart | Yes | No |
| 规格 | variation name | Yes | No |
| variation option | Yes | No |
| variation image | Yes | No |
| price | No | Yes |
| purchase limit | No | Yes |
| wholesales | No | Yes |
| stock | No | Yes |
| model status | Yes | Yes |
| 模块 | seller SKU | Yes | No |
| weight | Yes | No |
| dimension | Yes | No |
| 配送 | logistics channel | No | Yes |
| installation channel | No | Yes |
| 其他 | DTS | No | Yes |
| seller SKU | Yes | No |
| condition | Yes | No |

**关键操作包括：**1.添加 Mart SKU -> v2.product.add_item2.更新 SKU 库存/价格 -> v2.product.update_stock, v2.product.update_price（仅在 outlet 级别）3.发布 Outlet SKU -> v2.product.publish_item_to_outlet_shop4.同步 Mart SKU 到 Outlet SKU -> v2.product.update_item


3.2.2.1 添加 Mart SKU


通过使用 mart shop_id 调用 v2.product.add_item 添加 mart SKU。


**更多信息请参考****创建产品****文章。**


**调用示例：**


{
    "original_price": 123.3,
    "description": "rachel add item from openapi 002",
    "weight": 1.1,
    "item_name": "rachel add item from openapi item 001",
    "item_status": "NORMAL",
    "dimension": {
        "package_height": 2,
        "package_length": 3,
        "package_width": 4
    },
    "category_id": 400091,
    "logistic_info": [{
        "size_id": 0,
        "shipping_fee": 2.5,
        "enabled": true,
        "logistic_id": 80018,
        "is_free": false
    },
    {
        "size_id": 0,
        "shipping_fee": 2.5,
        "enabled": true,
        "logistic_id": 81014,
        "is_free": false
    }],
    "image": {
        "image_id_list": ["c54265d475b85e00ffb2404585e32b6f", "6fb33d484f232510b5f9b169f2758322", "591ab15ea954b9879374765854595600", "00a2258551b5a2f0a7c283f877330f93", "abf02b19b42e4aa964ef0725491ca9e3", "730f45972377cd4eb9813c6e53e60e9a"]
    },
    "pre_order": {
        "is_pre_order": false,
        "days_to_ship": 2
    },
    "item_sku": "item sku 001",
    "condition": "NEW",
    "brand": {
        "brand_id": 0,
        "original_brand_name": "no brand"
    },
    "item_dangerous": 0,
    "description_info": {
        "extended_description": {
            "field_list": [{
                "field_type": "text",
                "text": "rachel add item from openapi 001",
                "image_info": {
                    "image_id": "-"
                }
            },
            {
                "field_type": "image",
                "text": "-",
                "image_info": {
                    "image_id": "c54265d475b85e00ffb2404585e32b6f"
                }
            }]
        }
    },
    "description_type": "extended",
    "seller_stock": [{
        "location_id": "IDZ",
        "stock": 555
    }]
}


3.2.2.2 更新 Mart SKU 库存/价格


通过调用 v2.product.update_stock 或 v2.product.update_price 更新 Mart SKU 库存和价格。


**更多信息请参考****库存与价格管理****文章。**


*注意：库存和价格只能在 outlet 店铺级别进行管理。调用 API 更新库存或价格时，必须提供 outlet 店铺的 shop_id。*


3.2.2.3 发布 Outlet SKU


调用 v2.product.publish_item_to_outlet_shop 发布 outlet SKU。


**调用示例：**


{
    "mart_item_id": 1234,
    "outlet_shop_id": 2345,
    "publish_item": {
        "model": [
            {
                "relate_mart_model_id": 1234,
                "original_price": 123,
                "seller_stock": [
                    {
                        "location_id": "IDZ",
                        "stock": 100
                    }
                ],
                "pre_order": {
                    "is_pre_order": false,
                    "days_to_ship": 3
                }
            }
        ],
        "logistic_info": [
            {
                "logistic_id": 12345,
                "enabled": true,
                "shipping_fee": 3.45,
                "size_id": 0,
                "is_free": false
            }
        ]
    }
}


调用 v2.product.get_item_base_info 检查 outlet 商品信息是否正确同步。


**请参考****产品基础信息管理****文章查看商品信息。**


3.2.2.4 获取商品映射信息


当 mart SKU 已发布到 outlet SKU 时，调用 v2.get_mart_item_mapping_by_id 获取商品映射信息。


**调用示例：**


{
    "mart_item_id": 844087076,
    "outlet_shop_id_list": [
        225034791
    ]
}


3.2.2.5 同步 Mart SKU 到 Outlet SKU


**将 mart sku 字段同步到 outlet sku。**


1.调用 v2.product.update_item 更新 mart 商品字段。
2.调用 v2.product.get_item_base_info/进入 outlet 店铺卖家中心检查 outlet 商品信息是否正确同步。


*注意：只有 mart sku 管理的字段才能同步到 outlet sku。*

#### 3.2.3 印尼即时配送渠道依赖关系

3.2.3.1 渠道结构概述


|**掩码渠道**|**物流渠道**|
| --- | --- |
| 8000 - Instant | 80012 - GoSend Instant80019 - GrabExpress Instant80044 - SPX Instant |
| 8008 - Instant 2 hours | 80054 - SPX Instant - 2 Jam80061- GrabExpress Instant - 2 Jam80063- GoSend Instant - 2 Jam        |
| 8007 - Instant 4 hours | 80053 -SPX Instant - 4 Jam80062- GrabExpress Instant - 4 Jam80064-GoSend Instant - 4 Jam |

**开发者应注意，卖家需要单独申请这些渠道的白名单。**


3.2.3.2 印尼即时渠道限制汇总


***Instant 2-hours (8008) 和 Instant 4-hours (8007) 必须始终同时开启或关闭。***


|**案例**|**当前状态**|**操作**|**错误提示**|
| --- | --- | --- | --- |
| 1 | 8000 Instant:**ON**80044 SPX Instant:**ON**80012 GoSend Instant:**OFF**80019 GrabExpress Instant:**OFF**8008 Instant 2-hours:**OFF**80054- SPX Instant - 2 Jam:**OFF**80061-GrabExpress Instant - 2 Jam:**OFF**80063-GoSend Instant - 2 Jam:**OFF**8007 Instant 4-hours:**OFF**80053-SPX Instant - 4 Jam:**OFF**80062-GrabExpress Instant - 4 Jam:**OFF**80064-Gosend Instant - 4 Jam:**OFF**| 关闭 80044 | SPX Instant cannot be turned off. Please enable at least 1 of the following channel(s): {GoSend Instant, GrabExpress Instant, SPX Instant - 2 Jam, GrabExpress Instant - 2 Jam,GoSend Instant - 2 Jam,SPX Instant - 4 Jam,GrabExpress Instant - 4 Jam,GoSend Instant - 4 Jam} |
| 2 | 8000 Instant:**OFF**80044 SPX Instant:**OFF**80012 GoSend Instant:**OFF**80019 GrabExpress Instant:**OFF**8008 Instant 2-hours:**ON**80054- SPX Instant - 2 Jam:**ON**80061-GrabExpress Instant - 2 Jam:**OFF**80063-GoSend Instant - 2 Jam:**OFF**  8007 Instant 4-hours:**ON**     80053- SPX Instant - 4 Jam:**ON**80062-GrabExpress Instant - 4 Jam:**OFF**80064-Gosend Instant - 4 Jam:**OFF**| 关闭 80054 | SPX Instant - 2 Jam channel cannot be turned off. Please enable at least 1 of the following channel(s). {SPX Instant, GoSend Instant, GrabExpress Instant, GrabExpress Instant - 2 Jam, GrabExpress Instant - 4 Jam, GoSend Instant - 2 Jam, GoSend Instant - 4 Jam} |
| 3 | 8000 Instant:**OFF**80044 SPX Instant:**OFF**80012 GoSend Instant:**OFF**80019 GrabExpress Instant:**OFF**8008 Instant 2-hours:**ON**80054-SPX Instant - 2 Jam :**ON**80061-GrabExpress Instant - 2 Jam:**OFF**80063-GoSend Instant - 2 Jam:**OFF**  8007 Instant 4-hours:**ON**     80053-SPX Instant - 4 Jam:**ON**80062-GrabExpress Instant - 4 Jam:**OFF**80064-Gosend Instant - 4 Jam:**OFF**| 关闭 80053 | SPX Instant - 4 Jam channel cannot be turned off. Please enable at least 1 of the following channel(s). {SPX Instant, GoSend Instant, GrabExpress Instant, GrabExpress Instant - 2 Jam, GrabExpress Instant - 4 Jam, GoSend Instant - 2 Jam, GoSend Instant - 4 Jam,SPX Instant - 2 Jam} |
| 4 | *卖家仅具有 8000 Instant 渠道的白名单*8000 Instant:**ON**80044 SPX Instant:**ON**80012 GoSend Instant:**OFF**80019 GrabExpress Instant:**OFF**| 关闭 80044 | SPX Instant channel cannot be turned off. Please enable the following channel(s).  GoSend Instant, GrabExpress Instant |

#### 3.2.4 泰国即时配送渠道依赖关系

3.2.4.1 渠道结构概述


|**掩码渠道**|**物流渠道**|
| --- | --- |
| 0 | 70124-Instant Delivery - สงทนท (แพก 30 นาท) |
| 0 | 70125-Instant Delivery - สงทนท (แพก 10 นาทจากสาขา) |
#### 3.2.5 越南即时配送渠道依赖关系

3.2.5.1 渠道结构概述


|**掩码渠道**|**物流渠道**|
| --- | --- |
| 5115 | 50040-SPX Instant - Hoa Toc - Uu Tien |
#### 3.2.6 菲律宾即时配送渠道依赖关系

3.2.6.1 渠道结构概述

|**掩码渠道**|**物流渠道**|
| --- | --- |
| 0 | 40079-Instant Delivery |
| 0 | 40080-Instant Delivery Priority |
#### 3.2.7 订单管理

要创建测试订单，请前往 Shopee 开放平台 Console 的 Test Order 页面，选择 *Create Test Order*。


![图片](https://open.shopee.com/opservice/api/v1/image/download/?image_id=K34RFeggDVp1VnSay1ytBxh8tZbcigs%2F4nRMZ2wTVqn%2BzBCtBjya4JYU4bfCXN4m11yj4BS%2FFDpb4n%2BDjrBbng%3D%3D&image_type=png)


选择店铺、商品和配送选项，然后点击 *Create* 生成订单。


![图片](https://open.shopee.com/opservice/api/v1/image/download/?image_id=rbuiBvf07YCjiFiuQQrgjyZrXU1UA6jUurSUQWL4CLDmPIFs9%2B7wqxOFWU6VfRTlnIoELegnSDWyrDJXhOynKw%3D%3D&image_type=png)


订单信息包括 Order SN、Item ID、Status、Update Time 和 Shop ID。您还可以在此页面进行取件、配送或删除订单。


![图片](https://open.shopee.com/opservice/api/v1/image/download/?image_id=6I260nsaQWNLCtX1thRKAUX1goP%2BuCiKGZCwoOvfk11vsagH3%2B3m8o7AaesM5ZIm8Lsekst4wgJ466%2BZT36R2w%3D%3D&image_type=png)


**更多后续步骤请参考****订单管理****文章。**

#### 3.2.8 退货退款管理


**更多信息请参考****退货退款管理****文章。**

#### 3.2.9 财务：获取收入和钱包交易

您可以通过使用 Mart shop_id 调用 API 来生成和获取收入报表、收入报告或钱包交易。使用 Mart shop_id 时，响应将返回包含该 Mart 下所有 outlet 店铺的汇总文档。


|**功能**|**开放 API**|**备注**|
| --- | --- | --- |
| 生成收入报告 | v2.payment.generate_income_report | 请求参数：release_time_from 和 release_time_to。 |
| 获取收入报告 | v2.payment.get_income_report | 通过传入 income_report_id 查询收入报告状态并提供文件链接。 |
| 生成收入报表 | v2.payment.generate_income_statement | 请求参数：statement_type=1 表示周报表；statement_type=2 表示月报表 |
| 获取收入报表 | v2.payment.get_income_statement | 通过传入 income_statement_id 查询收入报表状态并提供文件链接 |
| 获取钱包交易 | v2.payment.get_wallet_transaction_list | 获取钱包的交易记录。 |
#### 3.2.10 店铺设置

1.您可以通过调用 v2.shop.update_profile 更新店铺名称、Logo 和描述。2.您可以通过调用 v2.logistics.update_operating_hours 更新营业时间。*****注意：***

- *提供的值必须符合从****v2.logistics.get_operating_hour_restrictions****获取的限制条件。*
- *此 API 执行覆盖式更新。更新取件营业时间时，必须包含所有时间段，即使未发生变化也是如此。*

## 4. 推送机制

推送机制是来自 Shopee 的系统通知字典，涵盖产品、订单、退货、营销、稳定性和通用市场更新。


对于 Instant Mart，建议连接**order_status_push**。更多详情请参考 *order_status_push* 文章。


## 5. FAQ 与寻求帮助

常见问题请参考 FAQs。


如果您遇到与**Instant Mart APIs**相关的任何问题（例如接入、物流渠道配置、订单同步等），请[在此]向 Shopee 产品支持团队提交 ticket。


提交 ticket 时，请选择：**L1 Question Category -> Instant Mart**


选择正确的分类有助于我们更有效地识别您的请求并确定优先级。
