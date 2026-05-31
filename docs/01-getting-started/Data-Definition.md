# V2.0 数据定义

> 来源: [Shopee Open Platform](https://open.shopee.com/developer-guide/31)
> 分类: Getting Started

## 基本数据类型

- uint8: 8 位无符号整数
- uint16: 16 位无符号整数
- int32: 32 位有符号整数
- uint32: 32 位无符号整数
- uint64: 64 位无符号整数
- timestamp: uint32
- country: ISO ALPHA-2 代码，2 个字符的字符串
## OrderStatus（订单状态）

- UNPAID: 订单已创建，买家尚未付款。
- PENDING: 订单待处理，无法进入发货安排。
- READY_TO_SHIP: 卖家可安排发货。
- PROCESSED: 卖家已在线安排发货，从第三方物流获取运单号。
- RETRY_SHIP: 第三方物流取件失败，需要重新安排发货。
- SHIPPED: 包裹已交付给第三方物流或已被第三方物流取走。
- TO_CONFIRM_RECEIVE: 买家已收到订单。
- IN_CANCEL: 订单正在处理取消。
- CANCELLED: 订单已取消。
- TO_RETURN: 买家申请退货，订单正在处理退货。
- COMPLETED: 订单已完成。
## ReturnStatus（退货状态）

- REQUESTED
- ACCEPTED
- CANCELLED
- JUDGING
- CLOSED
- PROCESSING
- SELLER_DISPUTE
## ReturnSolution（退货解决方案）

- RETURN_REFUND
- REFUND
## ReturnReason（退货原因）

- NONRECEIPT
- WRONG_ITEM
- ITEM_DAMAGED
- DIFF_DESC
- MUITAL_AGREE
- OTHER
- USED
- NO_REASON
- ITEM_WRONGDAMAGED
- CHANGE_MIND
- ITEM_MISSING
- EXPECTATION_FAILED
- ITEM_FAKE
- PHYSICAL_DMG
- FUNCTIONAL_DMG
- ITEM_NOT_FIT
- SUSPICIOUS_PARCEL
- EXPIRED_PRODUCT
- WRONG_ORDER_INFO
- WRONG_ADDRESS
- CHANGE_OF_MIND
- SELLER_SENT_WRONG_ITEM
- SPILLED_CONTENTS
- BROKEN_PRODUCTS
- DAMAGED_PACKAGE
- SCRATCHED
- DAMAGED_OTHERS
- SIZE_DEVIATION
- LOOK_DEVIATION
- DATE_DEVIATION
- DIFFERENT_DESCRIPTION
## LogisticsStatus（物流状态）

- LOGISTICS_NOT_START: 初始状态，订单尚未准备好履行
- LOGISTICS_PENDING_ARRANGE: 订单物流待安排
- LOGISTICS_COD_REJECTED: 集成物流 COD：订单 COD 被拒绝
- LOGISTICS_READY: 从支付角度看，订单已准备好履行：非 COD：已支付；COD：已通过 COD 筛选
- LOGISTICS_REQUEST_CREATED: 订单已安排发货
- LOGISTICS_PICKUP_DONE: 订单已交给第三方物流
- LOGISTICS_DELIVERY_DONE: 订单已成功送达
- LOGISTICS_INVALID: 订单在 LOGISTICS_READY 状态时取消
- LOGISTICS_REQUEST_CANCELED: 订单在 LOGISTICS_REQUEST_CREATED 状态时取消
- LOGISTICS_PICKUP_FAILED: 因取件失败或已取件但无法继续配送，第三方物流取消订单
- LOGISTICS_PICKUP_RETRY: 订单等待第三方物流重试取件
- LOGISTICS_DELIVERY_FAILED: 因第三方物流配送失败而取消订单
- LOGISTICS_LOST: 因第三方物流丢失订单而取消订单
## PackageFulfillmentStatus（包裹履行状态）

- LOGISTICS_NOT_START: 初始状态，包裹尚未准备好履行
- LOGISTICS_READY: 从支付角度看，包裹已准备好履行。非 COD：已支付；COD：已通过 COD 筛选
- LOGISTICS_REQUEST_CREATED: 包裹已安排发货
- LOGISTICS_PICKUP_DONE: 包裹已交给第三方物流
- LOGISTICS_DELIVERY_DONE: 包裹已成功送达
- LOGISTICS_INVALID: 包裹在 LOGISTICS_READY 状态时订单取消
- LOGISTICS_REQUEST_CANCELED: 包裹在 LOGISTICS_REQUEST_CREATED 状态时订单取消
- LOGISTICS_PICKUP_FAILED: 因取件失败或已取件但无法继续配送，第三方物流取消订单
- LOGISTICS_PICKUP_RETRY: 包裹等待第三方物流重试取件
- LOGISTICS_DELIVERY_FAILED: 因第三方物流配送失败而取消订单
- LOGISTICS_LOST: 因第三方物流丢失包裹而取消订单
## ReturnDisputeReasonId（退货争议原因 ID）

- "1": "我想拒绝未收到商品的索赔"
- "2": "我想拒绝退货请求"
- "3": "我同意退货请求，但我未收到应退回的商品"
- "4": "未收到退货"
- "5": "商品毁损/瑕疵"
- "6": "商品缺件/不符"
- "7": "非鉴赏期商品"
- "8": "其他"
- "9": "我已发货商品并有发货证明"
- "10": "我按买家订单发送了正确的商品"
- "11": "我发货时商品处于良好工作状态"
- "12": "我同意退货请求，但我未收到应退回的商品"
- "13": "我同意退货请求，但我收到了买家退回的错误/损坏商品"
- "41": "我已发货商品并有发货证明"
- "42": "我按买家订单发送了正确的商品"
- "43": "我发货时商品处于良好工作状态"
- "44": "无法与买家达成一致"
- "45": "商品不在鉴赏期内"
- "46": "未收到退回的商品"
- "47": "收到有物理损坏的退货商品"
- "48": "收到不完整的退货商品（缺少数量/配件）"
- "49": "收到错误的退货商品"
- "50": "收到退货商品，买家的索赔不正确"
- "51": "无法与卖家达成一致"
- "53": "买家的索赔不正确"
- "54": "买家退款金额错误"
- "55": "买家索赔正确，但我有其他顾虑"
- "56": "收到退货商品，但商品已被使用"
- "81": "未收到退回的商品"
- "82": "收到有物理损坏的退货商品"
- "83": "收到不完整的退货商品（缺少数量/配件）"
- "84": "收到错误的退货商品"
- "85": "商品不在鉴赏期内"
- "86": "收到退货商品，买家的索赔不正确"
- "87": "退回的商品不在买家法定撤销权范围内"
- "88": "买家在卖家安排退货中未响应"
- "89": "收到退货商品，但商品已被使用"
## AttributeType（属性类型）

- INT_TYPE
- STRING_TYPE
- ENUM_TYPE
- FLOAT_TYPE
- DATE_TYPE
- TIMESTAMP_TYPE
## AttributeInputTypeEdit（属性输入类型）

- DROP_DOWN
- TEXT_FILED
- COMBO_BOX
- MULTIPLE_SELECT
- ﻿MULTIPLE_SELECT_COMBO_BOX


更多详细信息，请查看：`https://open.shopee.com/faq?top=162&sub=166&page=1&faq=195`

## CancelReason（卖家取消原因）

- OUT_OF_STOCK
- UNDELIVERABLE_AREA（仅限 TW 和 MY）
## FeeType（费用类型）

- SIZE_SELECTION
- SIZE_INPUT
- FIXED_DEFAULT_PRICE
- CUSTOM_PRICE
- SELLER_LOGISTICS
## PaymentMethod（支付方式）

- Cybersource [ID, VN, TW, SG, MY, TH, PH]
- Nicepay Credit Card [ID]
- IPay88 Credit Card [MY]
- Airpay Credit Card [PH]
- Stripe CC [PH]
- Airpay Credit Card [ID, VN, TW, TH]
- Bank Transfer [ID]
- Bank BCA (Manual Transfer) [ID]
- Bank Mandiri (Manual Transfer) [ID]
- Bank BNI (Manual Transfer) [ID]
- Bank BRI (Manual Transfer) [ID]
- Bank CIMB Niaga (Manual Transfer) [ID]
- Bank Transfer [VN]
- Fubon Bank Transfer [TW]
- Esun Bank Transfer [TW]
- Bank Transfer [TW]
- Esun CB Bank Transfer [TW]
- Bank Transfer [SG]
- Bank Transfer [MY]
- ATM Payment [TH]
- ATM Payment (BBL) [TH]
- Bank Transfer [TH]
- ATM Payment (KBANK) [TH]
- ATM Payment (KTB) [TH]
- ATM Payment (SCB) [TH]
- ATM Payment (BAY) [TH]
- Online Payment (KBANK) [TH]
- Online Payment (BAY) [TH]
- Bank Transfer [PH]
- Cash on Delivery [ID, VN, SG, MY, TH, PH]
- 现付 [TW]
- Shopee Seller Wallet [ID]
- Shopee Wallet [ID, VN, TW, SG, MY, TH, PH]
- Indomaret [ID]
- Bank BRI (Virtual Account) [ID]
- Bank BCA (Virtual Account) [ID]
- Bank Mandiri (Virtual Account) [ID]
- Bank BNI (Virtual Account) [ID]
- Virtual Account Parent [ID]
- Android Pay [SG]
- MOLPay [MY]
- iPay 88 [MY]
- iBanking Payment [TH]
- iBanking Payment (BBL) [TH]
- iBanking Payment (KTB) [TH]
- iBanking Payment (SCB) [TH]
- Dragonpay - Remittance Center [PH]
- Dragonpay - OTC [PH]
- Dragonpay - Online Payment [PH]
- Buyer-Seller Self Arrange [ID, VN, TW, SG, MY, TH, PH]
- Kredivo [ID]
- Kredivo - BNPL [ID]
- Kredivo - 3 Months Installment [ID]
- Kredivo - 6 Months Installment [ID]
- Kredivo - 12 Months Installment [ID]
- Nicepay Credit Card Installment [ID]
- BCA One Klik [ID]
- Akulaku [ID]
- Free [Vn, TW, SG, MY, TH, PH]
- iPay88 CC Installment [MY]
- Ebanx Credit Card [BR]
- Ebanx Credit Card Installment [BR]
- Ebanx Credit Card Installment 1x installment plan [BR]
- Ebanx Credit Card Installment 2x installment plan [BR]
- Ebanx Credit Card Installment 3x installment plan [BR]
- Ebanx Credit Card Installment 4x installment plan [BR]
- Ebanx Credit Card Installment 5x installment plan [BR]
- Ebanx Credit Card Installment 6x installment plan [BR]
- Ebanx Boleto [BR]
## CancelReason（取消原因）

- Out of Stock
- Buyer Request to Cancel
- Undeliverable Area
- COD Unsupported
- Parcel is Lost
- Game Completed
- Unpaid Order
- Underpaid Order
- Unsuccessful / Rejected Payment
- Logistics Request is Cancelled
- 3PL pickup Fail
- Failed Delivery
- COD Rejected
- Seller did not Ship
- Transit Warehouse Cancelled
- Other
- Inactive Seller
- Auto Cancel
- Logistic Issue
- You are approver did not approve order on time.
- You are unable to place order at the moment.
- TBC
## ShippingDocumentType（运输单据类型）

- NORMAL_AIR_WAYBILL
- THERMAL_AIR_WAYBILL
- NORMAL_JOB_AIR_WAYBILL
- THERMAL_JOB_AIR_WAYBILL
## ItemStatus（商品状态）

- NORMAL
- BANNED
- UNLIST
- REVIEWING
- SELLER_DELETE
- SHOPEE_DELETE
## StockType（库存类型）

- 1: Shopee 仓库库存
- 2: 卖家库存
## Language（语言）

- zh-hans
- zh-hant
- ms-my
- en-my
- en
- id
- vi
- th
- pt-br
- es-mx
- pl
- es-CO
- es-CL
- es-ES
- es-ar
## PromotionType（促销类型）

- Campaign
- Discount Promotions
- Flash Sale
- Whole Sale
- Group Buy
- Bundle Deal
- Welcome Package
- Add-on Discount
- Brand Sale
- In ShopFlash Sale
- Gift with purchase
- ﻿Exclusive Price
- Platform Streaming
- Seller Streaming
## BuyerCancelReason（买家取消原因）

- Seller is not Responsive to buyer's Inquires
- Seller ask Buyer to Cancel
- Modify Existing Order
- Product has Bad Reviews
- Seller Takes too Long to Ship The Order
- Seller is Untrustworthy
- Others
- Forgot to Input Voucher Code
- Need to change delivery address
- Need to Change Delivery Address
- Need to input / Change Voucher Code
- Need to Modify Order
- Payment Procedure too Troublesome
- Found Cheaper Elsewhere
- Don't Want to Buy Anymore
- You are approver rejected the order.
- You are unable to place order at the moment.
- Need to change delivery address
- Too long delivery time
- Modify existing order (color, size, voucher, etc)
- Change of mind / others
## TrackingLogisticsStatus（追踪物流状态）

- INITIAL
- ORDER_INIT
- ORDER_SUBMITTED
- ORDER_FINALIZED
- ORDER_CREATED
- PICKUP_REQUESTED
- PICKUP_PENDING
- PICKED_UP
- DELIVERY_PENDING
- DELIVERED
- PICKUP_RETRY
- TIMEOUT
- LOST
- UPDATE
- UPDATE_SUBMITTED
- UPDATE_CREATED
- RETURN_STARTED
- RETURNED
- RETURN_PENDING
- RETURN_INITIATED
- EXPIRED
- CANCEL
- CANCEL_CREATED
- CANCELED
- FAILED_ORDER_INIT
- FAILED_ORDER_SUBMITTED
- FAILED_ORDER_CREATED
- FAILED_PICKUP_REQUESTED
- FAILED_PICKED_UP
- FAILED_DELIVERED
- FAILED_UPDATE_SUBMITTED
- FAILED_UPDATE_CREATED
- FAILED_RETURN_STARTED
- FAILED_RETURNED
- FAILED_CANCEL_CREATED
- FAILED_CANCELED
## SellerProofStatus（卖家举证状态）

- NOT_NEEDED
- PENDING
- UPLOADED
- OVERDUE
## TransactionType（交易类型）

- ESCROW_VERIFIED_ADD = 101;  // 托管已验证并支付给卖家。
- ESCROW_VERIFIED_MINUS = 102; // 托管已验证，因托管金额为负数而从卖家扣款。
- WITHDRAWAL_CREATED = 201; // 卖家已创建提现，从余额中扣除。
- WITHDRAWAL_COMPLETED = 202; // 提现已完成，进行中金额减少。
- WITHDRAWAL_CANCELLED = 203; // 提现已取消，金额加回卖家余额。进行中金额也减少。
- REFUND_VERIFIED_ADD = 301; //  正常订单退款。
- AUTO_REFUND_ADD=302; // 正常订单自动退款。
- ADJUSTMENT_ADD = 401; // 一项调整已支付给卖家。
- ADJUSTMENT_MINUS = 402; // 一项调整已从卖家扣款。
- FBS_ADJUSTMENT_ADD = 404; // 与 Shopee 履约订单相关的一项调整已添加到卖家账户。
- FBS_ADJUSTMENT_MINUS = 405; // 与 Shopee 履约订单相关的一项调整已从卖家账户扣除。
- ADJUSTMENT_CENTER_ADD = 406; // 一项调整已添加到卖家钱包。
- ADJUSTMENT_CENTER_DEDUCT = 407; // 一项调整已从卖家钱包扣除。
- ESCROW_ADJUSTMENT_FOR_FD_DEDUCT = 408; // 已取消/无效订单的 FSF 费用转移。
- PERCEPTION_VAT_TAX_DEDUCT = 409; // 感知制度增值税的额外费用（阿根廷）。
- ADJUSTMENT_FOR_RR_AFTER_ESCROW_VERIFIED = 411;// 托管验证后的 RR 调整（卖家已收到包裹），扣款。
- AFFILIATE_COMMISSION_FEE_ADD = 412; // 将卖家联盟佣金记入卖家钱包。
- CROSS_MERCHANT_ADJUSTMENT_ADD = 413;// 根据特定交叉 listing 订单中 FBS/B2C 店铺拥有的托管金额，自动正向调整 FBS/B2C 钱包。
- CROSS_MERCHANT_ADJUSTMENT_DEDUCT = 414; // 根据特定交叉 listing 订单中 FBS/B2C 店铺拥有的托管金额，自动负向调整 FBS/B2C 钱包。
- SELLER_COMPENSATE_ADD = 415; // 在新的 RR 流程中，买家将获得自动和加速退款的好处，Shopee 可以在没有卖家的情况下接受退款。随后，如有需要，卖家可以提出补偿请求。此交易类型用于补偿此类卖家。
- CAMPAIGN_PACKAGE_ADD = 416; // 退还没有被多收活动费用的卖家，仅限 ID。
- CAMPAIGN_PACKAGE_MINUS = 417;// 进一步扣除活动费用未被足额收取的卖家，仅限 ID。
- PAID_ADS_CHARGE = 450; // 付费广告从卖家扣除。
- PAID_ADS_REFUND = 451; // 付费广告退还卖家。
- FAST_ESCROW_DISBURSE = 452; // 加。快速托管的第一笔付款已支付给卖家。
- AFFILIATE_ADS_SELLER_FEE = 455; // 扣。联盟广告卖家费用从卖家收取。
- AFFILIATE_ADS_SELLER_FEE_REFUND = 456; // 加。联盟广告卖家费用退还卖家。
- FAST_ESCROW_DEDUCT = 458; // 发生退货退款时，快速托管从卖家余额中扣除。
- FAST_ESCROW_DISBURSE_REMAIN = 459; // 快速托管的第二笔付款已支付给卖家。
- AFFILIATE_FEE_DEDUCT = 460; // 使用联盟营销服务的联盟营销费用从卖家扣除。
- SHOPEE_WALLET_PAY = 501;// 本地 SIP，从卖家钱包扣除。
- SPM_DEDUCT = 502;// SPM 从卖家钱包扣款作为支付。
- APM_DEDUCT = 503;// APM 从卖家钱包扣款作为支付。
- SPM_REFUND_ADD = 504; // 正常订单退款。
- APM_REFUND_ADD = 505; // 正常订单退款。
- DP_REFUND_VERIFIED_ADD = 701; // 数字产品购买退款已验证并支付给卖家。
- SPM_DEDUCT_DIRECT = 801; // Shopee Credit 卖家贷款还款，例如：provision channel id. 8008601
- SPM_DISBURSE_ADD = 802; // 卖家贷款支付到卖家钱包。
## SellerCompensationStatus（卖家补偿状态）

- COMPENSATION_NOT_APPLICABLE
- COMPENSATION_INITIAL_STAGE
- COMPENSATION_PENDING_REQUEST
- COMPENSATION_NOT_REQUIRED
- COMPENSATION_REQUESTED
- COMPENSATION_APPROVED
- COMPENSATION_REJECTED
- COMPENSATION_CANCELLED
- COMPENSATION_NOT_ELIGIBLE
## NegotiationStatus（协商状态）

- PENDING_RESPOND
- PENDING_BUYER_RESPOND
- TERMINATED
## **退货退款请求类型**

- 0:  正常 RR（买家收到包裹后，根据预计送达日期/配送完成提起的 RR）
- 1: 运输中 RR（商品仍在运输途中时，买家提起的 RR）
- 2: 当场退货（买家在配送时拒收包裹后，由配送员提起的 RR）
## **验证类型**

- seller_validation: 对于退货包裹将送达卖家进行验证和决定（退款买家或提起争议）的退货退款请求
- warehouse_validation: 对于退货包裹将送达仓库进行验证和决定（退款买家或提起争议）的退货退款请求
## **逆向物流状态**
### **【正常退货】**

- LOGISTICS_PENDING_ARRANGE: 退货现等待用户选择配送选项。集成物流和非集成物流均适用。
- LOGISTICS_READY: 用户已选择配送选项，等待系统创建物流请求。运单号尚不可用。集成物流和非集成物流均适用。
- LOGISTICS_REQUEST_CREATED: 物流请求已成功创建。运单号应可用。
- LOGISTICS_PICKUP_RETRY: 第三方物流提供商将再次尝试从买家处取件。仅适用于集成物流，因为此状态由第三方物流提供商回传至 Shopee。
- LOGISTICS_PICKUP_FAILED: 第三方物流提供商从买家处取件失败。仅适用于集成物流，因为此状态由第三方物流提供商回传至 Shopee。
- LOGISTICS_PICKUP_DONE: 对于集成物流，表示包裹已被第三方物流提供商取走。对于非集成物流，表示用户已输入发货证明。
- LOGISTICS_DELIVERY_FAILED: 包裹配送至卖家失败。仅适用于集成物流，因为此状态由第三方物流提供商回传至 Shopee。
- LOGISTICS_LOST: 包裹已被标记为丢失。仅适用于集成物流，因为此状态由第三方物流提供商回传至 Shopee。
- LOGISTICS_DELIVERY_DONE: 包裹已成功送达卖家。仅适用于集成物流，因为此状态由第三方物流提供商回传至 Shopee。
### **【运输中 RR】**

- Preparing
- Delivered  
- Delivery Failed  
- Lost
### **【当场退货】**

- Preparing
- Delivered  
- Delivery Failed  
- Lost
## **退货后物流状态**


注意：仅适用于从仓库寄回卖家的退货包裹

- POST_RETURN_LOGISTICS_REQUEST_CREATED: 物流请求已成功生成，附带运单号。
- POST_RETURN_LOGISTICS_REQUEST_CANCELED: 物流请求被仓库团队取消
- POST_RETURN_LOGISTICS_PICKUP_FAILED: 取件失败
- POST_RETURN_LOGISTICS_PICKUP_RETRY: 后续取件尝试
- POST_RETURN_LOGISTICS_PICKUP_DONE: 取件成功；正在运往目的地
- POST_RETURN_LOGISTICS_DELIVERY_FAILED: 包裹配送失败。配送员将包裹退回仓库
- POST_RETURN_LOGISTICS_DELIVERY_DONE: 包裹配送成功
- POST_RETURN_LOGISTICS_LOST: 包裹标记为丢失
