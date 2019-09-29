# Delete Alert Severity

删除告警级别。需要校验告警级别是否被其它规则使用，若有规则使用，则不允许删除。

## 请求格式

```
POST https://{apigw-address}/event-service/v2.1/alert-severities?action=delete
```

## 请求参数（URI）

| 名称          | 位置（Path/Query） | 是否必须 | 数据类型 | 描述      |
|---------------|------------------|----------|-----------|--------------|
| orgId         | Query            | true     | String    | 资产所属的组织ID。[如何获取orgId信息>>](/docs/api/zh_CN/2.0.9/api_faqs#id-orgid-orgid)                |
|severityId      | Query  |  true  |   String  |  告警级别编号|
| source  | Query  | false | String |自定义数据来源，用以表明告警级别适用的数据源。若适用于EnOS Cloud，则为空；若适用于EnOS Edge，则为edge。|



## 响应参数

| 名称  | 数据类型      | 描述               |
|-------|----------------|---------------------------|
|data   |   null  | 无   |



## 示例

### 请求示例

```json
POST https://{apigw-address}/event-service/v2.1/alert-severities?action=delete&orgId=1c499110e8800000&severityId=planetTemperature
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
