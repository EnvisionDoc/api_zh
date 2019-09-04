# Search Asset Node

查询满足条件的资产。

## 请求格式

```
https://{apigw-address}/asset-tree-service/v2.1/asset-nodes?action=searchAsset
```

## 请求参数（URI）

| 名称          | 位置（Path/Query） | 是否必须 | 数据类型 | 描述      |
|---------------|------------------|----------|-----------|--------------|
| orgId         | Query            | true     | String    | 资产所属的组织ID。[如何获取orgId信息>>](/docs/api/zh_CN/latest/api_faqs#id-orgid-orgid)  |


## 请求参数（Body）


.. list-table::
   :widths: auto
   :header-rows: 1

   * - 名称
     - 是否必须
     - 数据类型
     - 描述
   * - expression
     - False
     - String
     - 查询表达式，目前支持的字段有 ``assetId``、``modelId``、``rootModelIds``、``name``、``attributes``、``tags``、``treeId``、``productKey``及``deviceKey``。

       + ``assetId``、``modelId``、``rootModelIds``：支持in和=算术运算符；
       + ``productKey`` 及 ``deviceKey``：支持like模糊查询，支持=运算符；
       + ``name``：支持指定语言模糊查询：

         * ``name like ‘xxx’``：模糊查询default、中文和英文名称
         * ``name.default like ‘xxx’``：模糊查询默认名称
         * ``name.zh_CN like ‘xxx’``：模糊查询中文名称，不存在中文名称时模糊查询default名称
         * ``name.en_US like ‘xxx’``：模糊查询英文名称，不存在英文名称时模糊查询default名称

       `如何使用查询表达式>> </docs/api/zh_CN/latest/api_faqs.html#id1>`__

   * - pagination
     - False
     - pagination请求结构体
     - 随机分页。如未指定，默认分页大小是10。`Pagination请求结构体>> </docs/api/zh_CN/latest/overview.html?highlight=pagination#pagination>`__
   * - projection
     - False
     - Projection结构体
     - 用于在接口请求中描述待返回的对象projection。详见 `参数如何对结果集做裁剪>> </docs/api/zh_CN/latest/api_faqs.html#projection>`__



## 响应参数

| 名称 |数据类型  | 描述 |
|-----------|------------------|------------------|
| data      | Asset结构体Array |  asset的列表    |




## 示例 1

### 请求示例

```
https://{apigw-address}/asset-tree-service/v2.1/asset-nodes?action=searchAsset&orgId=1c499110e8800000
{
"projection": ["attributes", "assetId", "name"]
}
```

### 返回示例

```json
{
    "code": 0,
    "msg": "OK",
    "requestId": "cf08e75c-325a-429f-bdb9-ec5d6a1250d7",
    "pagination": {
       "pageNo": 1,
       "pageSize": 10,
       "totalSzie": 10,
       "sortedBy": null
    },
    "data": [{
       "assetId": "f1Y6KiOr",
       "name": {
           "i18nValue": {},
           "defaultValue": "earth"
       },
       "attributes": {
           "starsystem": "Solar System",
           "de001": 123
       }
    }, {
       "assetId": "WHIFQDEZ",
       "name": {
           "i18nValue": {},
           "defaultValue": "earth"
       },
       "attributes": {
           "starsystem": "Solar System",
           "de001": 123
       }
    }, {
       "assetId": "TdqGOisO",
       "name": {
           "i18nValue": {},
           "defaultValue": "earth"
       },
       "attributes": {
           "starsystem": "Solar System",
           "de001": 123
       }
    }, {
       "assetId": "T9VewFFA",
       "name": {
           "i18nValue": {},
           "defaultValue": "venus"
       },
       "attributes": {
           "starsystem": "Solar System",
           "de001": 123
       }
    }, {
       "assetId": "NU3EbpXK",
       "name": {
           "i18nValue": {},
           "defaultValue": "1559140566137"
       },
       "attributes": {
           "starsystem": "Solar System",
           "de001": 123
       }
    }, {
       "assetId": "9AE1XYBl",
       "name": {
           "i18nValue": {},
           "defaultValue": "earth"
       },
       "attributes": {
           "starsystem": "Solar System",
           "de001": 123
       }
    }, {
       "assetId": "ZPuCIbDw",
       "name": {
           "i18nValue": {},
           "defaultValue": "earth"
       },
       "attributes": {
           "starsystem": "Solar System",
           "de001": 123
       }
    }]
}
```

