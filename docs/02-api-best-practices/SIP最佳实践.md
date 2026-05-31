# SIP 最佳实践

> 来源: [Shopee Open Platform](https://open.shopee.com/developer-guide/261)
> 分类: API Best Practices

## 什么是 SIP?

SIP 全称为 Shopee International Platform（Shopee 国际平台）。卖家参加 SIP 项目后，Shopee 会帮您运营店铺，包括根据当地市场特点设置并提报行销活动等。 卖家开店后，您只需提前绑定收款账户、定期检查产品库存、参与各类活动报价确认、并按照发货时效发货即可！

## 名词解释：

**P shop (primary shop)**: 代运营模式中，卖家自主经营的主店铺，又称主店铺。


**A shop (affiliated shop)**:  Shopee 帮助卖卖家运营的代运营店铺，又称附属店铺。


**CB SIP (cross border SIP)**：如果 P shop 是跨境卖家运营，又称 CB SIP 模式。


**Local SIP**：如果 P shop 是本土卖家运营，又称 local SIP 模式。


**SIP rate**: 只适用于 CBSIP。SIP 调价比例，是指卖家根据商品成本价，对附属店铺设置的折扣率。当商品在附属店铺售出后，Shopee 将根据商品成本价格和 SIP 调价比例，自动计算出给卖家最后的结算价格。


**SIP Item price**: 商品成本价格，Shopee 将根据此价格计算 A shop 商品的售价以及商品结算价。


**Settlement price**: 卖家结算价格，Shopee 将根据此价格结算给卖家。

## 1.SIP 店铺授权
### 1.1 非 CNSC 卖家
#### 1.1.1 授权流程


授权流程同文章授权与鉴权 当卖家登陆 SIP P Shop 的账号进入授权页面点击确认授权后，SIP P Shop 将授权给此 APP。


![图片](https://open.shopee.com/opservice/api/v1/image/download/?image_id=wICW%2F2f1YfQskbVUFBJy5gR%2B5iF%2FjUfg2rFw2SvGKPuwFfZ3v0oQ7ZqVofDpl3UbnRlwvoqv%2FOwOaJRMX9RkgQ%3D%3D&image_type=png)

#### 1.1.2 获取 code

授权成功后，您可以直接通过回调地址拿到 P Shop 的 shop_id 以及可用的 code。


#### 1.1.3 获取 P shop 的 token


您可以调用`v2.public.get_access_token`接口，传入授权成功后的 P shop 的 shop id 和 code，接口将返回当前授权成功的 P shop 可用的 access token 和 refresh token。


#### 1.1.5 刷新 access_token

此时第三步获取的 access token 和 refresh token 可用于所有的 P shop。后续请调用 v2.public.refresh_access_token 接口分别刷新 P shop 的 access_token。


注意⚠️:


1. 新的 access_token 生成后，旧 access_token 依然在5 分钟内有效。


2. 重新授权会触发刷新 refresh_token 和 access_token。


3. 调用 Refreshaccesstoken 接口要在授权有效期内。


4. 如果丢失了返回的新的 refresh_token 和 access_token，请查看此 FAQ


### 1.2 CNSC 卖家
#### 1.2.1 授权流程


授权流程同授权与鉴权 当卖家登陆 Main account 进入授权页面后，每个 merchant 下的店铺列表中将会对 SIP P Shop 显示“SIP”的标签，点击右侧的“view”将能看到此 P Shop 下所有的 A Shop 信息与授权状态。勾选 SIP P Shop 并点击确认授权给此 APP，则它此时绑定的所有 SIP A Shop 都将自动授权给此 APP。


![图片](https://open.shopee.com/opservice/api/v1/image/download/?image_id=fON4MRg2jyP7Ska%2B5zTDPdB7n6PN7pkAWV637GaLOIVyn4cdB2EM4ZMiM6jqB%2FE7x0T%2BVB%2BsrXZrh7tUKmiO9Q%3D%3D&image_type=png)


注意⚠️


一个 main account 所有未绑定 merchant 的 shop，都会在 Unupgraded Shop Group 列表下，Unupgraded Shop Group 列表的 shop 如果有 SIP 标识，则同样代表它们是 SIP P Shop。


![图片](https://open.shopee.com/opservice/api/v1/image/download/?image_id=HCsGhQQJHApkIrEvBvtRWwnpplJQon2O6cjzNiTWaYLEMpJ4CMKIB9x5Ns1IVoBI8MOag5y8aifm01CPb4Lb3g%3D%3D&image_type=png)

#### 1.2.2 获取 code

授权成功后，您可以直接通过回调地址拿到 main_account_id 以及可用的 code。


#### 1.2.3 获取 token


您可以调用`v2.public.get_access_token`接口，传入授权成功后的到 main_account_id 和 code。merchant_id_list 将返回当前授权成功的 merchant，shop_id_list 将返回当前授权成功的所有 shop, 包括 SIP P shop、A shop 以及非 SIP 的 shop id。access_token 可以被当前授权成功的所有 merchant id 和 shop id 所共用。refresh_token 同理。


#### 1.2.4 获取店铺关系

随后，调用`v2.merchant.get_shop_list_by_merchant`接口，可以获取某个 merchant 关联的已授权店铺列表，调用`v2.shop.get_shop_info`接口，可以通过返回参数获取店铺是否属于 SIP 店铺，以及 SIP 主店铺和附属店铺的关系。


- 如果是普通店铺，is_sip=false 且 sip_affi_shops 字段不返回；
- 如果是 SIP P shop，is_sip=true 且 sip_affi_shops 字段返回且返回 A shop id list；
- 如果是 SIP A shop， is_sip=true 且 sip_affi_shops 字段不返回。


请注意每个 shop id 和 merchant id 的 access_token 和 refresh_token 都需要分开保存。您调用`v2.public.refresh_access_token`接口时，请分别刷新每个 shop id 和每个 merchant id 的 access token 和 refresh token。（即刷新后每个 shop id 的 access token 和 refresh token 不能共用，merchant id 同理）。


## 2. SIP 商品管理
### 2.1 商品同步逻辑

| 信息 | 同步逻辑 |
| --- | --- |
| 商品基础信息 | 刊登：卖家发布 P shop 商品后，Shopee 会将商品信息自动翻译成 A shop 当地语言并创建一个 A shop 商品。更新：卖家修改了 P shop 商品，Shopee 会将新商品信息自动同步到 A shop 商品。 |
| 商品状态 | P shop 商品被下架或者删除，A shop 商品也会被下架和删除，卖家不能单独操作 A shop 商品的状态。 |
| 商品库存 | P shop 商品库存等于 A shop 商品库存，例如 P shop 下有2个 A shop, 分别是 A shop1, A shop2, 且 P shop 库存=10，则 A shop1库存=A shop2库存=10。当 A shop1售出1个商品，则库存 P shop=A shop1=A shop2=9。 |
| 商品价格 | 卖家更新 P shop 商品价格，Shopee 会将同步到 A shop 商品价格。 |
### 2.2 商品价格逻辑
#### SIP Item Price

`v2.product.get_item_base_info`和`v2.product.get_model_list`接口价格字段返回说明


 "price_info": [


                    {


                        "currency": "MYR",


                        "original_price": 179.58,


                        "current_price": 179.58                   


                      **"sip_item_price_currency": "CNY",**


                      **"sip_item_price": 230.87,**


                      **"sip_item_price_source": "auto"**


                    }


注意⚠️

- 如果商品是主店铺商品且不包含变体，则您需要调用`v2.product.get_item_base_info` 接口即可拿到商品的 sip_item_price/sip_item_price_source/sip_item_price_currency。
- 如果商品是主店铺商品且包含变体，则您需要调用`v2.product.get_model_list` 接口即可拿到变体的 sip_item_price/sip_item_price_source/sip_item_price_currency。
- 如果商品是非主店铺商品，`v2.product.get_item_base_info`和`v2.product.get_model_list`接口将不返回 sip_item_price/sip_item_price_source/sip_item_price_currency 字段。

## 3. SIP 订单管理
### 3.1订单同步逻辑
#### 3.1.1 CB SIP

请您分别获取 SIP P shop order list 以及 SIP A shop order list 进行履约。其中：

- SIP A shop 中的订单，将不对 P shop seller 暴露买家支付金额。
- SIP A shop 中的订单，在 get_order_detail 接口中返回的 currency 为 CNY 或 USD。
#### 3.1.2 Local SIP


Shopee 自动将 SIP A shop order 同步至 SIP P shop，您仅需要获取 SIP P shop order list 并履约。其中：SIP A shop 的订单对于 P shop seller 无感知，A shop 生成对应的 P shop 订单，收货人则为位于 Local 境内的 Shopee 转运仓；Shopee 转运仓会进行跨境发货，最终发给 Buyer。


注意⚠️


Order Push 会同时推送 P shop 和 A shop 的订单，对于 CB SIP 的卖家需要关注 P shop 和 A shop 的推送，Local SIP 的卖家只需要关注 P shop 的推送即可。


更多订单履约流程请参考：`https://open.shopee.com/developer-guide/229`


## 4. SIP 订单收入

1. CB SIP A shop 中的订单，在 get_escrow_detail 接口中同时返回 A shop currency amount 以及对应的 P shop currency.
1. Local SIP A shop 中的订单收入相关数据，也默认转换成 P currency，与 P shop 订单无差异。


请留意`v2.payment.get_escrow_detail`接口下列字段


“✓” 表示接口会返回此字段。


“×” 表示接口不会返回此字段。


| 字段 | SIP P shop order | SIP A shop order |
| --- | --- | --- |
| escrow_amount | escrow_amount=buyer_total_amount+shopee_discount+voucher_from_shopee+coins+payment_promotion-buyer_transaction_fee-cross_border_tax-commission_fee-service_fee-seller_transaction_fee-seller_coin_cash_back-escrow_tax-final_product_vat_tax-final_shipping_vat_tax-drc_adjustable_refund-reverse_shipping_fee+rsf_seller_protection_fee_claim_amount-rsf_seller_protection_fee_premium_amount+final_shipping_fee(could be postitive/negtive). | escrow_amount=sum of all Asku's settlement price - service_fee - commission_fee -seller_return_refund - drc_adjustable_refund. |
| buyer_total_amount | ✓ | × |
| actual_shipping_fee | ✓ | × |
| buyer_paid_shipping_fee | ✓ | × |
| buyer_transaction_fee | ✓ | × |
| estimated_shipping_fee | ✓ | × |
| campaign_fee | ✓ | × |
| coins | ✓ | × |
| cross_border_tax | ✓ | × |
| escrow_tax | ✓ | × |
| final_product_protection | ✓ | × |
| final_product_vat_tax | ✓ | × |
| final_shipping_fee | ✓ | × |
| final_shipping_vat_tax | ✓ | × |
| seller_transaction_fee | ✓ | × |
| order_chargeable_weight | ✓ | × |
| original_cost_of_goods_sold | ✓ | × |
| original_shopee_discount | ✓ | × |
| payment_promotion | ✓ | × |
| reverse_shipping_fee | ✓ | × |
| rsf_seller_protection_fee_claim_amount | ✓ | × |
| rsf_seller_protection_fee_premium_amount | ✓ | × |
| seller_coin_cash_back | ✓ | × |
| seller_discount | ✓ | × |
| seller_lost_compensation | ✓ | × |
| seller_shipping_discount | ✓ | × |
| seller_transaction_fee | ✓ | × |
| shipping_fee_discount_from_3pl | ✓ | × |
| shopee_discount | ✓ | × |
| shopee_shipping_rebate | ✓ | × |
| voucher_from_seller | ✓ | × |
| voucher_from_shopee | ✓ | × |
| aff_currency | × | ✓ |
| commission_fee_pri | × | ✓ |
| drc_adjustable_refund_pri | × | ✓ |
| escrow_amount_pri | × | ✓ |
| original_price_pri | × | ✓ |
| refund_amount_to_buyer_pri | × | ✓ |
| seller_return_refund_pri | × | ✓ |
| service_fee_pri | × | ✓ |
| sip_subsidy_pri | × | ✓ |
| pri_currency | × | ✓ |
| sip_subsidy | × | ✓ |


## 5. SIP 接口权限


目前，我们限制了 SIP A shop 只能调用部分的接口，详细列表请查看 FAQ


