# Search History Alerts

查询最近三个月内的历史告警。

## 请求格式

```
POST https://{apigw-address}/event-service/v2.1/history-alerts?action=search
```

## 请求参数（URI）

| 名称          | 是否必须 | 数据类型 | 描述      |
|---------------|--------|----------|-----------|
| orgId         | true     | String    | 资产所属的组织ID。[如何获取orgId信息>>](/docs/api/zh_CN/latest/api_faqs#id-orgid-orgid)                |


## 请求参数（Body）

| 名称 | 是否必须 | 数据类型 | 描述 |
|------|-----------------|-----------|-------------|
| modelId          | false    | String    | 资产所属模型ID。[如何获取modelId信息>>](/docs/api/zh_CN/latest/api_faqs#modelid-modelid)  |
| assetId       | false     | String    | 资产ID。[如何获取Asset ID信息>>](/docs/api/zh_CN/latest/api_faqs#asset-id-assetid-assetid)    |
| measurepointsId     | false     | String    | 资产测点。[如何获取测点（pointId）信息>>](/docs/api/zh_CN/latest/api_faqs#pointid-pointid) |
| startOccurTime        | false     | String   | 查询起始时间，与`endOccurTime`配合使用，表示查询该时段内被触发的告警。见[API在使用的时间参数>>](/docs/api/zh_CN/latest/api_faqs.html#id5) |
| endOccurTime        | false     | String       | 查询结束时间，与`startOccurTime`配合使用，表示查询该时段内被触发的告警。见[API在使用的时间参数>>](/docs/api/zh_CN/latest/api_faqs.html#id5) |
| recoverStartTime        | false     | String  | 查询起始时间，与`recoverEndTime`配合使用，表示查询在该时段内异常状态恢复正常的告警，若不指定，默认为最近一周的数据。见[API在使用的时间参数>>](/docs/api/zh_CN/latest/api_faqs.html#id5) |
| recoverEndTime        | false     | String  | 查询起始时间，与`recoverStartTime`配合使用，表示查询在该时段内异常状态恢复正常的告警，若不指定，默认为最近一周的数据。见[API在使用的时间参数>>](/docs/api/zh_CN/latest/api_faqs.html#id5) |
| expression         | false    | String   | 查询表达式，支持类sql的查询。目前支持查询的字段是`modelId`，`assetId`，`measurepointId`，`hitRuleId`，`severityId`，`typeId`，`subTypeId`，`contentId`，`eventType`，`eventId`，`tag`。支持的算术运算符是=、in，逻辑运算符是and。[如何使用查询表达式>>](/docs/api/zh_CN/latest/api_faqs.html#id1)|
| scope |  false   | Scope结构体 | 查询指定资产树或资产树上某资产节点下的告警，并指定是否返回被屏蔽的衍生告警。**该参数不可与rootAlert参数同时使用**。见[Scope结构体](search_history_alerts#scope-scope)。 |
|  rootAlert  |   false  | RootAlert结构体 | 查询被指定根源告警屏蔽的衍生告警。**该参数不可与scope参数同时使用**。见[RootAlert结构体](search_history_alerts#rootalert-rootalert)。|
| pagination     | false     |  Pagination请求结构体   | 随机分页，默认按照`occurTime`倒序排列。如未指定，默认分页大小是10。见[Pagination请求结构体>>](/docs/api/zh_CN/latest/overview.html?highlight=pagination#pagination)|



### Scope结构体 <scope>

| 名称        | 是否必须 | 数据类型| 描述|
|------------|--------------|--------------|-----------|
| treeId            | true         | String       | 资产树ID|
| fromAssetId       | false        | String       | 资产ID。可选。<br>当未指定时，返回`treeId`指定的资产树内所有节点的告警；<br>当指定时，返回该资产节点下（包含该节点）的所有告警
| includeDerivative | false        | Boolean      | 是否返回衍生告警，默认为false，不返回衍生告警|



### RootAlert结构体 <rootalert>

| 名称   | 是否必须 | 数据类型 | 描述   |
|-------------|--------------|--------------|------------|
| treeId      | false        | String       | 资产树ID   |
| rootAlertId | true         | String       | 根源告警ID |



## 响应参数

| 名称  | 数据类型      | 描述               |
|-------|----------------|---------------------------|
| data | HistoryAlert结构体| 历史告警信息数组，包含恢复时间，事件ID，恢复原因等信息。见[HistoryAlert结构体>>](/docs/api/zh_CN/latest/event/search_history_alerts.html#id7)|

### HistoryAlert结构体

| 名称  | 数据类型      | 描述               |
|----------------|-----------------------|----------|
| eventId        | String                | 告警ID                                                                          |
| orgId          | String                | 资产所属的组织ID|
| assetId        | String                | 资产ID|
| modelId        | String                | 资产所属模型ID|
| modelIdPath    | String                | 模型所属路径|
| measurepointId | String                | 资产测点|
| hitRuleId      | String                | 触发的告警规则编号|
| value          | Integer/Double/Object | 测点值。若告警规则中指定了 ``triggeringDelayTimer``，则测点值为 ``triggeringDelayTimer``开始计时时测点的值。|
| occurTime      | Long                  | 告警发生的时间，以UTC时间表示|
| localOccurTime     | String                | 告警发生的时间，以本地时间表示|
| recoverTime     | Long                | 触发告警的异常状况恢复正常的时间，以UTC时间表示|
| localRecoverTime     | String                  | 触发告警的异常状况恢复正常的时间，以本地时间表示 |
| recoverReason     | String                | 异常状况恢复的原因|
| createTime     | Long                | 该告警记录的入库时间，以UTC时间表示|
| updateTime     | Long                  | 该告警记录的更新时间，以UTC时间表示 |
| severityId     | String                | 告警级别标识符|
| severityDesc   | StringI18n            | 告警级别描述|
| typeId         | String                | 告警类别标识符|
| typeDesc       | StringI18n            | 告警类型的具体描述                  |
| subTypeId      | String                | 告警子类型|
| subTypeDesc    | StringI18n            | 告警子类型描述 |
| contentId      | String                | 告警内容标识符|
| contentDesc    | StringI18n            | 告警内容描述|
| eventType      | Integer               | 事件类型:0：系统恢复的告警；1：系统触发的告警；2：手动恢复的告警；3：手动插入的告警 |
| tag            | Tag结构体             | 告警标签|
| ruleDesc       | StringI18n            | 规则描述|
| assetPaths  |  String Array     | 根据告警规则的作用域，返回告警资产在资产树上的路径列表。<br>返回格式为：["treeId1:/assetId1/assetId2/assetIdx", "treeId2:/assetId3/assetIdx"]|
| maskedBy  |  String Array     |如果该告警条目是衍生告警，返回导致该告警被屏蔽的根源告警信息。<br>返回格式为：["treeId1:eventId1", "treeId1:eventId2"]|



## 输入输出示例

### 请求示例

```json
POST https://{apigw-address}/event-service/v2.1/history-alerts?action=search&orgId=1c499110e8800000 

{
	"endOccurTime": "2019-06-15T00:00:00Z",
	"expression": "eventId='20190612cf89cd96b0be4cafcc342d0dc2ac75a4' ",
	"pagination": {
		"pageNo": 1,
		"pageSize": 2
	},
	"startOccurTime": "2019-05-20T00:00:00Z"
}
```

### 返回示例

```json
{
	"pagination": {
		"pageNo": 1,
		"pageSize": 2,
		"totalSize": 1,
		"sortedBy": [{
			"field": "occurTime",
			"order": "DESC"
		},
		{
			"field": "eventId",
			"order": "DESC"
		}]
	},
	"code": 0,
	"msg": "OK",
	"requestId": "dac2a872-b9b7-460c-992d-0a0c14ea36e9",
	"data": [{
		"recoverTime": 1560382560000,
		"recoverLocalTime": "2019-06-13 07:36:00",
		"recoverReason": "rule-recover",
		"eventId": "20190612cf89cd96b0be4cafcc342d0dc2ac75a4",
		"orgId": "yourOrgId",
		"assetId": "rQN8IRs4",
		"modelId": "lemo2",
		"modelIdPath": "/lemo2",
		"measurepointId": "lemo_point1_raw",
		"value": "99.06250421",
		"occurTime": 1560382380000,
		"localOccurTime": "2019-06-13 07:33:00",
		"createTime": 1560382559735,
		"updateTime": 1560744923855,
		"severityId": "Urgent",
		"severityDesc": {
			"i18nValue": {
				"en_US": "紧急告警",
				"zh_CN": "紧急告警"
			}
		},
		"typeId": "lemo_001",
		"typeDesc": {
			"i18nValue": {
				"en_US": "lemo_001",
				"zh_CN": "越上限告警"
			}
		},
		"contentId": "001",
		"contentDesc": {
			"i18nValue": {
				"en_US": "告警内容",
				"zh_CN": "已经越上限50啦，快去处理呀"
			}
		},
		"eventType": 0,
		"tag": {
			"tag999": "999",
			"tag000": "000"
		}
	}]
}
```

## Java SDK调用示例

```java
public void testSearchHistoryAlerts(){  
        String accessKey = "4ced4f38-1ced-476e0a446215-a602-4307";  
        String secretKey = "0a446215-a602-4307-9ff2-3feed3e983ce";  
        SearchHistoryAlertRequest request = new SearchHistoryAlertRequest();  
        request.setOrgId("1c499110e8800000");  
        request.setStartOccurTime("2019-05-20T00:00:00Z");  
        request.setEndOccurTime("2019-06-15T00:00:00Z");  
        Pagination pagination = new Pagination();  
        pagination.setPageSize(2);  
	        pagination.setPageNo(1);  
	        request.setPagination(pagination);  
	        request.setExpression("eventId='20190612cf89cd96b0be4cafcc342d0dc2ac75a4' ");  
	        request.headerParams().put("apim-accesskey","4ced4f38-1ced-476e0a446215-a602-4307");  
	        try {  
	            SearchHistoryAlertResponse response = Poseidon.config(PConfig.init().appKey(accessKey).appSecret(secretKey).debug())  
	                    .url("https://{apigw-address}")  
	                    .getResponse(request, SearchHistoryAlertResponse.class);  
	            Gson gson = new Gson();  
	            System.out.println(gson.toJson(response));  
	        }catch(Exception e){  
	            System.out.print(e);  
	        }  
	    }
```