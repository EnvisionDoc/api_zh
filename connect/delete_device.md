# Delete Device

删除设备。

## 请求格式

```
https://{apigw-address}/connect-service/v2.1/devices?action=delete
```

## 请求参数（URI）

注：以下非必须字段中，必须提供`assetId`或`productKey`与`deviceKey`的组合，用于指定设备。

| 名称          | 位置（Path/Query） | 是否必须 | 数据类型 | 描述      |
|---------------|------------------|----------|-----------|--------------|
| orgId         | Query            | True     | String    | 资产所属的组织ID。[如何获取orgId信息](/docs/api/zh_CN/latest/api_faqs#id-orgid-orgid)                |
| assetId  | Query            | False   | String         | 资产ID。[如何获取Asset ID信息](/docs/api/zh_CN/latest/api_faqs.html#asset-id-assetid-assetid) |
| productKey | Query          | False       | String       | Product Key标识符      |
| deviceKey | Query           | False      | String       | Device Key标识符          |




## 示例 1

### 请求示例

```
url:https://{apigw-address}/connect-service/v2.1/devices?action=delete&orgId=o15475450989191&assetId=mAEsF3sm
method: POST
headers: {}
requestBody: null
```

### 返回示例

```json
responseBody:{
"code":0,
"msg":"OK",
"requestId":"12d7e3be-6bac-43de-8733-7e02a4eb8a88",
"data":null
}
```

