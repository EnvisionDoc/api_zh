# Update History Alert Tags

更新历史告警的tag。

## 请求格式

```
POST https://apigw-address/event-service/v2.1/history-alerts?action=updateTags
```

## 请求参数（URI）

| 名称          | 是否必须 | 数据类型 | 描述      |
|---------------|--------|----------|-----------|
| orgId         | true     | String    | 资产所属的组织ID。[如何获取orgId信息](/docs/api/zh_CN/latest/api_faqs#orgid-orgid)                |
                                                                 

## 请求参数（Body）
| 名称 | 位置（Path/Query） | 是否必须 | 数据类型 | 描述 |
|------|----------|--------------------|----|------|
| eventId       | Query            | true     | String     | 告警id  |
| tags          | Query            | true     | Tags结构体 | 想要修改的tag map|
| isPatchUpdate | Query            | true     | Boolean    | 是否全量更新，false为全量修改，true为非全量修改。 |


## 响应参数

| 名称  | 数据类型      | 描述               |
|-------|----------------|---------------------------|
| data | Integer | 更新的条数|


## 输入输出示例

### 请求示例

```json
POST https://apigw-address/event-service/v2.1/history-alerts?action=updateTags&orgId=1c499110e8800000

{
	"eventId": "20190612cf89cd96b0be4cafcc342d0dc2ac75a4",
	"isPatchUpdate": true,
	"tags": {
		"tag000": "000"
	}
}

```

### 返回示例

```json
{
	"code": 0,
	"msg": "success",
	"requestId": "4873095e-621d-4cfd-bc2c-edb520f574ea",
	"data": 1
}
```

## Java SDK调用示例

```java
1.	public void testUpdateHistoryAlertTags(){  
2.	    String appKey = "4ced4f38-1ced-476e0a446215-a602-4307";  
3.	    String appSecret = "0a446215-a602-4307-9ff2-3feed3e983ce";  
4.	    UpdateHistoryAlertTagsRequest request = new UpdateHistoryAlertTagsRequest();  
5.	    request.setOrgId("1c499110e8800000");  
6.	    request.setEventId("20190612cf89cd96b0be4cafcc342d0dc2ac75a4");  
7.	    Map<String,String> map = new HashMap<>();  
8.	    map.put("tag000","000");  
9.	    request.setTags(map);  
10.	    request.setIsPatchUpdate(true);  
11.	    request.headerParams().put("apim-accesskey","4ced4f38-1ced-476e0a446215-a602-4307");  
12.	    try {  
13.	        UpdateHistoryAlertTagsResponse response = Poseidon.config(PConfig.init().appKey(appKey).appSecret(appSecret).debug())  
14.	                .url("https://apigw-address")  
15.	                .getResponse(request, UpdateHistoryAlertTagsResponse.class);
16.	        System.out.println(response);  
17.	    }catch(Exception e){  
18.	        System.out.print(e);  
19.	    }  
20.	}
```