# Disable Device

禁用设备。

## 请求格式

```
https://{apigw-address}/connect-service/v2.1/devices?action=disable
```

## 请求参数（URI）

.. note:: 以下非必须字段中，必须提供assetId或productKey与deviceKey的组合，用于指定设备。

| 名称          | 位置（Path/Query） | 是否必须 | 数据类型 | 描述      |
|---------------|------------------|----------|-----------|--------------|
| orgId         | Query            | True     | String    | 资产所属的组织ID。[如何获取orgId信息](/docs/api/zh_CN/latest/api_faqs#id-orgid-orgid)                |
| assetId  | Query          | False      | String        | 资产ID。[如何获取Asset ID信息](/docs/api/zh_CN/latest/api_faqs.html#asset-id-assetid-assetid) |
| productKey | Query         | False      | String         | Product Key标识符      |
| deviceKey | Query         | False     | String          | Device Key标识符          |
    


## 错误码

| 代码| 数据类型 | 描述         |
|-------------|-----------------------------------|-----------------------------|
| 11794 |                | 要禁止的设备已处于禁用状态                |


## 示例 1

### 请求示例

```
url:https://{apigw-address}/connect-service/v2.1/devices?action=disable&orgId=o15475450989191&assetId=9HhK0YxX
method: POST
```

### 返回示例

```json
responseBody: {
	"code": 0,
	"msg": "OK",
	"requestId": "b3f22f9b-d90d-4bf2-9e97-79162a3d1dff",
	"data": null
}
```

