# Search Sub-Device

搜索网关下的子设备信息。

## 请求格式

```
https://{apigw-address}/connect-service/v2.1/device-topos?action=searchSubDevice
```

## 请求参数（URI）

| 名称          | 位置（Path/Query） | 是否必须 | 数据类型 | 描述      |
|---------------|------------------|----------|-----------|--------------|
| orgId         | Query            | true     | String    | 资产所属的组织ID。[如何获取orgId信息>>](/docs/api/zh_CN/latest/api_faqs#id-orgid-orgid)                |


## 请求参数（Body）

| 名称          | 是否必须 | 数据类型 | 描述      |
|--------------------|----------|-----------|--------------|
| gateway | True      | DeviceIdentfier结构体 | 需要添加子设备的网关信息，见[DeviceIdentfier结构体>>](/docs/api/zh_CN/latest/connect/search_sub_device.html#deviceidentifier) |
| pagination  | False      | Pagination请求结构体  | 分页参数。如未指定，默认每页10条。见[Pagination请求结构体>>](/docs/api/zh_CN/latest/overview.html?highlight=pagination#pagination) |


### DeviceIdentifier结构体

.. note:: 以下非必须字段中，必须提供 ``assetId`` 或 ``productKey`` + ``deviceKey`` 的组合，用于指定设备。

>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>


| 名称      | 数据类型 |描述|
|----------------|----------------|------------------|
| assetId  | String         | 资产ID。[如何获取Asset ID信息>>](/docs/api/zh_CN/latest/api_faqs.html#asset-id-assetid-assetid) |
| productKey | String         | Product Key      |
| deviceKey | String         | Device Key          |




## 响应参数

| 名称| 数据类型 | 描述         |
|-------------|-----------------------------------|-----------------------------|
| data | Device结构体                     | 网关下指定分页的一组子设备信息，见[Device结构体](/docs/api/zh_CN/latest/connect/search_sub_device.html#id3)。    |


### Device结构体

| 名称| 数据类型 | 描述         |
|------------------|--------------------|-------|
| orgId            | String                            | 资产所属的组织ID|
| assetId  | String         | 资产ID|
| modelId             | String                          | 资产所属模型ID|
| modelIdPath      | String                            | 模型ID的路径                                                               |
| productKey       | String                            | Product Key                                                                |
| productName      | StringI18n                        | 产品名称                                                                |
| productType      | String                            | 产品类型                                                                   |
| dataFormat       | String                            | 数据格式。Custom表示支持用户自定义数据格式，Json表示只支持EnOS设备协议格式。 |
| deviceKey        | String                            | Device Key                                                                    |
| deviceName       | StringI18n                        | 设备名称                                                                   |
| deviceSecret     | String                            | 设备的连接秘钥                                                             |
| deviceDesc       | String                            | 设备描述                                                                   |
| timezone         | String                            | 设备所在时区                                                               |
| deviceAttributes | Map（Key为String，Value为String） | 设备的属性                                                                 |
| deviceTags       | Map（Key为String，Value为String） | 设备的标志                                                                 |
| createTime       | Long                              | 设备的创建时间                                                             |
| status           | String                            | 设备的状态（online, offline, inactive 或 disable）                         |
| activeTime       | Long                              | 设备的激活时间                                                             |
| lastOnlineTime   | Long                              | 设备最后一次上线时间                                                       |
| lastOfflineTime  | Long                              | 设备最后一次离线时间                                                       |



## 错误码

| 代码| 数据类型 | 描述         |
|-------------|-----------------------------------|-----------------------------|
| 11738 |                | 参数gateway指定的设备不是网关                |


## 示例 1

### 请求示例

```
url:https://{apigw-address}/connect-service/v2.1/device-topos?action=searchSubDevices&orgId=o15475450989191
method: POST
requestBody: {"gateway":{"assetId":"J1Rqyaqz"}}
```

### 返回示例

```json
responseBody: {
		"code": 0,
		"msg": "OK",
		"requestId": "498d1c5b-7c4f-401a-a9ff-9072931bec2e",
		"data": [{
			"orgId": "yourOrgId",
			"assetId": "mAEsF3sm",
			"modelId": "AlterTest0617",
			"modelIdPath": "/AlterTest0617",
			"productKey": "yourProductKey",
			"productName": {
				"defaultValue": "AlterTest0617_Product",
				"i18nValue": {}
			},
			"productType": "Device",
			"dataFormat": "Json",
			"deviceKey": "yourDeviceKey",
			"deviceName": {
				"defaultValue": "testforCreatedevice",
				"i18nValue": {}
			},
			"deviceSecret": "yourDeviceSecret",
			"deviceDesc": "test for createdevice",
			"timezone": "+08:00",
			"deviceAttributes": {
				"testatt": 111111
			},
			"deviceTags": {},
			"createTime": 1560755091998,
			"status": "inactive",
			"activeTime": 0,
			"lastOnlineTime": 0,
			"lastOfflineTime": 0
		}, {
			"orgId": "yourOrgId",
			"assetId": "gVRwKQ3C",
			"modelId": "AlterTest0617",
			"modelIdPath": "/AlterTest0617",
			"productKey": "yourProductKey",
			"productName": {
				"defaultValue": "AlterTest0617_Product",
				"i18nValue": {}
			},
			"productType": "Device",
			"dataFormat": "Json",
			"deviceKey": "yourDeviceKey",
			"deviceName": {
				"defaultValue": "AlterTest0617_Product",
				"i18nValue": {}
			},
			"deviceSecret": "yourDeviceSecret",
			"deviceDesc": null,
			"timezone": "+10:00",
			"deviceAttributes": {},
			"deviceTags": {},
			"createTime": 1560730295671,
			"status": "offline",
			"activeTime": 1560730567958,
			"lastOnlineTime": 1560743932166,
			"lastOfflineTime": 1560744112166
		}],
		"pagination":{"sortedBy":null,"pageNo":1,"pageSize":2,"totalSize":2}}
```

