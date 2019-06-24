# Search Alert Severity

分页查询告警级别。

## 请求格式

```
POST https://apigw-address/event-service/v2.0/alert-severities?action=search
```

## 请求参数（URI）

| 名称          | 位置（Path/Query） | 是否必须 | 数据类型 | 描述      |
|---------------|------------------|----------|-----------|--------------|
| orgId         | Query            | true     | String    | 资产所属的组织ID。[如何获取orgId信息](/docs/api/zh_CN/latest/api_faqs#orgid-orgid)                |
                                                                 

## 请求参数（Body）
| 名称 | 是否必须 | 数据类型 | 描述 |
|------|-----------------|-----------|-------------|
| expression         | false    | String   | 查询表达式，查询表达式，支持类sql的查询。目前支持查询的字段是`modelId`，`assetId`，`measurepointId`，`hitRuleId`，`severityId`，`typeId`，`subTypeId`，`contentId`，`eventType`，`eventId`，`tag`。支持的算术运算符是=，in，逻辑运算符是and。[如何使用查询表达式](/docs/api/zh_CN/latest/api_faqs.html#id1)|
| pagination     | false     | 见[Pagination请求结构体](/docs/api/zh_CN/latest/overview.html?highlight=pagination#pagination)    | 分页的参数。如果不填，默认每页10条。按照`updateTime`降序排序。用户可以指定`AlertSeverity`结构体中的字段作为排序字段。|

## 响应参数

| 名称  | 数据类型      | 描述               |
|-------|----------------|---------------------------|
| data | AlertSeverity结构体Array | 告警级别|

### AlertSeverity结构体

| 名称  | 数据类型      | 描述               |
|----------------|-----------------------|----------|
| severityId        | String                | 告警级别编号|
| orgId          | String                | 资产所属的组织ID。[如何获取orgId信息](/docs/api/zh_CN/latest/api_faqs#orgid-orgid)|
| severityDesc   | StringI18n            | 告警级别描述。为一个国际化名称结构体。详见[国际化名称结构体](/docs/api/zh_CN/latest/api_faqs.html#id3) |
| tags        | Tag结构体          | 标签|
| updatePerson        | String                | 更新人|
| updateTime    | Long                | 更新的UTC时间



## 输入输出示例

### 请求示例

```json
POST  https://apigw-address/event-service/v2.1/alert-severities?action=search&orgId=1c499110e8800000
{
	"pagination": {
		"pageNo": 1,
		"pageSize": 1,
		"sorters": [{
			"field": "severityID",
			"order": "ASC"
		}]
	}
}
```

### 返回示例

```json
{
	"pagination": {
		"pageNo": 1,
		"pageSize": 1,
		"totalSize": 19,
		"sortedBy": [{
			"field": "severityID",
			"order": "ASC"
		}]
	},
	"code": 0,
	"msg": "OK",
	"requestId": "bd591868-0eb1-46dc-a989-c1de33cc671e",
	"data": [{
		"severityId": "001",
		"orgId": "1c499110e8800000",
		"severityDesc": {
			"i18nValue": {
				"en_US": "Serious！！！",
				"zh_CN": "严重！！！"
			}
		},
		"tags": {
			"111": "2222"
		},
		"updatePerson": "yj_test_customer",
		"updateTime": 1559204166000
	}]
}
```

## Java SDK调用示例

```java
1.	public void testSearchAlertSeverity() {  
2.	    SearchAlertSeverityRequest request = new SearchAlertSeverityRequest();  
3.	    request.setOrgId("1c499110e8800000");  
4.	    Pagination pagination = new Pagination();  
5.	    pagination.setPageSize(1);  
6.	    pagination.setPageNo(1);  
7.	    Sorter sorter = new Sorter("severityID", Sorter.Order.ASC);  
8.	    List<Sorter> sorterList = new ArrayList<>();  
9.	    sorterList.add(sorter);  
10.	    pagination.setSorters(sorterList);  
11.	    request.setPagination(pagination);  
12.	  
13.	    request.headerParams().put("apim-accesskey", "4ced4f38-1ced-476e0a446215-a602-4307");  
14.	  
15.	  
16.	    try {  
17.	        SearchAlertSeverityResponse response = Poseidon.config(PConfig.init().appKey(appKey).appSecret(appSecret).debug())  
18.	                .url("https://apigw-address")  
19.	                .getResponse(request, SearchAlertSeverityResponse.class);  
20.	        Gson gson = new Gson();  
21.	        System.out.println(gson.toJson(response));  
22.	    } catch (Exception e) {  
23.	        System.out.print(e);  
24.	    }  
25.	}
```