# Update Alert Content

更新告警内容。需要校验的字段为`modelId`和`alertTypeId`。

## 请求格式

```
POST https://{apigw-address}/event-service/v2.1/alert-contents?action=update
```

## 请求参数（URI）

| 名称          | 位置（Path/Query） | 是否必须 | 数据类型 | 描述      |
|---------------|------------------|----------|-----------|--------------|
| orgId         | Query            | true     | String    | 资产所属的组织ID。[如何获取orgId信息>>](/docs/api/zh_CN/latest/api_faqs#id-orgid-orgid)                |
|isPatchUpdate|Query|true|Boolean|是否全量更新。<br>当其值为true时，只更新参数中指定字段的值；<br>当其值为false时，更新所有字段的值，即未指定值的字段将被置空。|


## 请求参数（Body）
| 名称 | 是否必须 | 数据类型 | 描述 |
|------|-----------------|-----------|-------------|
| alertContent          | true    | generateContent结构体    | 告警内容，见[generateContent结构体](update_alert_content#generatecontent-generatecontent)。|



### generateContent结构体 <generatecontent>

| 名称 | 是否必须 | 数据类型 | 描述 |
|------|-----------------|-----------|-------------|
|contentId|true|String|告警内容编号|
|contentDesc|true|String|告警内容描述|
| modelId          | true    | String    | 告警内容所适用模型的ID。[如何获取modelId信息>>](/docs/api/zh_CN/latest/api_faqs#modelid-modelid)  |
| alertTypeId        | true     | String    | 关联的告警类型编号 |
|tags|false|tags数据类型|标签，只支持全量更新|
| source  | false | String |自定义数据来源，用以表明告警内容适用的数据源。若适用于EnOS Cloud，则为空；若适用于EnOS Edge，则为edge。|

## 响应参数

| 名称  | 数据类型      | 描述               |
|-------|----------------|---------------------------|
|data | null  |  无  |




## 示例

### 请求示例

```json
POST https://{apigw-address}/event-service/v2.1/alert-rules?action=update&orgId=1c499110e8800000&isPatchUpdate=false
{
	"alertContent": {
		"contentId": "planetTemperature",
		"contentDesc": {
			"defaultValue": "Grid is connected from converter",
			"i18nValue": {
				"en_US": "Grid is connected from converter",
				"zh_CN": "风机已并网"
			}
		},
		"modelId": "WindDev-E0",
		"alertTypeId": "9001",
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
