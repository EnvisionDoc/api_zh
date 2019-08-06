# Update Alert Severity

更新告警级别，需要校验`severityId`。

## 请求格式

```
POST https://{apigw-address}/event-service/v2.1/alert-severities?action=update
```

## 请求参数（URI）

| 名称          | 位置（Path/Query） | 是否必须 | 数据类型 | 描述      |
|---------------|------------------|----------|-----------|--------------|
| orgId         | Query            | true     | String    | 资产所属的组织ID。[如何获取orgId信息](/docs/api/zh_CN/latest/api_faqs#id-orgid-orgid)|
|isPatchUpdate	 | Query      | true |  Boolean  | 是否全量更新，false为全量更新，true为部分更新|


## 请求参数（Body）
| 名称 | 是否必须 | 数据类型 | 描述 |
|------|-----------------|-----------|-------------|
| severity   |   true   |   generateSeverity结构体  |  告警级别，见[generateSeverity结构体](update_alert_severity#generateseverity-generateseverity) |


### generateSeverity结构体 <generateseverity>

| 名称  | 是否必选 | 数据类型 | 描述                         |
|--------------|--------------|--------------|-------------------------------------|
| severityId   | true         | String       | 告警级别编号                        |
| severityDesc | true         | StringI18n   | 国际化告警级别描述，其中default必填。结构请见[国际化名称结构体](/docs/api/zh_CN/latest/api_faqs.html#id3) |
| tags         | false        | tags数据类型 | 标签                                |


## 响应参数

| 名称  | 数据类型      | 描述               |
|-------|----------------|---------------------------|
|data   |   null  | 无  |



## 示例

### 请求示例

```json
POST https://{apigw-address}/event-service/v2.1/alert-severities?action=update&orgId=1c499110e8800000&isPatchUpdate=false
{
	"severity": {
		"severityId": "planetTemperature",
		"severityDesc": {
			"defaultValue": "Error",
			"i18nValue": {
				"en_US": "Error",
				"zh_CN": "错误"
			}
		},
		"tags": {
			"year": "2000",
			"author": "cshan"
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
