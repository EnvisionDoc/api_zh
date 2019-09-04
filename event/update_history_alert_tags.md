# Update History Alert Tags

更新历史告警的标签内容。

## 请求格式

```
POST https://{apigw-address}/event-service/v2.1/history-alerts?action=updateTags
```

## 请求参数（URI）

| 名称          | 是否必须 | 数据类型 | 描述      |
|---------------|--------|----------|-----------|
| orgId         | true     | String    | 资产所属的组织ID。[如何获取orgId信息>>](/docs/api/zh_CN/latest/api_faqs#id-orgid-orgid)                |
                                                                 

## 请求参数（Body）

| 名称 | 位置（Path/Query） | 是否必须 | 数据类型 | 描述 |
|------|----------|--------------------|----|------|
| eventId       | Query            | true     | String     | 告警ID  |
| tags          | Query            | true     | Tags结构体 | 想要修改的标签内容|
| isPatchUpdate | Query            | true     | Boolean    | 是否全量更新。<br>当其值为true时，只更新参数中指定字段的值；<br>当其值为false时，更新所有字段的值，即未指定值的字段将被置空。 |


## 响应参数

| 名称  | 数据类型      | 描述               |
|-------|----------------|-------|
| data | Integer | 更新的条数|


## 输入输出示例

### 请求示例

```json
POST https://{apigw-address}/event-service/v2.1/history-alerts?action=updateTags&orgId=1c499110e8800000

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
public void testUpdateHistoryAlertTags(){  
    String accessKey = "4ced4f38-1ced-476e0a446215-a602-4307";  
    String secretKey = "0a446215-a602-4307-9ff2-3feed3e983ce";  
    UpdateHistoryAlertTagsRequest request = new UpdateHistoryAlertTagsRequest();  
    request.setOrgId("1c499110e8800000");  
    request.setEventId("20190612cf89cd96b0be4cafcc342d0dc2ac75a4");  
    Map<String,String> map = new HashMap<>();  
    map.put("tag000","000");  
    request.setTags(map);  
	    request.setIsPatchUpdate(true);  
	    request.headerParams().put("apim-accesskey","4ced4f38-1ced-476e0a446215-a602-4307");  
	    try {  
	        UpdateHistoryAlertTagsResponse response = Poseidon.config(PConfig.init().appKey(accessKey).appSecret(secretKey).debug())  
	                .url("https://{apigw-address}")  
	                .getResponse(request, UpdateHistoryAlertTagsResponse.class);
	        System.out.println(response);  
	    }catch(Exception e){  
	        System.out.print(e);  
	    }  
}
```