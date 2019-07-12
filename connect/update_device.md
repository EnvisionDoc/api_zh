# Update Device

更新设备。更新模式采用`IsPathcUpdate`为true，`assetId`（或`productKey`和`deviceKey`）为请求字段，其他字段为更新字段。

## 请求格式

```
https://{apigw-address}/connect-service/v2.1/devices?action=update
```

## 请求参数（URI）

注：以下非必须字段中，必须提供`assetId`或`productKey`与`deviceKey`的组合，用于指定设备。

| 名称          | 位置（Path/Query） | 是否必须 | 数据类型 | 描述      |
|---------------|------------------|----------|-----------|--------------|
| orgId         | Query            | True     | String    | 资产所属的组织ID。[如何获取orgId信息](/docs/api/zh_CN/latest/api_faqs#id-orgid-orgid)                |
| assetId  | Query          | False      | String        | 资产ID。[如何获取Asset ID信息](/docs/api/zh_CN/latest/api_faqs.html#asset-id-assetid-assetid) |
| productKey | Query         | False      | String         | Product Key      |
| deviceKey | Query         | False     | String          | 设备key          |


## 请求参数（Body）

| 名称          | 是否必须 | 数据类型 | 描述      |
|----------------|---------------|--------------------------|---|
|timezone | True          | String         | 欲更新的设备所在时区     |
| deviceName | True          | StringI18n | 欲更新的设备名称         |
| deviceAttributes | False         | Map       | 欲更新的设备属性         |
| deviceTags   | False         | Map（key为String，value为String）    | 欲更新的设备tags |
| deviceDesc  | False         | String    | 欲更新的设备描述信息     |




## 响应参数

| 名称 | 数据类型 | 描述         |
|-------------|-------------------|-----------------------------|
| data |    String        | （空） |





## 示例 1

### 请求示例

```
url:https://{apigw-address}/connect-service/v2.1/devices?action=update&orgId=o15475450989191&assetId=9HhK0YxX
method: POST
requestBody: {
	"deviceTags": {
		"test": "test for tags"
	},
	"deviceAttributes": {
		"int11": 617
	},
	"deviceName": {
		"defaultValue": "testforname",
		"i18nValue": {}
	}
	"deviceDesc": "test for updatedevice"
}
```

### 返回示例

```json
responseBody: {
	"code": 0,
	"msg": "OK",
	"requestId": "0d61752e-0633-4846-abb1-b6fb39801a5f",
	"data": ""
}
```

