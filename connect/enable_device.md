# Enable Device

启用设备。

## 请求格式

```
https://{apigw-address}/connect-service/v2.1/devices?action=enable
```

## 请求参数（URI）

注：以下非必须字段中，必须提供`assetId`或`productKey`与`deviceKey`的组合，用于指定设备。

| 名称          | 位置（Path/Query） | 是否必须 | 数据类型 | 描述      |
|---------------|------------------|----------|-----------|--------------|
| orgId         | Query            | True     | String    | 资产所属的组织ID。[如何获取orgId信息](/docs/api/zh_CN/latest/api_faqs#id-orgid-orgid)                |
| assetId  | Query          | False      | String        | 资产ID，支持查询多个资产，多个资产ID之间用英文逗号隔开。[如何获取Asset ID信息](/docs/api/zh_CN/latest/api_faqs.html#asset-id-assetid-assetid) |
| productKey | Query         | False      | String         | Product Key      |
| deviceKey | Query         | False     | String          | 设备key          |
    


## 错误码

| 代码| 数据类型 | 描述         |
|-------------|-----------------------------------|-----------------------------|
| 11794 |                | 要启用的设备已处于激活状态             |


## 示例 1

### 请求示例

```
url:https://{apigw-address}/connect-service/v2.1/devices?action=enable&orgId=o15475450989191&assetId=9HhK0YxX
method: POST
```

### 返回示例

```json
responseBody: {
	"code": 0,
	"msg": "OK",
	"requestId": "06dd8ea3-cb9e-4628-8f93-d36c416bcd3a",
	"data": null
}
```

