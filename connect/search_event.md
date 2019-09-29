# Search Event

按条件分页搜索事件。

## 请求格式

```
https://{apigw-address}/connect-service/v2.1/events?action=search
```

## 请求参数（URI）

| 名称          | 位置（Path/Query） | 是否必须 | 数据类型 | 描述      |
|---------------|------------------|----------|-----------|--------------|
| orgId         | Query            | True     | String    | 资产所属的组织ID。[如何获取orgId信息>>](/docs/api/zh_CN/2.0.9/api_faqs#id-orgid-orgid)                |


## 请求参数（Body）

| 名称          | 是否必须 | 数据类型 | 描述      |
|------------------|---------------|----------|---|
| productKey  | False         | String| Product Key|
| deviceKey   | False         | String| Device Key|
| assetId  | False  | String | 资产ID。[如何获取Asset ID信息>>](/docs/api/zh_CN/2.0.9/api_faqs.html#asset-id-assetid-assetid)|
| tslEventKey | False         | String| 事件key|
| tslEventType | False         | String| 事件类型|
| startTime   | False         | String | 开始时间，针对事件的发生时间而言，格式yyyy-MM-dd HH:mm:ss代表查询本地时间，yyyy-MM-ddTHH:mm:ssZ代表utc时间，如果不填，默认最近一周的数据。|
| endTime  | False         | String    | 结束时间，针对事件的发生时间而言，格式yyyy-MM-dd HH:mm:ss代表查询本地时间，yyyy-MM-ddTHH:mm:ssZ代表UTC时间，如果不填，默认最近一周的数据。|
| expression  | False         | String| 查询表达式，支持类sql的查询。目前支持查询的字段是`productKey`、`deviceKey`、`assetId`、`tslEventKey`、`tslEventType`。支持的算术运算符是=、in，逻辑运算符是and和or。[如何使用查询表达式>>](/docs/api/zh_CN/2.0.9/api_faqs.html#id1) |
| pagination  | False  |Pagination请求结构体 | 分页参数。如未指定，默认每页10条。参见[Pagination请求结构体>>](/docs/api/zh_CN/2.0.9/overview.html?highlight=pagination#pagination)  |



## 响应参数

| 名称| 数据类型 | 描述         |
|-------------|-------------------|-----------------------------|
| data |  Event结构体      |查询得到的事件列表，见[Event结构体>>](/docs/api/zh_CN/2.0.9/connect/get_event.html#id3) |


## 示例 1

### 请求示例

```
url:https://{apigw-address}/connect-service/v2.1/events/search?action=search&orgId=1c499110e8800000
method: POST
requestBody: {"pagination":{"pageNo":1,"pageSize":2},"action":"search"}
```

### 返回示例

```json
{
    "code":0,
    "msg":"OK",
    "requestId":"aae68461-f211-406f-9959-d04af12f28b1",
    "data":[
        {
            "eventId":"20190506587247156ca85be5e3422d30e2642dd1",
            "orgId":"yourOrgId",
            "productKey":"yourProductKey",
            "deviceKey":"yourDeviceKey",
            "assetId":"wNzx7q3S",
            "tslEventKey":"guzang01",
            "tslEventType":"INFO",
            "output":"{"fioat":116}",
            "timestamp":1557113821000,
            "localtime":"2019-05-06 11:37:01"
        }
    ],
    "pagination":{
        "sortedBy":null,
        "pageNo":1,
        "pageSize":2,
        "totalSize":1
    }
}
```

