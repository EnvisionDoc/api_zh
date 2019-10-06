# Cancel Command

取消缓存命令的接口。如果有`commandId`，则取消单个命令，如果无`commandId`，则取消该设备的所有缓存命令。

## 请求格式

```
https://{apigw-address}/connect-service/v2.1/commands?action=cancel
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
| commandId | Query            | False    | String        | 命令ID          |


## 响应参数

| 名称| 数据类型 | 描述         |
|-------------|-------------------|-----------------------------|
| data |    getCommand结构体        | 被取消的命令列表。参见[Command结构体>>](/docs/api/zh_CN/latest/connect/get_command.html#command-com) |




## 示例 1

### 请求示例

```
url:https://{apigw-address}/connect-service/v2.1/commands?action=cancel&deviceKey=mqtt_01&productKey=bXuuAiku&orgId=o15541858646501
method: POST
```

### 返回示例

```json
{
    "code": 0,
    "msg": "Success",
    "submsg": null,
    "requestId": "7d863d517eae4f18a2776452eb1305bb",
    "data": [{
        "commandId": "2278935391225618432",
        "orgId": "yourOrgId",
        "productKey": "yourProductKey",
        "deviceKey": "yourDeviceKey",
        "assetId": "oxWwM9i5",
        "createTime": 1560505243577,
        "createLocalTime": 1560505243577,
        "commandType": 1,
        "commandName": {
            "defaultValue": "Int_value",
            "i18nValue": {
                "en_US": "Int_value"
            }
        },
        "timeout": 1,
        "pendingTtl": 6000,
        "state": 1,
        "tslIdentifier": "Int_value",
        "inputData": 222
    }]
}
```

