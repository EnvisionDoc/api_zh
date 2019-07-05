# Remove Sub-Device

将子设备从网关下移除（解除拓扑关系）。

## 请求格式

```
https://{apigw-address}/connect-service/v2.1/device-topos?action=removeSubDevice
```

## 请求参数（URI）

| 名称          | 位置（Path/Query） | 是否必须 | 数据类型 | 描述      |
|---------------|------------------|----------|-----------|--------------|
| orgId         | Query            | true     | String    | 资产所属的组织ID。[如何获取orgId信息](/docs/api/zh_CN/latest/api_faqs#id-orgid-orgid)                |


## 请求参数（Body）

| 名称          | 是否必须 | 数据类型 | 描述      |
|--------------------|----------|-----------|--------------|
| gateway | True      |DeviceIdentfier结构体  | 需要添加子设备的网关信息，见[DeviceIdentfier结构体](/docs/api/zh_CN/latest/connect/remove_sub_device.html#deviceidentifier) |
| subDevices           | True      | DeviceIdentfier结构体  | 需要添加到指定网关的子设备列表信息，见[DeviceIdentfier结构体](/docs/api/zh_CN/latest/connect/remove_sub_device.html#deviceidentifier) |


### DeviceIdentifier结构体

注：以下字段必须提供`assetId`或者`(productKey, deviceKey)`。

| 名称      | 数据类型 |描述|
|----------------|----------------|------------------|
| assetId  | String         | 资产ID，支持查询多个资产，多个资产ID之间用英文逗号隔开。[如何获取assetId信息](/docs/api/zh_CN/latest/api_faqs.html#asset-id-assetid-assetid)|
| productKey | String         | Product Key      |
| deviceKey | String         | 设备key          |




## 响应参数

| 名称| 数据类型 | 描述         |
|-------------|-----------------------------------|-----------------------------|
| data | String                           | （空）               |


## 错误码

| 代码| 数据类型 | 描述         |
|-------------|-----------------------------------|-----------------------------|
| 11738 |                | 参数gateway不是网关设备                |
| 11795 |                | 提供的子设备存在已有拓扑或为网关      |


## 示例 1

### 请求示例

```
url:https://{apigw-address}/connect-service/v2.1/device-topos?action=remove&orgId=o15475450989191
 method: POST
requestBody: {"subDevices":[{"assetId":"gVRwKQ3C"}],"gateway":{"assetId":"J1Rqyaqz"}}
```

### 返回示例

```json
responseBody:{"code":0,"msg":"OK","requestId":"ea6608bb-b8cb-46f3-a836-ee24ea9a028c","data":null}
```

