# API 调用

> 来源: [Shopee Open Platform](https://open.shopee.com/developer-guide/16)
> 分类: Getting Started


*请注意本文章只针对 V2.0接口调用进行讲述。*

## **请求域名**


正式环境和测试环境我们都提供两种域名：


正式环境：


`https://openplatform.shopee.cn/` —服务部署地近中国大陆的开发者使用


`https://openplatform.shopee.com.br/` —服务部署地近美国的开发者使用


`https://partner.shopeemobile.com/` —服务部署地近新加坡的开发者使用


沙箱环境：


`https://openplatform.sandbox.test-stable.shopee.sg/` —所有开发者都可以使用


`https://openplatform.sandbox.test-stable.shopee.cn/` —中国大陆的开发者使用


请您根据调用 Open API 服务器所在地，选择正确的域名。

## **请求方法**


目前 Open API 只提供两种请求方法：**GET** 和 **POST**。


## 接口协议

大多数 API 使用 HTTP/JSON 协议。某些 API（例如上传文件的 API）使用 HTTP/FORM。

## **请求参数**


在 API 文档中，您将会看到两种请求参数，一种是公共请求参数（Common Parameter），一种是业务请求参数（Request Parameter），对于**GET**类型的接口，可能两种参数同时存在，也可能只存在公共请求参数，Post 类型接口，两种参数同时存在。


下面是关于公共参数的说明：

| 参数 | 说明 |
| --- | --- |
| partner_id | 所有接口调用都需要合作伙伴 ID, 您可以通过在控制台创建 App 获取到 partner id, Test partner_id 只能用于测试环境，Live partner_id 只能用于生产环境 |
| timestamp | 所有接口调用都需要时间戳，时间戳样例：1610000000，每次的接口请求都需要用最近5 分钟内的时间戳请求，点击这里了解时间戳 |
| sign | 所有接口调用都需要签名，签名需要用 SHA256算法生成，不同接口类型签名生成方法不同，详细参考本文章中<签名的计算>部分 |
| access_token | 获取和修改卖家数据相关接口都需要访问令牌，访问令牌4 小时有效，可在有效期内重复使用，访问令牌需要定期刷新，获取和刷新方法可以参考授权文章 |
| shop_id | Shopee 商店的唯一标识 ID，可以通过店铺授权后获取到，获取方法参考授权文章 |
| merchant_id | Shopee 商家的唯一标识 ID，Open API 只支持跨境卖家使用 merchant id，可以通过店铺授权后获取到，获取方法参考授权文章 |
## **Open API 的三种类型**


在 API 文档中，根据公共参数的不同，我们分为三种 API 类型，这三种类型包含的公共参数如下：

-**Shop API**: partner_id、 timestamp、sign、access_token、shop_id
-**Merchant API**: partner_id、 timestamp、sign、access_token、merchant_id
-**Public API**: partner_id、 timestamp、sign


可以看到，Public 类型接口不需要 access_token, Shop 类型和 Merchant 类型接口都需要 access_token, 这意味着 Shop 类型和 Merchant 类型接口需要完成店铺授权之后才能调用，Public 类型接口不需要。


*目前只有 Shopee 跨境商家需要使用 Merchant 类型接口，本土卖家不需要使用。

## **签名的计算**


**第一步: 创建基本字符串(Base string):**


不同类型的 API，Base string 包含的元素不一样，请严格按照下列先后次序，将 api path(不带 host) 和下列公共参数拼接为单一字符串，即为 base string:


*api path 样例：/api/v2/auth/token/get


**Shop API**: partner_id, api path, timestamp, access_token, shop_id


*样例：


partner_id: 2001887


api path: /api/v2/shop/get_shop_info


timestamp: 1655714431


access_token: 59777174636562737266615546704c6d


shop id: 14701711


Base string=2001887/api/v2/shop/get_shop_info165571443159777174636562737266615546704c6d14701711


**Merchant API:**partner_id, api path, timestamp, access_token, merchant_id


*样例：


partner_id: 2001887


api path: /api/v2/global_product/get_category


timestamp: 1655714431


access_token: 09777174636962737266615546704c6d


merchant_id: 1000000


Base string=2001887/api/v2/global_product/get_category165571443109777174636962737266615546704c6d1000000


**Public API**:partner_id, api path, timestamp


*样例：


partner_id:2001887


api path: /api/v2/public/get_shops_by_partner


timestamp:1655714431


Base string=2001887/api/v2/public/get_shops_by_partner1655714431


**第二步: 采用 HMAC-SHA256算法计算签名(sign)**


将基本字符串(Base string)和 partner Key( 通过控制台获取）用 HMAC-SHA256散列算法来计算签名。 散列函数的输出是一个十六进制编码的字符串。


*样例：


sign=56f31d01aeda9d08bf456b37f6f6640ef8614b4d6ad49baafe30b39a061f0e26


*如果您在调用过程中遇到 Wrong sign 的报错，可以点击这里查看解决方案


生成签名代码样例：


```python
#!/usr/bin/env python
# encoding: utf-8

import hmac
import hashlib
import time
import requests

timest = int(time.time())
host = "https://partner.shopeemobile.com"
partner_id = 80001
partner_key = "your_partner_key"
access_token = "your_access_token"

# ---- Shop level API call ----
shop_id = 209920
path = "/api/v2/example/shop_level/get"

# Build base string: partner_id + api_path + timestamp + access_token + shop_id
base_string = f"{partner_id}{path}{timest}{access_token}{shop_id}"
sign = hmac.new(partner_key.encode(), base_string.encode(), hashlib.sha256).hexdigest()

url = f"{host}{path}?partner_id={partner_id}&shop_id={shop_id}&timestamp={timest}&access_token={access_token}&sign={sign}"
headers = {"Content-Type": "application/json"}
resp = requests.post(url, headers=headers)

# ---- Merchant level API call ----
merchant_id = 1234567
path = "/api/v2/example/merchant_level/get"

base_string = f"{partner_id}{path}{timest}{access_token}{merchant_id}"
sign = hmac.new(partner_key.encode(), base_string.encode(), hashlib.sha256).hexdigest()

url = f"{host}{path}?partner_id={partner_id}&merchant_id={merchant_id}&timestamp={timest}&access_token={access_token}&sign={sign}"
resp = requests.post(url, headers=headers)

# ---- Public API call (no access_token needed) ----
path = "/api/v2/auth/access_token/get"

base_string = f"{partner_id}{path}{timest}"
sign = hmac.new(partner_key.encode(), base_string.encode(), hashlib.sha256).hexdigest()

url = f"{host}{path}?partner_id={partner_id}&timestamp={timest}&sign={sign}"
body = {
 "partner_id": partner_id,
 "merchant_id": merchant_id,
 "refresh_token": "testing_token",
}
resp = requests.post(url, json=body, headers=headers)
```

## **API 请求样例**


对于**GET**请求，您需要将**公共参数和业务参数都放在 url**中


例如`v2.product.get_category` 


请求 URL 样例:


`https://partner.shopeemobile.com/api/v2/product/get_category?partner_id=851249&timestamp=1654673582&shop_id=1001094&access_token=367a0a8eb9d1837cbf7c43b587a0faa4&sign=a40fc50a08c382eeee08e2eb00deb8464c6fdcbe4f1c271e033cdbca3ded4d5b&language=zh-hans`


**此接口中，partner_id、timestamp、access_token、shop_id、sign 都是公共参数，language 是业务参数*


对于**Post 请求**，您需要将**公共参数放在请求 url 中**，**业务参数放在 request body 中**


例如`v2.shop.update_profile` 


请求 URL 样例:


`https://partner.shopeemobile.com/api/v2/shop/update_profile?partner_id=851249&timestamp=1654673582&shop_id=1001094&access_token=367a0a8eb9d1837cbf7c43b587a0faa4&sign=80cbce8da907d5a1237711409920fc16908a9f9e01b1254ff9cc44aaf0836122`


Request body:


{


"shop_logo": "https://cf.shopee.sg/file/8424390be4677b0b3c37ce6499ce261a",


"description": "TTest",


"shop_name": "123"


}


**此接口中，partner_id、timestamp、access_token、shop_id、sign 都是公共参数，shop_log、description、shop_name 是业务参数*

## **API 返回参数**

| 字段名 | 是否必返 | 说明 |
| --- | --- | --- |
| request id | 是 | 每个 API 请求都有一个唯一的 request id 相关联，当您遇到 API 问题时请提供这个 ID 和对应的接口，以保证您可以获得更快的回复 |
| error | 是 | 错误码。当请求成功时，error 将返回空，如果请求失败，将会返回对应 error code |
| message | 否 | 错误提示信息，当请求成功时，message 将返回空，如果请求失败，这个字段将返回更加详细的错误信息 |
| warning | 否 | 接口调用成功，但部分数据没有返回或者批量请求有部分失败，将通过此字段返回信息 |
| response | 否 | 当请求成功时，这个字段将返回具体的数据 |
## **API 功能**

| API 模块 | 功能说明 |
| --- | --- |
| Product | 获取商品相关的类目树，属性和品牌等信息，获取店铺商品数据，创建/删除/更新店铺商品信息，获取商品参与活动信息，置顶商品，获取置顶商品列表，评论商品，获取评论列表，获取商品推荐类目和推荐属性，注册商品品牌。 |
| Shop | 获取店铺名称，店铺所属市场，店铺类型等，更新店铺信息 |
| Merchant | *该模块只有跨境卖家需要获取商家信息（商家名称/地区/币种以及），获取商家下已授权所有的店铺列表 |
| GlobalProduct | *该模块只有跨境卖家需要获取相关的类目树，属性和品牌等信息，获取全球商品数据，创建/删除/更新全球商品，获取可发布市场，发布全球商品，设置全球商品信息同步开关，获取已发布市场商品，获取市场商品对应的全球商品 ID，获取全球商品推荐类目和推荐属性 |
| MediaSpace | 上传视频，上传图片 |
| Order | 获取店铺订单列表，获取订单详情，拆单，解除拆单，取消订单，处理卖家取消订单申请，设置订单备注，添加/上传发票，获取待上传发票订单列表，下载发票，获取发票信息 |
| Logistics | 获取发货参数，订单发货，获取订单物流跟踪号，获取面单支持格式，获取面单，获取订单物流轨迹，获取店铺地址列表，删除店铺地址，设置店铺地址标识，获取店铺渠道信息，更新店铺渠道状态，批量发货 |
| FirstMile | *该模块只有跨境卖家需要获取未绑定订单，生成批次号，获取批次号详情，绑定首公里订单，获取批次号列表，获取首公里面单，获取首公里渠道 |
| Returns | 获取退货退款的列表，获取退款详情，获取退货退款方案，确认退款，提交争议，退款议价，上传争议图片证据 |
| Payment | 获取订单收入，获取放款数据，获取钱包数据，获取结算订单列表，分期付款店铺设置和商品列表 |
| Discount | 折扣的增删改查 |
| Bundle Deal | 捆绑销售的增删改查 |
| Add-On Deal | 加购活动的增删改查 |
| Voucher | 优惠券的增删改查 |
| Follow Prize | 关注礼的增删改查 |
| TopPicks | 店长推荐的增删改查 |
| ShopCategory | 商店分类的增删改查 |
| AccountHealth | 获取店铺表现数据，获取店铺罚分 |
| Public | 获取已授权店铺，获取已授权商家，重发 code 获取令牌，升级 code 获取令牌，获取令牌，刷新令牌 |
| Push | 获取 push 设置/更新 push 设置 |
| Chat | *此模块只开放给白名单用户，有需要请先查看如何申请 FAQ 获取会话列表，获取会话详情，获取会话信息，删除会话，标记会话未读，置顶/解除置顶会话，上传聊天图片，发送人工回复信息，发送自动回复信息，获取/设置议价状态 |
## API 限频


每个 API 都有调用频率限制，如果超出限制您会收到**HttpCode429**的错误。当您收到此错误时，请适当降低调用频率，以便在接口限流的情况下保持稳定的调用，避免频繁的重试操作，因为这会进一步增加接口的负载压力。如果您未及时进行调整并且持续产生此错误，我们会限制您的 API 调用，这可能会对您的业务产生不利影响。

## **API 问题**


如果您在 API 集成过程中，遇到问题，可以先查询 FAQ 模块，如果仍不能解决，可以提报工单**。**

