# Create Alert Severity

创建一条告警级别。

## 请求格式

```
POST https://{apigw-address}/event-service/v2.1/alert-severities?action=create
```

## 请求参数（URI）

| 名称          | 位置（Path/Query） | 是否必须 | 数据类型 | 描述      |
|---------------|------------------|----------|-----------|--------------|
| orgId         | Query            | true     | String    | 资产所属的组织ID。[如何获取orgId信息>>](/docs/api/zh_CN/latest/api_faqs#id-orgid-orgid)                |


## 请求参数（Body）
| 名称 | 是否必须 | 数据类型 | 描述 |
|------|-----------------|-----------|-------------|
| severity |  true  |  generateSeverity结构体  |  告警级别，见[generateSeverity结构体](create_alert_severity#generateseverity-generateseverity)   |



### generateSeverity结构体 <generateseverity>

| 名称   | 是否必选| 数据类型 | 描述                          |
|--------------|--------------|--------------|-------------------------------------|
| severityId   | true         | String       | 告警级别编号|
| severityDesc | true         | StringI18n   | 国际化告警级别描述，其中default必填。结构请见[国际化名称结构体>>](/docs/api/zh_CN/latest/api_faqs.html#id3)|
| tags         | false        | tags数据类型 | 告警级别的标签|
| source  | false | String |自定义数据来源，用以表明告警级别适用的数据源。若适用于EnOS Cloud，则为空；若适用于EnOS Edge，则为edge。|



## 响应参数

| 名称  | 数据类型      | 描述               |
|-------|----------------|---------------------------|
|  data   |  String   |  severityId   |



## 示例

### 请求示例

```json
POST https://{apigw-address}/event-service/v2.1/alert-severities?action=create&orgId=yourOrgId
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
	"requestId": "4873095e-621d-4cfd-bc2c-edb520f574ea"
}
```
