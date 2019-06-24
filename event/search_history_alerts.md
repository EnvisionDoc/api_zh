# Search History Alerts

查询历史告警。

## 请求格式

```
POST https://apigw-address/event-service/v2.1/history-alerts?action=search
```

## 请求参数（URI）

| 名称          | 是否必须 | 数据类型 | 描述      |
|---------------|--------|----------|-----------|
| orgId         | true     | String    | 资产所属的组织ID。[如何获取orgId信息](/docs/api/zh_CN/latest/api_faqs#orgid-orgid)                |
                                                                 

## 请求参数（Body）
| 名称 | 位置（Path/Query） | 是否必须 | 数据类型 | 描述 |
|------|----------|--------------------|----|------|
| 名称 | 是否必须 | 数据类型 | 描述 |
|------|-----------------|-----------|-------------|
| modelId          | false    | String    | 资产所属模型ID。[如何获取modelId信息](/docs/api/zh_CN/latest/api_faqs#modeid-modeid)  |
| assetIds        | false     | String    | 资产ID，支持查询多个资产，多个资产ID之间用英文逗号隔开。[如何获取assetId信息](/docs/api/zh_CN/latest/api_faqs#assetid-assetid)    |
| measurepointsId     | false     | String    | 资产测点，支持多测点查询，各个测点间用逗号隔开；支持查询的（设备数*测点数）上限为3000。[如何获取测点（pointId）信息](/docs/api/zh_CN/latest/api_faqs#pointid-pointid) |
| startOccurTime        | false     | String，见[API在使用的时间参数](/docs/api/zh_CN/latest/api_faqs.html#id5)   | 告警触发时间的起始时间。 |
| endOccurTime        | false     | String，见[API在使用的时间参数](/docs/api/zh_CN/latest/api_faqs.html#id5)       | 告警触发时间的结束时间。 |
| recoverStartTime        | false     | String，见[API在使用的时间参数](/docs/api/zh_CN/latest/api_faqs.html#id5)       | 告警的恢复时间的起始时间，如果不填，默认最近一周的数据。 |
| recoverEndTime        | false     | String，见[API在使用的时间参数](/docs/api/zh_CN/latest/api_faqs.html#id5)       | 告警的恢复时间的结束时间，如果不填，默认最近一周的数据 |
| expression         | false    | String   | 查询表达式，查询表达式，支持类sql的查询。目前支持查询的字段是`modelId`，`assetId`，`measurepointId`，`hitRuleId`，`severityId`，`typeId`，`subTypeId`，`contentId`，`eventType`，`eventId`，`tag`。支持的算术运算符是=，in，逻辑运算符是and。[如何使用查询表达式](/docs/api/zh_CN/latest/api_faqs.html#id1)|
| pagination     | false     | 见[Pagination请求结构体](/docs/api/zh_CN/latest/overview.html?highlight=pagination#pagination)    | 随机分页，默认就是按照`occurTime`倒序排列，用户不能指定排序字段。默认分页大小是10。|


## 响应参数

| 名称  | 数据类型      | 描述               |
|-------|----------------|---------------------------|
| data | HistoryAlert结构体Array | 历史告警信息数组，包含恢复时间，事件ID，恢复原因等信息|

### HistoryAlert结构体

| 名称  | 数据类型      | 描述               |
|----------------|-----------------------|----------|
| eventId        | String                | 告警id                                                                          |
| orgId          | String                | 资产所属的组织ID。[如何获取orgId信息](/docs/api/zh_CN/latest/api_faqs#orgid-orgid)|
| assetId        | String                | 资产ID，支持查询多个资产，多个资产ID之间用英文逗号隔开。[如何获取assetId信息](/docs/api/zh_CN/latest/api_faqs#assetid-assetid) |
| modelId        | String                | 资产所属模型ID。[如何获取modelId信息](/docs/api/zh_CN/latest/api_faqs#modeid-modeid)  |
| modelIdPath    | String                | 模型路径                                                                        |
| measurepointId | String                | 资产测点，支持多测点查询，各个测点间用逗号隔开；支持查询的（设备数*测点数）上限为3000。[如何获取测点（pointId）信息](/docs/api/zh_CN/latest/api_faqs#pointid-pointid) |
| hitRuleId      | String                | *匹配的规则编号*                                                                |
| value          | Integer/Double/Object | 测点值，参照ThingModel定义                                                      |
| occurTime      | Long                  | 告警发生时间 UTC时间                                                            |
| localOccur     | String                | 告警发生时间 本地时间                                                           |
| recoverTime     | Long                | 告警恢复时间                                                          |
| recoverLocaltime     | String                  | 告警恢复本地时间 |
| recoverReason     | String                | 恢复原因                                                          |
| createTime     | Long                | 入库UTC时间                                                         |
| updateTime     | Long                  | 更新UTC时间                                                                     |
| severityId     | String                | 告警级别编号                                                                    |
| severityDesc   | StringI18n            | 告警级别描述。为一个国际化名称结构体。详见[国际化名称结构体](/docs/api/zh_CN/latest/api_faqs.html#id3)                                                                  |
| typeId         | String                | 告警类别编号                                                                    |
| typeDesc       | StringI18n            | 告警类型的具体描述。为一个国际化名称结构体。详见[国际化名称结构体](/docs/api/zh_CN/latest/api_faqs.html#id3)                                         |
| subTypeId      | String                | 告警子类型                                                                      |
| subTypeDesc    | StringI18n            | 告警子类型描述。为一个国际化名称结构体。详见[国际化名称结构体](/docs/api/zh_CN/latest/api_faqs.html#id3) |
| contentId      | String                | 告警内容编号                                                                    |
| contentDesc    | StringI18n            | 告警描述。为一个国际化名称结构体。详见[国际化名称结构体](/docs/api/zh_CN/latest/api_faqs.html#id3) |
| eventType      | Integer               | 事件类型:0—系统恢复的告警；1—系统触发的告警；2—手动恢复的告警；3—手动插入的告警 |
| tag            | Tag结构体             | 告警标签                                                                        |
| ruleDesc       | StringI18n            | 规则描述。为一个国际化名称结构体。详见[国际化名称结构体](/docs/api/zh_CN/latest/api_faqs.html#id3) |



## 输入输出示例

### 请求示例

```json
POST https://apigw-address/event-service/v2.1/history-alerts?action=search&orgId=1c499110e8800000 

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
		"recoverLocaltime": "2019-06-13 07:36:00",
		"recoverReason": "rule-recover",
		"eventId": "20190612cf89cd96b0be4cafcc342d0dc2ac75a4",
		"orgId": "1c499110e8800000",
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
1.	public void testSearchHistoryAlerts(){  
2.	        String appKey = "4ced4f38-1ced-476e0a446215-a602-4307";  
3.	        String appSecret = "0a446215-a602-4307-9ff2-3feed3e983ce";  
4.	        SearchHistoryAlertRequest request = new SearchHistoryAlertRequest();  
5.	        request.setOrgId("1c499110e8800000");  
6.	        request.setStartOccurTime("2019-05-20T00:00:00Z");  
7.	        request.setEndOccurTime("2019-06-15T00:00:00Z");  
8.	        Pagination pagination = new Pagination();  
9.	        pagination.setPageSize(2);  
10.	        pagination.setPageNo(1);  
11.	        request.setPagination(pagination);  
12.	        request.setExpression("eventId='20190612cf89cd96b0be4cafcc342d0dc2ac75a4' ");  
13.	        request.headerParams().put("apim-accesskey","4ced4f38-1ced-476e0a446215-a602-4307");  
14.	        try {  
15.	  
16.	            SearchHistoryAlertResponse response = Poseidon.config(PConfig.init().appKey(appKey).appSecret(appSecret).debug())  
17.	                    .url("https://apigw-address")  
18.	                    .getResponse(request, SearchHistoryAlertResponse.class);  
19.	            Gson gson = new Gson();  
20.	            System.out.println(gson.toJson(response));  
21.	        }catch(Exception e){  
22.	            System.out.print(e);  
23.	        }  
24.	    }
```