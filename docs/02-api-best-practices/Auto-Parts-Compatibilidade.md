# 汽车配件：汽车零部件兼容性

> 来源: [Shopee Open Platform](https://open.shopee.com/developer-guide/378)
> 分类: API Best Practices


自 2024 年 6 月 24 日起，Shopee 推出了允许添加车辆与汽车零部件产品之间兼容性的功能。为此，新增了一些端点，并对其他端点进行了相关更新。

#### **使用兼容性功能的优势**

- 卖家可以配置更完整的商品，包含与其产品兼容的车辆数据；
- 填写了兼容性信息的商品将在买家搜索结果页面 (SRP) 中获得更高的展示权重；
- 买家在购买时将更有信心，因为更容易确认商品是否与其车辆兼容。

考虑到这一情况，如果您的客户（卖家）经营汽车零部件商品，我们强烈建议您在您的平台上实施新的端点。

#### **数据结构**


车辆数据按以下方式存储：

| 参数 | 含义 | 示例 |
| --- | --- | --- |
| brand_id | 特定品牌的 ID | 5770 |
| brand_name | 与每个 brand_id 相关的品牌名称 | "Chevrolet" |
| model_id | 特定车型的 ID | 5905 |
| model_name | 与 model_id 相关的车型名称 | "Chevette" |
| year_id | 每个年份的 ID | 5712 |
| year_name | 与给定 year_id 相关的年份 | "1979" |
| version_id | 车辆每个版本的 ID | 5907 |
| version_name | 与 version_id 相关的版本名称 | "Hatch" |

需要强调的是，上述参数遵循以下依赖关系：brand > model > year > version。

#### **新增端点：**


**v2.product.get_all_vehicle_list**


- 顾名思义，此端点负责返回 Shopee 数据库中的完整车辆列表。使用时，必填参数是页面大小 (page_size)，最多为 100 项。有关该端点的更多详细信息，请参阅 API Reference 页面。
- 端点返回示例：

```python
{ "error": "", "message": "", "warning": "", "request_id": "6535ecb33a3f8c6900c8d2b515f3c821", "response": { "vehicle_list": [ { "brand_id": 5770, "brand_name": "Chevrolet", "model_id": 5905, "model_name": "Chevette", "year_id": 5712, "year_name": "1979", "version_id": 5907, "version_name": "Hatch" }, { "brand_id": 5770, "brand_name": "Chevrolet", "model_id": 5905, "model_name": "Chevette", "year_id": 5712, "year_name": "1979", "version_id": 5906, "version_name": "S" }.... ], "has_next_page": true, "next_offset": 61 }}
```


**v2.product.get_vehicle_list_by_compatibility_detail**


- 通过此端点可以识别车辆每个元素（品牌/车型/年份/版本）的详细信息。必填参数是 "compatibility_details"，您可以在此指定所需的详细程度。可选参数 (brand_id / model_id / year_id / version_id) 有助于细化搜索。更多信息请参见其 API Reference 页面。
- 端点调用示例：
|**Request**|**Response**|
| --- | --- |
|**compatibility_details**="Brand" | "response": { "compatibility_tree": [ { "compatibility_details": [ { "brand_id": 12345, "brand_name": "Toyota", }, { "brand_id": 13524, "brand_name": "Renault", }, { "brand_id": 14235, "brand_name": "Chevrolet", }, … |
|**compatibility_brand_id**=12345&**compatibility_details**="Model" | "response": { "compatibility_tree": [ { "compatibility_details": [ { "model_id": 222234, "model_name": "Etios", }, { "model_id": 234234, "model_name": "Corolla", }, { "model_id": 225243, "model_name": "Bandeirante", }, … |
#### 现有端点的变更


一些端点已进行调整以适应兼容性流程，具体如下：

- V2.product.add_item;
- V2.product.update_item;
- v2.product.get_item_base_info;

在前两个端点中，可以分别为新商品/现有商品插入兼容性信息。第三个端点的变更有助于确认兼容性信息是否正确添加。

v2.product.add_item 和 v2.product.update_item 的调用结构示例


```python
 "compatibility_info": { "vehicle_info_list": [ { "brand_id": 5770, "model_id": 5911, "year_id": 5590, "version_id": 5912 }, { "brand_id": 5508, "model_id": 5509, "year_id": 5516 }, { "brand_id": 5770, "model_id": 5905 } ] },
```


 

一些重要注意事项：

- 如果某个产品与特定年份的所有版本兼容，只需提供 brand、model 和 year 的 ID，系统将自动将该年份的所有版本添加到兼容性列表中；

```python
		{ "brand_id": 5508, "model_id": 5509, "year_id": 5516 }
```


- 类似地，如果某个车型所有年份的所有版本都与产品兼容，只需提供 brand 和 model 的 ID；

```python
 { "brand_id": 5770, "model_id": 5905 }
```


- v2.product.update_item 可正常用于向尚无兼容性信息的现有商品添加兼容性信息。在这种情况下，只需按照上述示例提供兼容性列表即可；

-**注意：**使用 v2.product.update_item**向已在其列表中包含车辆的商品添加兼容性信息时**，您必须提供该商品当前已有的 ID 列表加上新的兼容性 ID。否则，现有的 ID 列表将被 update item 调用中提供的新 ID 覆盖。


如果对使用新端点有任何疑问，请提交 ticket，我们将协助您正确集成新功能。
