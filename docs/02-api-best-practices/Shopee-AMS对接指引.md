# Shopee AMS 对接指引

> 来源: [Shopee Open Platform](https://open.shopee.com/developer-guide/702)
> 分类: API Best Practices

### **1. Shopee AMS 介绍**


**Shopee Affiliate Marketing Solutions (联盟营销，简称 ****AMS) **是一个整合的营销与合作管理平台，助力品牌和卖家通过 Shopee 庞大的联盟网络扩展触达并提升销量。同时，卖家仅需为联盟伙伴带来的实际成交订单支付费用。



通过 AMS，卖家可以与各类联盟伙伴展开合作 —— 包括** Shopee Live** 和 **Shopee Video** 上的内容创作者、关键意见领袖 (KOL) 及社交媒体合作伙伴 —— 实现跨多渠道的商品推广，并获得可衡量的效果。


![图片](https://open.shopee.com/opservice/api/v1/image/download/?image_id=clz8hXw0W0hsPfH9t9of3oH19OGJ%2BB3PMj%2FbmsZuk5ujQ3PMv0jwvKP67rDD2%2Bkq3wylZyK2%2F6tGfNoZ9s7Nxw%3D%3D&image_type=png)


更多信息可参考：<u>Shopee Affiliate Marketing Solution (AMS) 2025</u>。



AMS 提供两种主要合作模式：



**● 公开活动 (Open Campaign)****：**卖家可将店铺商品开放给公众联盟推广，创作者可自由选择并推广商品。


**● 定向活动 (****Targeted Campaign)****：**卖家可邀请特定联盟伙伴进行定制合作，并设置专属佣金。 


AMS 还提供**全面的数据看板**，涵盖流量、转化及销售表现，帮助卖家监控效果、识别高绩效联盟伙伴，并优化投资回报率 (ROI)。



该 Open API 支持外部开发者自动化 AMS 操作 —— 包括活动创建、活动管理、效果追踪及账单审核 —— 提升卖家效率与系统整合灵活性。

### **2. **API 分类概述


AMS API 主要分为四大类：


1. **公开活动管理 (Open Campaign Management)** —— 管理店铺级公开活动及产品。
1. **定向活动管理 (Targeted Campaign Management)** —— 管理特定联盟的定向活动及产品。
1. **绩效仪表盘 (Performance Dashboard)** —— 获取绩效数据和报告。
1. **验证与转化报告 (Validation & Conversion Reports)** —— 查询 AMS 验证账单及订单详情。
### **3. **公开活动管理 API


**公开活动 (Open Campaign) **允许卖家灵活推广指定产品，吸引广泛联盟网络参与。以下 API 可用于管理公开活动的创建、产品加入、佣金设置和自动添加规则。

#### **3.1 获取公开活动下已添加 / 未添加的商品**

![图片](https://open.shopee.com/opservice/api/v1/image/download/?image_id=t1wSUPTTdBoQQMDrBKwly%2BZ%2B6X8CASJ0QQp2SEtlNB5SPFr8wUiDop%2FxB6rFSmJKco4sFW1URioqYq43KW7C5Q%3D%3D&image_type=png)


● v2.ams.get_open_campaign_added_product: 获取当前已加入公开活动、随时可供联盟伙伴选择推广的所有商品。


● v2.ams.get_open_campaign_not_added_product: 获取符合条件但尚未加入公开活动的商品。

#### **3.2 向公开活动添加商品**


在设置有效的佣金比例和推广周期后，商品可立即加入**公开活动**，供联盟伙伴推广。通过提供的 API，可以选择按**商品 ID **添加特定商品，也可以一次性将**店铺内所有商品**加入公开活动。



此外，可以启用 **“自动添加”** 功能，系统会在店铺新商品上架后自动将其加入公开活动。


![图片](https://open.shopee.com/opservice/api/v1/image/download/?image_id=3JEN%2B2IDlPFNojRaNzsy3Z2kfBJq%2B39AeLJxxjzDLrSVKu%2FLSh0TqBAm1%2Bq%2Fq7GL6DyAHO7i%2BzA3W5sXi%2F68Fg%3D%3D&image_type=png)



● v2.ams.batch_add_products_to_open_campaign: 按商品 ID 批量加入公开活动。


● v2.ams.add_all_products_to_open_campaign: 将店铺所有符合条件产品加入公开活动。


● v2.ams.get_auto_add_new_product_toggle_status: 查询 “自动添加” 功能是否启用，以及其当前的默认佣金比例。


● v2.ams.update_auto_add_new_product_setting: 更新 “自动添加” 功能的开关状态及其默认佣金比例。


● v2.ams.get_open_campaign_batch_task_result: 获取公开活动的批量操作任务结果。

#### **3.3 编辑公开活动中的商品设置**


**编辑佣金比例：**可调整处于推广中的商品的佣金比例。但请注意，若有联盟伙伴正在推广该商品，原佣金比例仍将持续生效 7 天；同时，调整的佣金比例会立即生效。


![图片](https://open.shopee.com/opservice/api/v1/image/download/?image_id=rk0sIqmSzyunK4f%2Ftr%2BIEx8N768V52jWIK7ciVwrLuHiTS3kRfo8bMo%2FpIKJ0evs41Gt%2FF8nke9ZFTjaEBRSfQ%3D%3D&image_type=png)



**编辑推广周期：**为实现最大曝光量并维持订单增长，建议设置较长的推广周期，以便联盟伙伴能够持续推广你的商品。



请注意，活动一旦生效，推广周期便不能缩短，以此保障所有联盟伙伴获得公平、一致的合作体验。


![图片](https://open.shopee.com/opservice/api/v1/image/download/?image_id=zX1wgHHRCImvQGp8cxbc36h8YYIqhznZUR%2BpVCmztzL1FdYie8pTCAZX3GvEv%2F1OK7aj6OdYlBw5dOwng%2Fc9XQ%3D%3D&image_type=png)


● v2.ams.batch_edit_products_open_campaign_setting: 批量更新多个商品的活动设置。


● v2.ams.edit_all_products_open_campaign_setting: 更新活动中所有商品的设置。


● v2.ams.get_open_campaign_batch_task_result: 获取公开活动的批量操作任务结果。

#### **3.4 从公开活动中移除商品**


你可以通过提供的 API 从公开活动中移除商品 —— 既可指定商品 ID 移除特定商品，也可一次性清除所有商品。



请注意，从公开活动中移除的商品，**仍将在之后 7 天内保持可获得佣金的资格**，以确保对正在进行的联盟推广活动进行公平的归因统计。


![图片](https://open.shopee.com/opservice/api/v1/image/download/?image_id=WsGq7qvC7k%2F5qanjXHwooCcJgYkLgkX37UtuweS6vB9LYcIiE0Z9vp4AShOfPvntB3kZhN8WPpg06aFqoWwo0A%3D%3D&image_type=png)


● v2.ams.batch_remove_products_open_campaign_setting: 批量移除多个商品。


● v2.ams.remove_all_products_open_campaign_setting: 清除公开活动中的所有商品。


● v2.ams.get_open_campaign_batch_task_result: 获取公开活动的批量操作任务结果。

#### **3.5 获取公开活动的商品优化建议**


![图片](https://open.shopee.com/opservice/api/v1/image/download/?image_id=7YMxYyjCiJ%2Bv0CeUON0P6Z5THaLPjbd1bFMLsDu5n28mcFgch8TJHuf1xZ%2BuNi3SNIpLN0krgg4ZxVBRiIFORg%3D%3D&image_type=png)


● v2.ams.get_optimization_suggestion_product: 该 API 提供 3 类商品优化建议，帮助卖家提升活动效果及联盟伙伴参与度：


○ **添加高潜力商品** —— 推荐畅销、热门或订单潜力高的商品，这些商品所属品类在 AMS 中的供给量相对市场需求较低。


○ **优化佣金比例** —— 针对品类内竞争力评分低于 60 百分位的商品，建议调整佣金比例，以吸引更多联盟伙伴。


○ **延长推广周期** —— 针对剩余推广时间不足 30 天的活动中的商品，建议延长活动周期，使联盟伙伴能够持续推动转化。

#### **3.6 获取商品获取商品的建议佣金比例**


● v2.ams.batch_get_products_suggested_rate: 遵循每个商品的建议佣金比例，将显著提升你的商品竞争力，并提高商品在联盟伙伴中的曝光度。


● v2.ams.get_shop_suggested_rate: 为店铺所有商品设置公开活动时，可参考此 API 获取统一的建议佣金比例，适用于全店商品。

### **4. **定向活动管理 API


**定向活动 (Targeted Campaign) **允许卖家与特定联盟伙伴开展定制化、以效果为导向的推广合作。API 支持开发者创建、编辑和监控定向活动，包括商品选择、联盟伙伴选择及活动设置。

#### **4.1 创建新的定向活动**


**获取商品列表：**


● v2.ams.get_targeted_campaign_addable_product_list: 获取可添加至定向活动的店铺商品。


![图片](https://open.shopee.com/opservice/api/v1/image/download/?image_id=0wts05PewNr1GOvhI2ZSH1IotwJCJrO7k7uoJF%2BfyIsWGIO4Z2Hz5PukNYx%2F8P2olyBXHXaUWdn1O3VfjoKu3w%3D%3D&image_type=png)



**获取联盟伙伴列表：**


● v2.ams.get_recommended_affiliate_list: 获取定向活动的优质推荐联盟伙伴列表。


● v2.ams.get_managed_affiliate_list: 获取店铺已收藏的管理联盟伙伴列表 (该功能在卖家中心的 AMS 系统中可用)。


![图片](https://open.shopee.com/opservice/api/v1/image/download/?image_id=1VHNPPPD8doYwzAKBEraahok5%2FPCkjXBAN5Dx4Nq1V1kt4ephCejksSf4FDv99y%2BlKJDnvgGLTesE%2BMR0qJFHQ%3D%3D&image_type=png)



**创建新的定向活动：**


● v2.ams.create_new_targeted_campaign: 创建新的定向活动时，需选择商品和联盟伙伴，并按商品维度设置佣金比例。你也可以沿用之前的商品推荐，并参照建议的佣金比例来完成设置。

#### **4.2 查看与编辑定向活动**


● v2.ams.get_targeted_campaign_list: 获取卖家创建的所有定向活动。


● v2.ams.get_targeted_campaign_settings: 获取当前定向活动的详情，包括关联商品及对应佣金比例、联盟伙伴等信息。


● v2.ams.update_basic_info_of_targeted_campaign:  更新活动基本信息，如活动名称、推广周期、活动说明及预算。


● v2.ams.edit_product_list_of_targeted_campaign: 修改现有定向活动中的商品列表。


● v2.ams.edit_affiliate_list_of_targeted_campaign: 修改现有定向活动中的联盟伙伴列表。


● v2.ams.terminate_targeted_campaign: 终止处于活跃状态的定向活动。

### **5. **效果与分析 API


AMS 提供一系列分析仪表盘，帮助卖家轻松查看、分析和理解其联盟营销表现，助力基于数据进行优化并持续改进。

#### **5.1 核心绩效**


● v2.ams.get_performance_data_update_time: 所有数据每日更新，反映截至前一天产生的订单。你可以通过此 API 获取 AMS 效果数据的最新更新时间，确保你的系统展示的是最新的效果洞察。


● v2.ams.get_shop_performance: 查询店铺在 AMS 中的表现相关的几个核心指标。


![图片](https://open.shopee.com/opservice/api/v1/image/download/?image_id=8Ch2o3C%2BpA83z0a6UlU3FhvNMP44ehFq9UGLEDwrY5jaGE7lO5aRQH76xyFf65715HfCuAZ4IizdmmCvDUTFjg%3D%3D&image_type=png)

#### **5.2 商品分析**


● v2.ams.get_product_performance: 获取店铺内特定商品的效果数据。


![图片](https://open.shopee.com/opservice/api/v1/image/download/?image_id=lNUXAT10bb%2Bx0j5s6rzbe7DJgDETcsmnElAjnmE1kZxNQXszeC2QMyxg5a6nbIcICY%2BpIM7zECLVbV24bb5Lfw%3D%3D&image_type=png)

#### **5.3 联盟伙伴分析**


● v2.ams.get_affiliate_performance：获取特定联盟伙伴为店铺带来的效果数据。


![图片](https://open.shopee.com/opservice/api/v1/image/download/?image_id=Mtz%2BC4ptyH9wW%2BJ2Qf%2FZ4m2HSW6aBoeJpiy35Br7Qc%2BwdoS4zjlVq8rBNrgCba%2FLrvHIzZOPWD8Xk%2BhX%2BgkMwA%3D%3D&image_type=png)

#### **5.4 内容分析**


● v2.ams.get_content_performance: 获取店铺的 Shopee Live 和 Shopee Video 的内容表现数据。


![图片](https://open.shopee.com/opservice/api/v1/image/download/?image_id=trqgm4BY31ryv2R0gFysXwDjqO5fjSz4uz6XNtTYVwY6pSrAbsd4nqLWmTNBeOYYhwlYCSU%2FIWIrjoXsT9%2FSTQ%3D%3D&image_type=png)

#### **5.5 活动分析**


● v2.ams.get_campaign_key_metrics_performance: 获取公开活动和定向活动的核心指标。


● v2.ams.get_open_campaign_performance: 获取公开活动中所有商品的效果数据。


● v2.ams.get_targeted_campaign_performance: 获取定向活动列表及效果数据。


![图片](https://open.shopee.com/opservice/api/v1/image/download/?image_id=dNUTGgwD1c0XYeUH2%2FdK4xDOY9lpxLEW%2FJEJQqTA5tuiKRyaJpXY5nGgNXs6zdFaJpK1Lud6Hxdl1G7%2FbnGLXQ%3D%3D&image_type=png)

### **6. **转化与验证报告类 API


用于获取和核对 AMS 账单及转化报告，帮助卖家了解订单级别的表现，并审核通过 AMS 产生的每笔交易的详细佣金及费用扣除情况。

#### **6.1 转化报告**


● v2.ams.get_conversion_report: 获取包含订单级详情的转化报告。


![图片](https://open.shopee.com/opservice/api/v1/image/download/?image_id=4UmqOargBfMY%2BwSW4Rr4yNlhwQCqMEL4uyvtGlAsArsglm0E2V36ofkMdkJ%2FTRbPfzS3%2B7XycPSmc9Pa2bqNgw%3D%3D&image_type=png)

#### **6.2 验证账单**


● v2.ams.get_validation_list: 获取卖家的 AMS 验证账单列表。


● v2.ams.get_validation_report: 获取特定验证账单的详细信息。


![图片](https://open.shopee.com/opservice/api/v1/image/download/?image_id=hFmA9ltyM1Fdp2zC9JpAcie6C%2FIaYMhOKDQR%2BI%2FphiihtrAHFjUEgDArwpaJmCBqo%2FQAKzKAJR0QLol3lY6vfw%3D%3D&image_type=png)

### **7. **开发者集成说明


● 仅 **“****Affiliate Marketing Solution Management****” **类型的应用有权访问 AMS Open API。请在控制台中创建相应类型的应用后再进行对接。


● 所有 AMS API 均需要有效的店铺授权与鉴权。详情请参考：<u>Authorization and Authentication</u>.


● 对于支持分页的接口，请使用分页功能处理大量数据。


● 效果数据和转化报告存在数据范围及记录数量限制。


● 对于异步任务 (如批量更新)，请使用批量任务结果 API 查询状态。

### **8. **后续步骤


● 参考 Shopee 开放平台文档，了解身份验证、授权及错误处理的详细信息。


● 如需熟悉 AMS 功能并确保测试准确，请访问卖家中心的 AMS 模块。请注意，**在执行任何与 AMS 相关的 API 操作前，卖家必须在 Seller Center 签署 ****AMS Terms & Conditions****。**


● 使用 AMS Open API 实现活动管理自动化、效果分析，并将 AMS 数据与你的外部系统或工具集成，以简化运营流程。

