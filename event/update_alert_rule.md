# Update Alert Rule

更新告警规则。所有请求参数（Body）中包含的参数，只要不是null，都可以被更新。需要进行校验的字段有：模型ID（`modelId`）、测点（`measurepointId`）、告警级别（`severityId`）、告警内容（`contentId`）、查询范围（`scope`）。

## 请求格式

```
POST https://{apigw-address}/event-service/v2.1/alert-rules?action=update
```

## 请求参数（URI）

| 名称          | 位置（Path/Query） | 是否必须 | 数据类型 | 描述      |
|---------------|------------------|----------|-----------|--------------|
| orgId         | Query            | true     | String    | 资产所属的组织ID。[如何获取orgId信息](/docs/api/zh_CN/latest/api_faqs#id-orgid-orgid)                |
|isPatchUpdate|Query|true|Boolean|是否全量更新，false为全量更新，true为部分更新|


## 请求参数（Body）
| 名称 | 是否必须 | 数据类型 | 描述 |
|------|-----------------|-----------|-------------|
|alertRule|true|alertRule结构体|告警规则，见[alertRule结构体](update_alert_rule#alertrule-alertrule)|


### alertRule结构体 <alertrule>

| 名称 | 是否必选（特指在isPatchUpdate=false的情况下） | 数据类型 | 描述 |
|------|-----------------|-----------|-------------|
| ruleId         | true| String| 告警规则编号，由用户指定，是用于定位需要更新的告警规则的唯一标识。|
| ruleDesc       | true| StringI18n| 国际化告警描述，只支持全量更新。结构请见[国际化名称结构体](/docs/api/zh_CN/latest/api_faqs.html#id3)|
| modelId| true| String| 规则适用的模型。[如何获取modelId信息](/docs/api/zh_CN/latest/api_faqs#modelid-modelid)|
| measurepointId | true| String                | 资产测点。[如何获取测点（pointId）信息](/docs/api/zh_CN/latest/api_faqs#pointid-pointid)|
| condition      | true| String| 表达式。使用“/”表达层级关系，目前只支持最多向下一层。[如何使用查询表达式](/docs/api/zh_CN/latest/api_faqs.html#id1) |
| severityId     | true| String| 告警级别编号|
| contentId      | true| String| 告警内容编号|
| tags           | false| tags结构体| 规则标签，只支持全量更新|
| scope          | true         | AssetNode结构体 | 指定资产树上的节点来表明作用域，如果`treeId`为“all”，则这是一个特殊的节点，代表组织下的全局。见[AssetNode结构体](update_alert_rule#assetnode-assetnode) |
| isEnabled      | false| Boolean| 是否允许生效，默认生效（true）|

### AssetNode结构体 <assetnode>

| 名称|是否必选| 数据类型 | 描述|
|----------|--------------|--------------|----------|
| treeId   | true         | String       | 资产树ID |
| assetId  | true         | String       | 资产ID。[如何获取Asset ID信息](/docs/api/zh_CN/latest/api_faqs#asset-id-assetid-assetid)  |


## 响应参数

| 名称  | 数据类型      | 描述               |
|-------|----------------|---------------------------|
|data|null|无|




## 示例

### 请求示例

```json
POST https://{apigw-address}/event-service/v2.1/alert-rules?action=update&orgId=1c499110e8800000&isPatchUpdate=false
{
	"alertRule": {
		"ruleId": "user BID",
		"ruleDesc": {
            "defaultValue": "Grid is connected from converter",
			"i18nValue": {
				"en_US": "Grid is connected from converter",
				"zh_CN": "电网由变频器连接"
			}
		},
		"modelId": "EnOS_Solar_CombinerBox",
		"measurepointId": "CBX.BranchStateAttr",
		"condition": "CBX.BranchStateAttr = 18",
		"severityId": "WARN",
		"contentId": "planetTemperature",
		"tags": {
			"key1": "v1"
		},
		"orgId": "1c499110e8800000",
		"scope": [{
			"treeId": "ptde66nd",
			"assetId": "FbFy8qyz"
		}],
		"isEenabled": true
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
