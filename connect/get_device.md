# Get Device

获取设备信息。

## 请求格式

```
https://{apigw-address}/connect-service/v2.1/devices?action=get
```

## 请求参数（URI）

.. note:: 以下非必须字段中，必须提供 ``assetId`` 或 ``productKey`` + ``deviceKey`` 的组合，用于指定设备。

>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>

| 名称          | 位置（Path/Query） | 是否必须 | 数据类型 | 描述      |
|---------------|------------------|----------|-----------|--------------|
| orgId         | Query            | True     | String    | 资产所属的组织ID。[如何获取orgId信息>>](/docs/api/zh_CN/latest/api_faqs#id-orgid-orgid)                |
| assetId  | Query            | False   | String         | 资产ID。[如何获取Asset ID信息>>](/docs/api/zh_CN/latest/api_faqs.html#asset-id-assetid-assetid) |
| productKey | Query          | False       | String       | Product Key      |
| deviceKey | Query           | False      | String       | Device Key          |
    

## 响应参数

| 名称 | 数据类型 | 描述         |
|-------------|-------------------|-----------------------------|
| data |    Device结构体        | 网关设备信息，见[Device结构体](/docs/api/zh_CN/latest/connect/get_device.html#id3)。 |


### Device结构体

| 名称 | 数据类型 | 描述         |
|------------------|-----------------------|----------------------------|
| orgId |  String | 资产所属的组织ID |
| assetId  | String         | 资产ID|
| modelId             | String                          | 资产所属模型ID|
| modelIdPath      | String                            | 模型ID的路径                                                               |
| productKey       | String                            | Product Key                                                                |
| productName      | StringI18n                        | 产品名称                                                                |
| productType      | String                            | 产品类型                                                                   |
| dataFormat       | String                            | 数据格式。Custom表示支持用户自定义数据格式，Json表示只支持EnOS设备协议格式 |
| deviceKey        | String                            | Device Key                                                                    |
| deviceName       | StringI18n                        | 设备名称                                                                   |
| deviceSecret     | String                            | 设备的连接秘钥                                                             |
| deviceDesc       | String                            | 设备描述                                                                   |
| timezone         | String                            | 设备所在时区                                                               |
| deviceAttributes | Map（Key为String，Value为String） | 设备的属性                                                                 |
| deviceTags       | Map（Key为String，Value为String） | 设备的标志                                                                 |
| createTime       | Long                              | 设备的创建时间                                                             |
| status           | String                            | 设备的状态（online、offline、inactive或disable）                         |
| activeTime       | Long                              | 设备的激活时间                                                             |
| lastOnlineTime   | Long                              | 设备最后一次上线时间                                                       |
| lastOfflineTime  | Long                              | 设备最后一次离线时间                                                       |
| measurepointLastUpdate  | Long                              | 设备测点最近一次更新的时间                                                       |
| eventLastUpdate  | Long                              | 设备事件最近一次更新的时间                                                       |
| attributeLastUpdate  | Long                              | 设备属性最近一次更新的时间                                                       |
| featureLastUpdate  | Long                              | 设备最近一次更新的时间，以上述三个时间（`measurepointLastUpdate`、`eventLastUpdate`、`attributeLastUpdate`）里最近的时间为准 |




## 示例 1

### 请求示例

```
url:https://{apigw-address}/connect-service/v2.1/devices?action=get&orgId=o15475450989191&assetId=9HhK0YxX
method: GET
headers: {}
requestBody: null
```

### 返回示例

```json
responseBody: {
	"code": 0,
	"msg": "OK",
	"requestId": "835a5cc4-4487-4bf2-961a-55bc0ee77d02",
	"data": {
		"orgId": "yourOrgId",
		"assetId": "9HhK0YxX",
		"modelId": "abc-test",
		"modelIdPath": "/abc-test",
		"productKey": "yourProductKey",
		"productName": {
			"defaultValue": "abc-pk",
			"i18nValue": {}
		},
		"productType": "Device",
		"dataFormat": "Json",
		"deviceKey": "yourDeviceKey",
		"deviceName": {
			"defaultValue": "testforname",
			"i18nValue": {}
		},
		"deviceSecret": "yourDeviceSecret",
		"deviceDesc": "test for undatedevice",
		"timezone": "+08:00",
		"deviceAttributes": {
			"int11": 617
		},
		"deviceTags": {
			"test": "test for tags"
		},
		"createTime": 1557905107199,
		"status": "offline",
		"activeTime": 1557909526473,
		"lastOnlineTime": 1560743931658,
		"lastOfflineTime": 1560744111658,
		"measurepointLastUpdate":1565875705704,
		"eventLastUpdate":1565875705856,
		"attributeLastUpdate":1547793776699,
		"featureLastUpdate":1565875705856
	}
}
```

