# Update Alert Type

更新告警类型。需要校验的字段为`typeId`。

## 请求格式

```
POST https://{apigw-address}/event-service/v2.1/alert-types?action=update
```

## 请求参数（URI）

| 名称          | 位置（Path/Query） | 是否必须 | 数据类型 | 描述      |
|---------------|------------------|----------|-----------|--------------|
| orgId         | Query            | true     | String    | 资产所属的组织ID。[如何获取orgId信息>>](/docs/api/zh_CN/2.0.9/api_faqs#id-orgid-orgid)|
|isPatchUpdate	 | Query      | true |  Boolean  | 是否全量更新。<br>当其值为true时，只更新参数中指定字段的值；<br>当其值为false时，更新所有字段的值，即未指定值的字段将被置空。|


## 请求参数（Body）
| 名称 | 是否必须 | 数据类型 | 描述 |
|------|-----------------|-----------|-------------|
| type          | true    | generateType结构体    | 告警类型[generateType结构体](update_alert_type#generatetype-generatetype)。 |



### generateType结构体 <generatetype>

| 名称| 是否必选| 数据类型| 描述                        |
|----------|--------------|--------------|-------------------------------------|
| typeId   |  true        | String       | 告警类型编号|
| typeDesc | true         | StringI18n   | 国际化告警类型描述，其中default必填。结构请见[国际化名称结构体>>](/docs/api/zh_CN/2.0.9/api_faqs.html#id3)|
| tags     | false        | tags数据类型 | 标签 |
| source  | false | String |自定义数据来源，用以表明告警类型适用的数据源。若适用于EnOS Cloud，则为空；若适用于EnOS Edge，则为edge。|


## 响应参数

| 名称  | 数据类型      | 描述               |
|-------|----------------|---------------------------|
| data |  null |  无 |



## 示例

### 请求示例

```json
POST https://{apigw-address}/event-service/v2.1/alert-types?action=update&orgId=1c499110e8800000&isPatchUpdate=false
{
	"generateType": {
		"typeId": "planetTemperature",
 	        "typeDesc": {
			"defaultValue": "OverLimit",
			"i18nValue": {
				"en_US": "OverLimit",
				"zh_CN": "超限"
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
