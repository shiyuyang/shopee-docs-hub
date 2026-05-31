# Shopee Video API 对接指引

> 来源: [Shopee Open Platform](https://open.shopee.com/developer-guide/706)
> 分类: API Best Practices

### 1. Shopee Video 简介


Shopee Video 是一个内容创作和营销工具，使卖家和达人能够通过吸引人的短视频展示产品。它为卖家和达人制作和分享内容提供了灵活性。通过利用视觉叙事，创作者可以增加互动并推动更高的转化率。



**好处：**

- **获取买家和粉丝：**吸引关注并建立忠实的客户群。
- **提高知名度：**动态展示产品和品牌。
- **驱动销售：**建立信任，提高转化率并促进购买。


开放平台提供了一套用于视频管理和分析的 Open API，允许开发者上传和管理视频、发布内容以及跟踪效果，以优化视频驱动的营销策略。

### 2. 对接概述


对接 Shopee Video API 主要包括两个阶段：

- **通过公共视频上传 API 上传视频** – 上传视频文件并获取 video_upload_id。
- **通过 Shopee Video API 管理和发布视频** – 使用 v2.video.* API 来选择封面、编辑视频信息、发布、删除、查询和分析视频表现。
### 3. 公共视频上传 API


开放平台提供了一套公共的视频上传 API 和推送机制，旨在满足所有未来的视频上传场景。目前，这些 API 仅支持 Shopee Video。



**API 和推送列表：**


- <u>v2.media.init_video_upload</u>：初始化视频上传任务。
- <u>v2.media.upload_video_part</u>：分片上传视频文件。
- <u>v2.media.complete_video_upload</u>：完成上传并通知系统进行处理。
- <u>v2.media.get_video_upload_result</u>：查询上传结果。
- <u>v2.media.cancel_video_upload</u>：取消上传任务。
- <u>video_upload_result_push</u>：当上传达到最终状态 (SUCCEEDED, FAILED, 或 CANCELLED) 时推送通知，中间状态不会推送。


**上传流程: **


1. 调用 <u>v2.media.init_video_upload</u> 初始化上传任务。
1. 通过 <u>v2.media.upload_video_part</u> 上传视频分片。
1. 调用 <u>v2.media.complete_video_upload</u> 完成上传。
1. 系统异步处理视频，并通过 <u>video_upload_result_push</u> 推送上传结果。
1. (可选) 调用 <u>v2.media.get_video_upload_result</u> 检查进度。
1. 上传成功后，获取 video_upload_id 以调用 Shopee Video API。


注意：

- 使用推送机制异步接收上传完成通知，以避免轮询。
- 每个上传任务对应一个唯一的视频；避免多次上传同一视频。
### 4. Shopee Video APIs


Shopee Video API 分为两个模块：视频管理以及数据表现。

#### 4.1 视频管理


1) <u>v2.video.get_cover_list</u>：获取已上传视频的逐帧截图，并选择特定帧作为视频封面。



2) <u>v2.video.edit_video_info</u>：在发布前设置或编辑视频信息，包括视频标题、封面、关联产品、发布时间以及是否允许合拍和剪辑等。



注意：草稿视频可以多次编辑；一旦发布，则无法编辑。



3) <u>v2.video.post_video</u>：将草稿视频发布到 Shopee Video，必须先上传视频并编辑其信息。



4) <u>v2.video.get_video_list</u>：获取账户下的视频列表。



5) <u>v2.video.get_video_detail</u>：获取视频的详细信息。



6) <u>v2.video.delete_video</u>：删除草稿或已发布的视频。

#### 4.2 数据表现


**所有视频的整体表现：**



1) <u>v2.video.get_overview_performance</u>: 获取所有已发布视频的整体内容互动与交易转化表现。



2) <u>v2.video.get_metric_trend</u>：查询所有已发布视频的整体内容互动与交易转化表现随时间变化的趋势。



3) <u>v2.video.get_user_demographics</u>：获取所有已发布视频的观众分布数据 (包括性别、年龄、地区、活跃时间，以及内容和商品偏好)。



4) <u>v2.video.get_product_performance_list</u>：获取关联视频的产品表现数据。



**单个视频的表现：**



1) <u>v2.video.get_video_performance_list</u>：获取单个视频的整体表现概览。



2）<u>v2.video.get_video_detail_performance</u>：获取单个视频的内容互动与交易转化表现。



3）<u>v2.video.get_video_detail_metric_trend</u>：获取单个视频的内容互动与交易转化表现随时间变化的趋势。



4）<u>v2.video.get_video_detail_audience_distribution</u>：获取单个视频的观众分布数据 (包括性别、年龄、地区、活跃时间，以及内容和商品偏好)。



5）<u>v2.video.get_video_detail_product_performance</u>：获取单个视频关联商品的交易转化表现，用于评估视频对商品销售与转化的影响。



注意：所有表现数据通常至少有一天的延迟。

### 5. 授权与鉴权 (User-type APIs)

Shopee Video API 是 User-type API，需要 user_id 和 access_token，其授权和鉴权逻辑与 Livestream API 相同，有以下要点：


- **授权角色区分**
  - 若授权对象为**卖家**，生成授权链接时需设置 **auth_type=seller**，授权成功后通过 v2.public.get_access_token 获取 access_token，**返回 shop_id + user_id**；
  - 若授权对象为**达人**，生成授权链接时需设置 **auth_type=user**，授权成功后通过 v2.public.get_access_token 获取 access_token，**仅返回 user_id**。
- **接口公共参数为 user_id**
  - 所有 Video 相关接口调用均**以 user_id 作为公共请求参数**，而非 shop_id；
  - 所有 Video 相关接口的签名需**基于 user_id 构造**。
- **Access Token 与 Refresh Token 管理**
  - **需为每个 user_id 管理独立的 access_token 与 refresh_token。**


详细的授权和认证流程，请参考<u>直播管理对接指引</u>。

### 6. 开发者对接注意事项

- 只有 **Shopee Video Management **类型的应用才能调用 Video OpenAPI，在对接前，请在控制台创建相应的应用类型。
- 在执行任何与 Video 相关的 API 操作之前，**必须在 Seller Center 同意 Shopee Video's Terms & Conditions**。
