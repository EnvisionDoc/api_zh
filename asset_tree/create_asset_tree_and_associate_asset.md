# Create Asset Tree and Associate Asset

创建一个资产树，并关联一个已有的资产（设备资产或逻辑资产）作为其根节点。

## 请求格式

```
https://{apigw-address}/asset-tree-service/v2.1/asset-trees?action=associate
```

## 请求参数（URI）

.. note:: 以下非必须字段中，必须提供 ``assetId`` 或 ``productKey`` + ``deviceKey`` 的组合，用于指定设备。

>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>

| 名称 | 位置（Path/Query） | 是否必须 | 数据类型 | 描述      |
|---------------|------------------|----------|-----------|--------------|
| orgId      | Query              | true     | String   | 资产所属的组织ID。[如何获取orgId信息>>](/docs/api/zh_CN/latest/api_faqs#id-orgid-orgid)|
| assetId    | Query              | false    | String   | 待关联的资产ID：<br>如指定`assetId`，则关联由`assetId`唯一识别的资产。[如何获取Asset ID信息>>](/docs/api/zh_CN/latest/api_faqs.html#asset-id-assetid-assetid)<br>如未指定`assetId`，则关联以`productKey`与`deviceKey`组合唯一识别的资产。 |
| productKey | Query              | false    | String   | 待关联设备的Product Key|
| deviceKey  | Query              | false    | String   | 待关联设备的Device Key |


## 响应参数

| 名称 | 数据类型 | 描述               |
|:-----|:---------|:-------------------|
| data | String   | 创建成功的资产树ID |


## 示例 1

### 请求示例

```
https://{apigw-address}/asset-tree-service/v2.1/asset-trees?action=associate&orgId=yourOrgId&assetId=N5VpI5f9
```

### 返回示例

```json
{
    "code": 0,
    "msg": "OK",
    "requestId": "01b5477a-374e-49a0-8b68-7dbfe8f0b74f",
    "data": "cRUdS7sJ"
}
```
