# Search Active Alerts

查询实时告警。

## 请求格式

```
POST https://{apigw-address}/event-service/v2.1/active-alerts?action=search
```

## 请求参数（URI）

| 名称          | 位置（Path/Query） | 是否必须 | 数据类型 | 描述      |
|---------------|------------------|----------|-----------|--------------|
| orgId         | Query            | true     | String    | 资产所属的组织ID。[如何获取orgId信息](/docs/api/zh_CN/latest/api_faqs#id-orgid-orgid)                |
                                                                 

## 请求参数（Body）
| 名称 | 是否必须 | 数据类型 | 描述 |
|------|-----------------|-----------|-------------|
| modelId          | false    | String    | 资产所属模型ID。[如何获取modelId信息](/docs/api/zh_CN/latest/api_faqs#modelid-modelid)  |
| assetId        | false     | String    | 资产ID。[如何获取Asset ID信息](/docs/api/zh_CN/latest/api_faqs#asset-id-assetid-assetid)    |
| measurepointsId     | false     | String    | 资产测点，支持多测点查询，各个测点间用逗号隔开；支持查询的（设备数*测点数）上限为3000。[如何获取测点（pointId）信息](/docs/api/zh_CN/latest/api_faqs#pointid-pointid) |
| startOccurTime        | false     | String  | 告警触发时间的起始时间，见[API在使用的时间参数](/docs/api/zh_CN/latest/api_faqs.html#id5)  |
| endOccurTime        | false     | String     | 告警触发时间的结束时间，见[API在使用的时间参数](/docs/api/zh_CN/latest/api_faqs.html#id5)   |
| expression         | false    | String   | 查询表达式，支持类sql的查询。目前支持查询的字段是`modelId`、`assetId`、`measurepointId`、`hitRuleId`、`severityId`、`typeId`、`subTypeId`、`contentId`、`eventType`、`eventId`、`tag`。支持的算术运算符是=、in和!=，逻辑运算符是and和or。[如何使用查询表达式](/docs/api/zh_CN/latest/api_faqs.html#id1)|
| pagination     | false     |  Pagination请求结构体   | 随机分页，默认就是按照`occurTime`倒序排列，用户不能指定排序字段。默认分页大小是10。见[Pagination请求结构体](/docs/api/zh_CN/latest/overview.html?highlight=pagination#pagination)|

## 响应参数

| 名称  | 数据类型      | 描述               |
|-------|----------------|---------------------------|
| data | ActiveAlert结构体 | 实时告警列表。详见[ActiveAlert结构体](/docs/api/zh_CN/latest/event/search_active_alerts#id5)|

### ActiveAlert结构体

| 名称  | 数据类型      | 描述               |
|----------------|-----------------------|----------|
| eventId        | String                | 告警id                                                                          |
| orgId          | String                | 资产所属的组织ID。|
| assetId        | String                | 资产ID。|
| modelId        | String                | 资产所属模型ID。|
| modelIdPath    | String                | 模型ID路径|
| measurepointId | String| 资产测点|
| hitRuleId      | String                | 匹配的规则编号|
| value          | Integer/Double/Object | 测点值|
| occurTime      | Long| 告警发生时间UTC时间|
| localOccur     | String| 告警发生时间，本地时间|
| createTime     | Long| 入库UTC时间|
| updateTime     | Long| 更新UTC时间|
| severityId     | String| 告警级别编号|
| severityDesc   | StringI18n            | 告警级别描述|
| typeId         | String                | 告警类别编号|
| typeDesc       | StringI18n            | 告警类型的具体描述|
| subTypeId      | String                | 告警子类型|
| subTypeDesc    | StringI18n            | 告警子类型描述|
| contentId      | String                | 告警内容编号|
| contentDesc    | StringI18n            | 告警描述|
| eventType      | Integer               | 事件类型:0：系统恢复的告警；1：系统触发的告警；2：手动恢复的告警；3：手动插入的告警 |
| tag            | Tag结构体             | 告警标签|
| ruleDesc       | StringI18n            | 规则描述|



## 输入输出示例

### 请求示例

```json
POST https://{apigw-address}/event-service/v2.1/active-alerts?action=search &orgId=1c499110e8800000 
{
	"expression": "eventId='20190531b83331a8549e1e956f2413552eda1ec9'",
	"pagination": {
		"pageNo": 1,
		"pageSize": 20
	              }
}

```

### 返回示例

```json
{
	"pagination": {
		"pageNo": 1,
		"pageSize": 20,
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
	"requestId": "a9689b9f-0cb6-4e47-a41c-bd459b687309",
	"data": [{
		"eventId": "20190531b83331a8549e1e956f2413552eda1ec9",
		"orgId": "yourOrgId",
		"assetId": "qu5TmJRj",
		"modelId": "Inverter_Model",
		"modelIdPath": "/Inverter_Model",
		"measurepointId": "power",
		"value": "3.5559796405967736",
		"occurTime": 1559304899404,
		"localOccurTime": "2019-06-01 02:14:59",
		"createTime": 1559304899519,
		"updateTime": 1560745022684,
		"severityId": "alert_001",
		"severityDesc": {
			"i18nValue": {
				"en_US": "警告",
				"zh_CN": "警告"
			             }
		                },
		"typeId": "errorType",
		"typeDesc": {
			"i18nValue": {
				"en_US": "errorType desc",
				"zh_CN": ""
			             }
		            },
		"contentId": "001",
		"contentDesc": {
			"i18nValue": {
				"en_US": "001",
				"zh_CN": "001"
			             }
		               },
		"eventType": 1,
		"tag": {
			"Tag999": "999"
		       }
	        }]
}
```

## Java SDK调用示例

```java
public void testSearchActiveAlerts(){  
        String accessKey = "4ced4f38-1ced-476e0a446215-a602-4307";  
        String secretKey = "0a446215-a602-4307-9ff2-3feed3e983ce";  
        SearchActiveAlertRequest request = new SearchActiveAlertRequest();  
        request.setOrgId("1c499110e8800000");  
        request.setExpression("eventId='20190531b83331a8549e1e956f2413552eda1ec9'");  
        Pagination pagination = new Pagination();  
        pagination.setPageSize(20);  
        pagination.setPageNo(1);  
	        request.setPagination(pagination);  
	        request.headerParams().put("apim-accesskey","4ced4f38-1ced-476e0a446215-a602-4307");  
	        try {  
	            SearchActiveAlertResponse response = Poseidon.config(PConfig.init().appKey(accessKey).appSecret(secretKey).debug())  
	                    .url("https://{apigw-address}")  
	                    .getResponse(request, SearchActiveAlertResponse.class);  
	            Gson gson = new Gson();  
	            System.out.println(gson.toJson(response));  
	        }catch(Exception e){  
	            System.out.print(e);  
	        }  
}
```