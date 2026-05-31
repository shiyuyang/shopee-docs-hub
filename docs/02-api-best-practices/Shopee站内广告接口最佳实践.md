# Shopee 站内广告接口最佳实践

> 来源: [Shopee Open Platform](https://open.shopee.com/developer-guide/277)
> 分类: API Best Practices

## 什么是 Shopee 广告

Shopee 广告允许您使用 Shopee 平台站内广告，以增加您的产品和商店的曝光度。


了解 Shopee 广告：`https://ads.shopee.sg/learn/faq/96/195`

## 广告 API 使用规则

在使用广告 API 接口时，您需要遵守我们列出的以下规则以便 shopee 可以为所有卖家营造一个公平安全的市场：

1. 在处理广告数据时，需要遵守平台的数据保护政策。
1. 广告接口仅限于 Shopee 官方合作的 ISV，与平台卖家使用，可用于店铺广告运营与官方合作代运营项目，不能出于其他目的使用广告 API 接口。
1. 不得将店铺数据用于除店铺运营，及 Shopee 官方合作项目以外的任何途径。
1. ISV 接口调取卖家店铺数据，需通过授权流程征得平台卖家同意。
## Ads 接口介绍

广告 API 接口能力：

### **1.获取广告余额和店铺设置信息**
- `v2.ads.get_total_balance`: 使用此 API 返回卖家广告积分的实时总余额，包括付费积分和免费积分，卖家可以通过该接口关注余额状态，保证余额可以支持服务正常运行。
- `v2.ads.get_shop_toggle_info`: 使用此 API 获取店铺的广告配置信息：店铺是否开通广告自动充值，店铺是否开通广告价格优化


Top_Up Toggle：开启/关闭自动充值


![图片](https://open.shopee.com/opservice/api/v1/image/download/?image_id=xQhGaK85nC9epS6O8i08i5BaxDi7Ub6XOBQwJbkpJsK%2BFDMBA0S3i5sLFkWyp0hV9pc2nPMe2kVHtbmj%2BJpdWg%3D%3D&image_type=png)


Campaign_Surge:开启/关闭广告价格优化


![图片](https://open.shopee.com/opservice/api/v1/image/download/?image_id=%2BpvbPFCXjB8D3ZBw9xyxXObzdZDAkCrvPlM8JV9HnhWlymVz8vHfpGiORDd7iQvblZ5x9anRd9TE0bFmj62nyw%3D%3D&image_type=png)

### **2.获取商品广告实时表现概况数据（店铺维度）**
- `v2.ads.get_all_cpc_ads_hourly_performance`: 使用此 API 获取商店级 CPC 广告单日期内的效果（时间维度单位为小时）卖家可以获取到单日 Conversions，Conversion Rate, item sold, GMV, Ad GMV/Ad Expenditure 等信息。
- v2.ads.get_all_cpc_ads_daily_performance: 使用此 API 可以获得商店级 CPC 广告多天的效果（时间维度单位为天）。卖家可以获取到多日日 Conversions，Conversion Rate, item sold, GMV, Ad GMV/Ad Expenditure 等信息。

![图片](https://open.shopee.com/opservice/api/v1/image/download/?image_id=nbmTdBH0PkDRx7%2FQ%2FcZOo%2Bvb7DSa2QKGSY1hiaVwl1QkMZQAE%2FFsuL2o%2BObLzmV8F1hWxK8ZQfsRmwJM%2B23%2Fjg%3D%3D&image_type=png)

### **3. 获取推荐关键词和商品数据**
- `v2.ads.get_recommended_keyword_list`: 使用此 API 获取按项目推荐的关键字列表以及可选的搜索关键字，在获取关键词的同时，卖家可以查看该推荐词的质量分数，搜索量以及建议出价等信息。

![图片](https://open.shopee.com/opservice/api/v1/image/download/?image_id=7bItG5LFn7NxsQHPX3EOc6kM%2BRYECvMlQxHsJOXrji9cksvnOvfM7bIASZtKzWlPV4tjfnpObG%2F0XkrLeAYEHA%3D%3D&image_type=png)

- `v2.ads.get_recommended_item_list` 使用此 API 获取带有相应标签的推荐 SKU（商店级别）列表，即热门搜索/最畅销/最佳 ROI 标签。

![图片](https://open.shopee.com/opservice/api/v1/image/download/?image_id=O1GwkT8RofANcGljLqUrxycppzkT1mOtzPJVsdlc4o67UDa0kR5iThyJhtURm9%2Fg8m7IFeXcg0SR6MO%2F3Ne3ZQ%3D%3D&image_type=png)

### **4.获取广告计划维度数据**
- v2.ads.get_product_level_campaign_id_list：使用此 API 获取某个商品所属的广告计划列表。
- v2.ads.get_product_level_campaign_setting_info：使用此 API 获取广告计划的详细设置信息。
- v2.ads.get_product_campaign_daily_performance 和 v2.ads.get_product_campaign_hourly_performance：使用这两个 API 获取商品广告计划的每日 / 每小时效果数据。

![图片](https://open.shopee.com/opservice/api/v1/image/download/?image_id=BKGf1hQmN2QQ870jtQJ21kap7Hr9XSqJxnl7qh9Hl6QgNVQejSWt6EJlt9ae4mjXfzfx4Vzh%2BeMa7j3USi5%2FSw%3D%3D&image_type=png)

### **5. GMV Max 广告概览**

GMV Max 广告是 Shopee 提供的一种全站流量广告解决方案，通过自动出价与智能流量分配，帮助卖家最大化 GMV 表现。


目前 Shopee 支持两种 GMV Max 广告类型：

1. Item GMV Max 广告（商品维度）
1. Shop GMV Max 广告（全店推 / 自动选择商品）


两种广告类型均基于系统自动化投放逻辑，并围绕 ROAS（广告投入产出比）目标进行优化。

|**维度**|**Item GMV Max**|**Shop GMV Max**|
| --- | --- | --- |
| 广告层级 | 商品 | 店铺 |
| 商品选择 | 开发者指定 | 系统自动选择 |
| 创建接口 | create_manual_product_ads | create_gms_product_campaign |
| ROAS 控制 | 支持 | 支持 / 自动 |
| 广告数量限制 | 多条 | 每店仅 1 条 |
| 商品互斥规则 | 同一商品不能同时参与 Item GMV Max 广告与 Shop GMV Max 广告 |


### **6. Item GMV Max 广告（商品全站推广）**

Item GMV Max 广告是一种**商品维度**的全站推广广告，用于推广指定商品，并在 Shopee 全站流量中进行智能投放。


**主要特性：**

- 广告创建在商品（Item）层级
- 使用自动出价模式（Auto Bidding）
- 围绕 ROAS 目标进行投放优化
- 适合希望放大单个商品 GMV 的卖家


**通过 Open API 创建 Item GMV Max 广告，请使用：**

- v2.ads.create_manual_product_ads
- 关键参数说明：
 - bidding_method = auto → 创建 Item GMV Max 广告

![图片](https://open.shopee.com/opservice/api/v1/image/download/?image_id=D5v%2FGCC0GGvDXSQ2%2BtrCF48ohYn6vcHUzBeYzDDdgK%2BAMh0a4tlclsBLcNiuhlpBmKlQZWzxorwGKCGBWfPzmQ%3D%3D&image_type=png)


**在创建 Item GMV Max 广告前，开发者可调用以下接口获取推荐 ROAS：**

- v2.ads.get_product_recommended_roi_target

![图片](https://open.shopee.com/opservice/api/v1/image/download/?image_id=IyLShRfcLi6d%2FUsOjDayAZRA3tUaT1aPmHVNDQmu4KMfdkAbgGJDMop1PuiQOAYehnnJFGxKOjSf5aQ19%2Bvahw%3D%3D&image_type=png)


在创建 Item GMV Max 广告前，开发者可通过预算建议接口，获取系统推荐的广告预算范围，用于辅助广告创建与参数配置：

- v2.ads.get_create_product_ad_budget_suggestion

![图片](https://open.shopee.com/opservice/api/v1/image/download/?image_id=toqvLy8rp%2FY4kZv9yBwVHphTeHZOtKFuukDqjIwHwIvL%2FN2aXRWqAsfxLNGO4uo13rD7XRmdR%2BtVV2VjgURAWA%3D%3D&image_type=png)


**典型使用流程：**

1. 调用 v2.ads.get_product_recommended_roi_target 获取推荐 ROAS
1. 调用 v2.ads.get_create_product_ad_budget_suggestion 获取预算建议
1. 调用 v2.ads.create_manual_product_ads (bidding_method = auto)，创建 Item GMV Max 广告


说明：


预算建议与 ROAS 推荐均为系统参考值，最终广告表现仍以实际投放与系统学习结果为准。


### **7. Shop GMV Max 广告**

Shop GMV Max 广告是一种**店铺维度**的全站推广广告，系统将基于卖家设置的预算与 ROAS 目标，自动选择店铺内商品并进行智能投放，以最大化店铺整体 GMV 表现。


**主要特性：**

- 广告创建在店铺（Shop）层级
- 系统自动选择商品并动态分配预算
- 使用 GMV Max 自动化投放逻辑（支持 ROAS 目标或自动竞价）
- 适合希望降低商品管理成本、放大整体店铺 GMV 的卖家


**Shop GMV Max 投放模式说明**


Shop GMV Max 广告支持以下两种投放模式，开发者可在创建或编辑广告活动时进行配置：

1. Auto Bidding（自动竞价）
 - Auto Bidding 模式下，系统将在可接受的 ROAS 范围内，自动探索更多流量机会，以提升整体曝光与 GMV 表现。
1. Custom ROAS（自定义 ROAS）
 - Custom ROAS 模式下，系统将围绕开发者设置的 ROAS 目标，对广告投放进行优化，在 GMV 表现与投入产出之间保持平衡。


**通过 Open API 创建 Shop GMV Max 广告，请使用：**

- v2.ads.create_gms_product_campaign
 - FAQ：如何判断商品是否已经在 GMV Max 中？
 - 关键字段说明：roas_target
 - 该参数用于控制 Shop GMV Max 广告的投放模式，规则如下：
 - 不传 roas_target  → GMV Max Auto Bidding（Shop）
 - roas_target = 0  → GMV Max Auto Bidding（Shop）
 - roas_target > 0  → GMV Max Custom ROAS（Shop）

![图片](https://open.shopee.com/opservice/api/v1/image/download/?image_id=ZvAXZWvRXn37rXGLjONjk2hTEQXbRNWHHgU2FrD2iqTvIjQlbSjsl%2FnfqezvlsA%2FASMlCdfo2tpjzT1nFpBSWQ%3D%3D&image_type=png)


**在创建 Shop GMV Max 广告前，开发者可调用以下接口进行资格校验：**

- v2.ads.check_create_gms_product_campaign_eligibility
- 用于校验当前店铺是否具备创建 Shop GMV Max 广告的资格（白名单校验）


**Shop GMV Max 广告相关管理与数据接口：**

- 广告配置与管理
 - v2.ads.edit_gms_product_campaign  修改广告活动配置
- 商品管理
 - v2.ads.edit_gms_item_product_campaign  调整广告活动下的商品配置
 - v2.ads.list_gms_user_deleted_item  查询卖家已删除的商品信息
- 效果数据
 - v2.ads.get_gms_campaign_performance  获取广告活动整体表现数据
 - v2.ads.get_gms_item_performance  获取广告活动中商品维度的表现数据


**典型使用流程：**

1. 调用 v2.ads.check_create_gms_product_campaign_eligibility 校验店铺是否具备创建资格
1. 调用 v2.ads.create_gms_product_campaign 创建 Shop GMV Max 广告
1. （可选）调用 v2.ads.edit_gms_product_campaign 调整广告活动配置
1. v2.ads.get_gms_campaign_performance / v2.ads.get_gms_item_performance 调用效果数据接口，持续监控广告表现


**说明：**

- Shop GMV Max 广告默认由系统自动选择商品并进行预算分配，商品列表会按日进行自动更新。如卖家对商品列表进行了手动调整，则以卖家当前配置的商品列表为准。
- 广告表现将随系统学习阶段逐步优化，建议在学习期内避免频繁修改广告配置。
### **8. 手动商品广告**

手动商品广告是一种商品维度的广告形式，开发者需明确指定投放商品、关键词及出价策略。**现阶段，手动广告功能仅对少量白名单商家开放使用。**


**主要特性：**

- 广告创建在商品（Item）层级
- 使用手动出价模式（Manual Bidding）
- 支持关键词与商品定向配置
- 适合需要精细化控制投放策略的卖家


通过 Open API 创建手动商品广告，请使用：

- v2.ads.create_manual_product_ads
- 关键参数说明：
 - bidding_method = manual → 手动商品广告

![图片](https://open.shopee.com/opservice/api/v1/image/download/?image_id=yXKgzAmNPfQviCDFwJNNq6Wie0ETj6D36CmjJ72wv%2FGtZUFQ9IomgJ3oTNlLy9WHaMwPETeQWKW9Ky5BrsRawQ%3D%3D&image_type=png)


创建 bidding method=manual 的手动广告时，可以调用`v2.ads.get_recommended_item_list` 和 `v2.ads.get_recommended_keyword_list` 获取推进的广告商品和关键词，再输入预算、投放位置等信息进行投放


### **9. (即将下线)创建自动商品广告**

v2.ads.create_auto_product_ads(whitelist shop)


![图片](https://open.shopee.com/opservice/api/v1/image/download/?image_id=Pvd8T9sjTx6g9YKCcWNqP%2B7pNTUTloVpBX%2Ba6Oz3WGuENuQTMNgQLkcZnN%2Fh0XhQTXuNZB5GwnaU0mtnVctHBw%3D%3D&image_type=png)


若您串接时遇到问题，建议可先查看开发者指引以及查找常见问题 。


若仍无法解决 Open API 问题，请登录 Open Platform Console 进行工单提报。


