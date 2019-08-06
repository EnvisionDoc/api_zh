# Create History Alert

创建历史告警。除了必填性校验，不需要对参数的合法性进行校验。用户使用的如`contentId`不会在EnOS平台的系统上维护。相同`assetId`、`measurepointId`和`occurTime`的插入告警只作更新操作。

## 请求格式

```
POST https://{apigw-address}/event-service/v2.1/history-alerts?action=create
```

## 请求参数（URI）

| 名称          | 位置（Path/Query） | 是否必须 | 数据类型 | 描述      |
|---------------|------------------|----------|-----------|--------------|
| orgId         | Query            | true     | String    | 资产所属的组织ID。[如何获取orgId信息](/docs/api/zh_CN/latest/api_faqs#id-orgid-orgid)                |


## 请求参数（Body）
| 名称 | 是否必须 | 数据类型 | 描述 |
|------|-----------------|-----------|-------------|
| historyAlert | true | HistoryAlert结构体 | 历史告警，见[HistoryAlert结构体](create_history_alert#historyalert-historyalert) |



### HistoryAlert结构体 <historyalert>

| 名称 | 是否必须 | 数据类型 | 描述 |
|------|-----------------|-----------|-------------|
| assetId        | true     | String    | 资产ID。[如何获取Asset ID信息](/docs/api/zh_CN/latest/api_faqs#asset-id-assetid-assetid)    |
| modelId          | true    | String    | 告警适用的模型的ID。[如何获取modelId信息](/docs/api/zh_CN/latest/api_faqs#modelid-modelid)  |
| modelIdPath      | false        | String       | 模型路径                     |
| measurepointId   | true         | String       |  资产测点。[如何获取测点（pointId）信息](/docs/api/zh_CN/latest/api_faqs#pointid-pointid)|
| value            | true         | Object       | 测点值                       |
| occurTime        | true         | Long         | 发生的UTC时间片，格式见[UTC采用的ISO8601标准时间格式](/docs/api/zh_CN/latest/api_faqs.html#utciso8601)    |
| localOccurTime   | false        | String       | 本地发生时间，格式见[localtime采用的日期时间格式](/docs/api/zh_CN/latest/api_faqs.html#localtime)|
| recoverTime      | true         | Long         | 恢复的UTC时间，格式见[UTC采用的ISO8601标准时间格式](/docs/api/zh_CN/latest/api_faqs.html#utciso8601)|
| recoverLocalTime | false        | String       | 恢复的本地时间，格式见[localtime采用的日期时间格式](/docs/api/zh_CN/latest/api_faqs.html#localtime)|
| recoverReason    | false        | String       | 恢复原因|
| severityId       | false        | String       | 告警级别编号|
| severityDesc     | false        | StringI18n   | 告警级别描述|
| typeId           | false        | String       | 告警类型编号|
| typeDesc         | false        | StringI18n   | 告警描述|
| subTypeId        | false        | String       | 告警子类型编号|
| subTypeDesc      | false        | StringI18n   | 告警子类型描述|
| contentId        | false        | String       | 告警内容编号|
| contentDesc      | false        | StringI18n   | 告警内容描述|
| tags             | false        | tags数据类型 | 标签，只支持全量更新|



## 响应参数

| 名称  | 数据类型      | 描述               |
|-------|----------------|---------------------------|
|  data | null |  无  |



## 示例

### 请求示例

```json
POST https://{apigw-address}/event-service/v2.1/history-alerts?action=create&orgId=1c499110e8800000
{
  "historyAlert": {
	 "assetId": "qu5TmJRj",
	 "modelId": "Inverter_Model",
	 "modelIdPath": "/Inverter_Model",
	 "measurepointId": "power",
	 "value": "3.5559796405967736",
	 "occurTime": 1559304899404,
	 "localOccurTime": "2019-06-01 02:14:59",
	 "recoverTime": 1559304900404,
	 "localRecoverTime": "2019-06-01 12:14:59",
		 "severityId": "alert_001",
	 "severityDesc": {
        "defaultValue": "Warn",
		 "i18nValue": {
			 "en_US": "警告",
			 "zh_CN": "警告"
		 }
	 },
	 "typeId": "errorType",
	 "typeDesc": {
        "defaultValue": "Warn",
		 "i18nValue": {
			 "en_US": "login failed",
			 "zh_CN": "登录失败"
		 }
	 },
	 "contentId": "planetTemperature",
	 "contentDesc": {
        "defaultValue": "the temperature is too high",
		 "i18nValue": {
			 "en_US": "the temperature is too high",
			 "zh_CN": "温度过高"
		 }
	 },
	 "tags": {
		 "Tag666": "63253w532",
		 "Tag888": "63253w532888",
		 "Tag": "1111"
	 }
  }
}
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
