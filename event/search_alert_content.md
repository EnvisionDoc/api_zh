# Search Alert Content

分页查询告警内容。

## 请求格式

```
POST https://{apigw-address}/event-service/v2.1/alert-contents?action=search
```

## 请求参数（URI）

| 名称          | 位置（Path/Query） | 是否必须 | 数据类型 | 描述      |
|---------------|------------------|----------|-----------|--------------|
| orgId         | Query            | true     | String    | 资产所属的组织ID。[如何获取orgId信息>>](/docs/api/zh_CN/latest/api_faqs#id-orgid-orgid)                |


## 请求参数（Body）
| 名称 | 是否必须 | 数据类型 | 描述 |
|------|-----------------|-----------|-------------|
| modelId          | false    | String    | 资产所属模型ID。[如何获取modelId信息>>](/docs/api/zh_CN/latest/api_faqs#modelid-modelid)  |
| alertTypeId  | false    | String               | 告警类型ID   |
| subAlertTypeId | false | String | 告警子类型ID |
| expression         | false    | String   | 查询表达式，支持类sql的查询。目前支持查询的字段是`contentId`、`modelId`、`alertTypeId`。支持的算术运算符是=、in，逻辑运算符是and和or。[如何使用查询表达式>>](/docs/api/zh_CN/latest/api_faqs.html#id1)|
| pagination     | false     | Pagination请求结构体    | 分页的参数。如未指定，默认每页10条。默认按照`updateTime`降序排序，支持用户指定以下字段排序：`contentId`、`modelId`、`updatePerson`、`updateTime`。见[Pagination请求结构体](/docs/api/zh_CN/latest/overview.html?highlight=pagination#pagination)。|

## 响应参数

| 名称  | 数据类型      | 描述               |
|-------|----------------|---------------------------|
| data | AlertContent结构体 | 告警内容，见[AlertContent结构体>>](/docs/api/zh_CN/latest/event/search_alert_content.html#id4)|

### AlertContent结构体

| 名称  | 数据类型      | 描述               |
|----------------|-----------------------|----------|
| contentId| String           | 内容ID                 |
| contentDesc | StringI18n | 告警内容描述  |
| modelId| String           | 模型ID                 |
| orgId          | String| 资产所属的组织ID|
| alertType  | AlertType结构体  | 告警类型               |
| subAlertType | AlertType结构体 | 子告警类型 |
| tags| Tag结构体        | 用户自定义告警内容标签 |
| source | String |自定义数据来源，用以表明告警内容适用的数据源。若适用于EnOS Cloud，则为空；若适用于EnOS Edge，则为edge。|
| updatePerson| String           | 更新人员名称           |
| updateTime| Long             | 最后一次更新时间       |



## 输入输出示例

### 请求示例

```json
https://{apigw-address}/event-service/v2.1/alert-contents?action=search&orgId=1c499110e8800000
{
	"pagination": {
		"pageNo": 1,
		"pageSize": 1,
		"sorters": [{
			"field": "contentId",
			"order": "DESC"
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
		"totalSize": 9,
		"sortedBy": [{
			"field": "contentId",
			"order": "DESC"
		}]
	},
	"code": 0,
	"msg": "OK",
	"requestId": "c4e28bda-8d76-4145-bc42-11bfc2c09c0d",
	"data": [{
		"contentId": "dateContentid",
		"contentDesc": {
			"i18nValue": {
				"en_US": "dateContentid desc",
				"zh_CN": ""
			}
		},
		"modelId": "ssss",
		"orgId": "yourOrgId",
		"updatePerson": "yj_test_customer",
		"updateTime": 1546612131000,
		"alertType": {
			"typeId": "dateType",
			"typeDesc": {
				"i18nValue": {
					"en_US": "dateType desc",
					"zh_CN": ""
				}
			},
			"tags": {
				
			},
			"updateTime": 0
		},
		"subAlertType": {
			"typeDesc": {
				"i18nValue": {
					"en_US": "dateType desc",
					"zh_CN": ""
				}
			},
			"tags": {
			},
			"updateTime": 0
		},
		"tags": {	
		}
	}]
}
```

## Java SDK调用示例

```java
public void testSearchAlertContent() {  
        SearchAlertContentRequest request = new SearchAlertContentRequest();  
        request.setOrgId(orgId);  
        request.setModelId("ssss");  
        Pagination pagination = new Pagination();  
        pagination.setPageNo(1);  
        pagination.setPageSize(1);  
        List<Sorter> sorterList = new ArrayList<>();  
        sorterList.add(new Sorter("contentId", Sorter.Order.DESC));  
	        pagination.setSorters(sorterList);  
	        request.setPagination(pagination);  
	        try {  
	            SearchAlertContentResponse response = Poseidon.config(PConfig.init().appKey(accessKey).appSecret(secretKey).debug())  
	                    .url("https://{apigw-address}")  
	                    .getResponse(request, SearchAlertContentResponse.class);  
	            Gson gson = new Gson();  
	            System.out.println(gson.toJson(response));
	        } catch (Exception e) {  
	            e.printStackTrace();  
	        }   
}
```
