# Delete Active Alert

删除指定告警，如果不存在，返回失败并给出具体信息。

## 请求格式

```
POST https://{apigw-address}/event-service/v2.1/active-alerts?action=delete
```

## 请求参数（URI）

| 名称          | 位置（Path/Query） | 是否必须 | 数据类型 | 描述      |
|---------------|------------------|----------|-----------|--------------|
| orgId         | Query            | true     | String    | 资产所属的组织ID。[如何获取orgId信息>>](/docs/api/zh_CN/2.0.9/api_faqs#id-orgid-orgid)                |
|  eventId  | Query  | true  |  String  |  告警ID  |



## 响应参数

| 名称  | 数据类型      | 描述               |
|-------|----------------|---------------------------|
| data |  null |  无  |




## 示例

### 请求示例

```json
POST https://{apigw-address}/event-service/v2.1/active-alerts?action=delete&orgId=1c499110e8800000&eventId=2019060135b6df70b2de6aa2f2eb1d09e9aa1ae7
```

### 返回示例

```json
{
	"code": 0,
	"msg": "OK",
	"requestId": "4873095e-621d-4cfd-bc2c-edb520f574ea",
	"data": ""
}
```
