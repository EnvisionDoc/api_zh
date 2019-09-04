# Create Asset Tree

创建一棵资产树，并同时创建该资产树的根节点。

## 请求格式

```
https://{apigw-address}/asset-tree-service/v2.1/asset-trees?action=create
```

## 请求参数（URI）

| 名称          | 位置（Path/Query） | 是否必须 | 数据类型 | 描述      |
|---------------|------------------|----------|-----------|--------------|
| orgId         | Query            | true     | String    | 资产所属的组织ID。[如何获取orgId信息>>](/docs/api/zh_CN/latest/api_faqs#id-orgid-orgid)                |



## 请求参数（Body）

| 名称| 是否必须| 数据类型 | 描述         |
|-------------|---------------|--------------------|-----------------------------|
| asset| true  |  Asset结构体                   | 创建根节点资产所需的详情，见[Asset结构体>>](create_asset_tree.html#asset-assetstruc) |

### Asset结构体 <assetstruc>

| 名称  | 是否必须  |  数据类型      | 描述    |
|-------|-------|-------------|--------------|
|modelId|true|String|资产所属模型ID。[如何获取modelId信息>>](/docs/api/zh_CN/latest/api_faqs.html#modelid-modelid)|
| name |true| StringI18n |支持国际化的资产名称。结构请见[国际化名称结构体>>](/docs/api/zh_CN/latest/api_faqs.html#id3) |
|timezone  |true|  String  |资产所属时区。<br>使用+08:00格式表示不支持夏令时的时区。<br>使用Asia/Shanghai格式表示支持夏令时的时区。<br>详情请见[时区表示方法>>](/docs/api/zh_CN/latest/api_faqs.html#id4) |
|description |false|String|资产描述 |
|attributes  |false  |Map（Key为String，Value为Object）  |资产所属的模型属性。详情请见[attributes的表示方法>>](/docs/api/zh_CN/latest/api_faqs.html#attributes) |
|tags |false|Tag结构体|用户自定义标签，详情请见[标签的作用与表示方法>>](/docs/api/zh_CN/latest/api_faqs.html#id6)|


## 响应参数

| 名称 | 数据类型| 描述       |
|----------|--------------|----------------|
| data     | String       | 创建的资产树ID。 |



## 示例 1

### 请求示例

```
POST
https://{apigw-address}/asset-tree-service /v2.1/asset-trees?action=create&orgId=yourOrgId

{"asset":{
    "modelId": "eeeewqqw",
    "name": {
        "defaultValue": "hahah"
    },
    "timezone": "+12:00",
    "attributes":{},
    "description": "test example by tj"
}
}
```

### 返回示例

```json
{
  "msg":  "OK",
  "code": 0,
  "data": "HfzFPn1H",
  "requestId": "bb4f8c40-604a-451e-83bd-99cfba6bd53e"
}
```

