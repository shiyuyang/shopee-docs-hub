# SIP最佳实践

> 来源: [Shopee Open Platform](https://open.shopee.com/developer-guide/261)
> 分类: API Best Practices

## 什么是SIP?

SIP全称为Shopee International Platform（Shopee国际平台）。卖家参加SIP项目后，Shopee会帮您运营店铺，包括根据当地市场特点设置并提报行销活动等。 卖家开店后，您只需提前绑定收款账户、定期检查产品库存、参与各类活动报价确认、并按照发货时效发货即可！

## 名词解释：

**P shop (primary shop) **: 代运营模式中，卖家自主经营的主店铺，又称主店铺。


**A shop (affiliated shop) **:  Shopee帮助卖卖家运营的代运营店铺，又称附属店铺。


**CB SIP (cross border SIP) **：如果P shop是跨境卖家运营，又称CB SIP模式。


**Local SIP**：如果P shop是本土卖家运营，又称local SIP模式。


**SIP rate**: 只适用于CBSIP。SIP调价比例，是指卖家根据商品成本价，对附属店铺设置的折扣率。当商品在附属店铺售出后，Shopee将根据商品成本价格和SIP调价比例，自动计算出给卖家最后的结算价格。


**SIP Item price**: 商品成本价格，Shopee将根据此价格计算A shop商品的售价以及商品结算价。


**Settlement price**: 卖家结算价格，Shopee将根据此价格结算给卖家。

## 1.SIP店铺授权
### 1.1 非CNSC卖家
#### 1.1.1 授权流程


授权流程同文章<u>授权与鉴权</u> 当卖家登陆SIP P Shop的账号进入授权页面点击确认授权后，SIP P Shop将授权给此APP。



![图片](https://open.shopee.com/opservice/api/v1/image/download/?image_id=wICW%2F2f1YfQskbVUFBJy5gR%2B5iF%2FjUfg2rFw2SvGKPuwFfZ3v0oQ7ZqVofDpl3UbnRlwvoqv%2FOwOaJRMX9RkgQ%3D%3D&image_type=png)

#### 1.1.2 获取code

授权成功后，您可以直接通过回调地址拿到P Shop的shop_id以及可用的code。


#### 1.1.3 获取P shop的token


您可以调用<u>v2.public.get_access_token</u>接口，传入授权成功后的P shop的shop id和code，接口将返回当前授权成功的P shop可用的access token和refresh token。


#### 1.1.5 刷新access_token

此时第三步获取的access token和refresh token 可用于所有的P shop。后续请调用v<u>2.public.refresh_access_token</u> 接口分别刷新P shop的access token。



注意⚠️:


1. 新的access_token生成后, 旧access_token依然在5分钟内有效。


2. 重新授权会触发刷新refresh_token和access_token。


3. 调用Refreshaccesstoken接口要在授权有效期内。


4. 如果丢失了返回的新的refresh_token和access_token，请查看此<u>FAQ</u>


### 1.2 CNSC卖家
#### 1.2.1 授权流程


授权流程同<u>授权与鉴权</u> 当卖家登陆Main account进入授权页面后，每个merchant下的店铺列表中将会对SIP P Shop显示“SIP”的标签，点击右侧的“view”将能看到此P Shop下所有的A Shop信息与授权状态。勾选SIP P Shop并点击确认授权给此APP，则它此时绑定的所有SIP A Shop都将自动授权给此APP。



![图片](https://open.shopee.com/opservice/api/v1/image/download/?image_id=fON4MRg2jyP7Ska%2B5zTDPdB7n6PN7pkAWV637GaLOIVyn4cdB2EM4ZMiM6jqB%2FE7x0T%2BVB%2BsrXZrh7tUKmiO9Q%3D%3D&image_type=png)



注意⚠️


一个main account所有未绑定merchant的shop，都会在Unupgraded Shop Group列表下，Unupgraded Shop Group列表的shop如果有SIP标识，则同样代表它们是SIP P Shop。


![图片](https://open.shopee.com/opservice/api/v1/image/download/?image_id=HCsGhQQJHApkIrEvBvtRWwnpplJQon2O6cjzNiTWaYLEMpJ4CMKIB9x5Ns1IVoBI8MOag5y8aifm01CPb4Lb3g%3D%3D&image_type=png)

#### 1.2.2 获取code

授权成功后，您可以直接通过回调地址拿到main_account_id以及可用的code。


#### 1.2.3 获取token


您可以调用<u>v2.public.get_access_token</u>接口，传入授权成功后的到main_account_id和code。merchant_id_list将返回当前授权成功的merchant，shop_id_list将返回当前授权成功的所有shop, 包括SIP P shop、A shop以及非SIP的shop id。access_token可以被当前授权成功的所有merchant id和shop id所共用。refresh_token同理。


#### 1.2.4 获取店铺关系

随后，调用<u>v2.merchant.get_shop_list_by_merchant</u>接口，可以获取某个merchant关联的已授权店铺列表，调用<u>v2.shop.get_shop_info</u>接口，可以通过返回参数获取店铺是否属于SIP店铺，以及SIP主店铺和附属店铺的关系。


- 如果是普通店铺，is_sip=false 且sip_affi_shops字段不返回；
- 如果是SIP P shop，is_sip=true 且sip_affi_shops字段返回且返回A shop id list；
- 如果是SIP A shop， is_sip=true 且sip_affi_shops字段不返回。


请注意每个shop id和merchant id 的access_token和refresh_token都需要分开保存。您调用<u>v2.public.refresh_access_token</u>接口时，请分别刷新每个shop id和每个merchant id 的access token和refresh token。（即刷新后每个shop id的access token和refresh token不能共用，merchant id同理）。


## 2. SIP商品管理
### 2.1 商品同步逻辑

| 信息 | 同步逻辑 |
| --- | --- |
| 商品基础信息 | 刊登：卖家发布P shop商品后，Shopee会将商品信息自动翻译成A shop当地语言并创建一个A shop商品。更新：卖家修改了P shop商品，Shopee会将新商品信息自动同步到A shop商品。 |
| 商品状态 | P shop商品被下架或者删除，A shop商品也会被下架和删除，卖家不能单独操作A shop 商品的状态。 |
| 商品库存 | P shop商品库存等于A shop商品库存，例如P shop下有2个A shop, 分别是A shop1, A shop2, 且P shop库存=10，则A shop1库存=A shop2库存=10。当A shop1售出1个商品，则库存P shop=A shop1=A shop2=9。 |
| 商品价格 | 卖家更新P shop商品价格，Shopee会将同步到A shop商品价格。 |
### 2.2 商品价格逻辑
#### SIP Item Price

<u>v2.product.get_item_base_info</u>和<u>v2.product.get_model_list</u>接口价格字段返回说明


 "price_info": [


                    {


                        "currency": "MYR",


                        "original_price": 179.58,


                        "current_price": 179.58                   


                       ** "sip_item_price_currency": "CNY",**


                       ** "sip_item_price": 230.87,**


                       ** "sip_item_price_source": "auto"**


                    }


注意⚠️

- 如果商品是主店铺商品且不包含变体，则您需要调用<u>v2.product.get_item_base_info</u> 接口即可拿到商品的sip_item_price/sip_item_price_source/sip_item_price_currency。
- 如果商品是主店铺商品且包含变体，则您需要调用<u>v2.product.get_model_list</u> 接口即可拿到变体的sip_item_price/sip_item_price_source/sip_item_price_currency。
- 如果商品是非主店铺商品，<u>v2.product.get_item_base_info</u>和<u>v2.product.get_model_list</u>接口将不返回sip_item_price/sip_item_price_source/sip_item_price_currency 字段。

## 3. SIP订单管理
### 3.1订单同步逻辑
#### 3.1.1 CB SIP

请您分别获取SIP P shop order list 以及SIP A shop order list 进行履约。其中：

- SIP A shop中的订单，将不对P shop seller暴露买家支付金额。
- SIP A shop中的订单，在get_order_detail接口中返回的currency为 CNY 或 USD。
#### 3.1.2 Local SIP


Shopee自动将SIP A shop order同步至SIP P shop，您仅需要获取SIP P shop order list并履约。其中：SIP A shop的订单对于P shop seller无感知，A shop生成对应的P shop订单，收货人则为位于Local境内的Shopee转运仓；Shopee转运仓会进行跨境发货，最终发给Buyer。




注意⚠️


Order Push 会同时推送P shop和A shop的订单，对于CB SIP的卖家需要关注P shop和A shop的推送，Local SIP的卖家只需要关注P shop的推送即可。



更多订单履约流程请参考：<u>https://open.shopee.com/developer-guide/229</u>



## 4. SIP订单收入

1. CB SIP A shop中的订单，在get_escrow_detail接口中同时返回A shop currency amount 以及对应的P shop currency.
1. Local SIP A shop中的订单收入相关数据，也默认转换成P currency，与P shop订单无差异。


请留意<u>v2.payment.get_escrow_detail</u>接口下列字段



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


## 5. SIP接口权限


目前，我们限制了SIP A shop只能调用部分的接口，详细列表请查看<u>FAQ</u>


