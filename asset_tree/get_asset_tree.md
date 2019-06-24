# Get Asset Tree

获取指定OU下的一棵资产树。

## 请求格式

```
https://apigw-address/asset-tree-service/v2.1/asset-trees?action=get
```

## 请求参数（URI）

| 名称          | 位置（Path/Query） | 是否必须 | 数据类型 | 描述      |
|---------------|------------------|----------|-----------|--------------|
| orgId         | Query            | true     | String    | 资产所属的组织ID。[如何获取orgId信息](/docs/api/zh_CN/latest/api_faqs#orgid-orgid)                |
| treeId        | Query            | true    | String    | 需要获取的资产树ID。[如何获取资产树信息ID](/docs/api/zh_CN/latest/api_faqs#id)        |


## 响应参数

| 名称| 数据类型 | 描述         |
|-------------|-----------------------------------|-----------------------------|
| treeId| String                            | 资产树ID                    |
| tags| Map（Key为String，Value为String） | 用户自定义的一组资产树标签  |
| asset| [asset结构体](#assetstruc)                       | 资产树的根资产              |

### Asset结构体<assetstruc>

| 名称  |  数据类型      | 描述               |
|-------|-------|---------------------------|
| assetId |  String | 资产ID，支持查询多个资产，多个资产ID之间用英文逗号隔开。[如何获取assetId信息](/docs/api/zh_CN/latest/api_faqs.html#assetid-assetid)|
|modelId|String|资产所属模型ID。[如何获取modelId信息](/docs/api/zh_CN/latest/api_faqs.html#modeid-modeid)|
|modelIdPath|String|modelIdPath路径。|
| name | StringI18n |支持国际化的资产名称。结构请见[国际化名称结构体](/docs/api/zh_CN/latest/api_faqs.html#id3) |
|timezone  |  String  |资产所属时区。<br>使用+08:00格式表示不支持夏令时的时区。<br>使用Asia/Shanghai格式表示支持夏令时的时区。<br>详情请见[时区表示方法](http://www.envisioniot.com/docs/api/zh_CN/latest/api_faqs.html#id4) |
| description | String | 资产描述|
| label  | String | 资产类型：“0”表示设备资产，“1”表示逻辑资产|
| inValid  | Boolean | true为无效节点，false为有效节点|
|attributes   |Map（Key为String，Value为Object）  |资产所属的模型属性。<br>`Key`为属性id，String类型。Value的类型取决于模型中这个属性的定义。详情请见 [attributes的表示方法](/docs/api/zh_CN/latest/api_faqs.html#attributes) |
|tags|Map<br>（Key为String, Value为String）|用户自定义标签，详情请见[标签的作用与表示方法](http://www.envisioniot.com/docs/api/zh_CN/latest/api_faqs.html#id6)|



## 示例 1

### 请求示例

```
GET
https://apigw-address/asset-tree-service/v2.1/asset-trees?treeId=BRIt3ee3&action=get&orgId=o15541858646501
```

### 返回示例

```json
{
 "code": 0,
 "msg": "OK",
 "requestId": "f3c1ffc7-cc8e-4a50-ad40-0fa7b0c3a7ac",
 "data": {
  "treeId": "BRIt3ee3",
  "tags": {
   "user": "zm",
   "user0": "lily"
  },
  "asset": {
   "inValid": false,
   "assetId": "nlw68lR5",
   "modelId": "model_0422",
   "modelIdPath": "/model_0422",
   "name": {
    "defaultValue": "0430343",
    "i18nValue": {
     "en_US": "0430343"
    }
   },
   "timezone": "+08:00",
   "description": null,
   "label": "1",
   "attributes": {},
   "tags": {
    "tree": "0430"
   }
  }
 }
}
```

