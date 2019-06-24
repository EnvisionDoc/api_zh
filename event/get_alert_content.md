# Get Alert Content

根据组织ID和内容ID获取告警内容。

## 请求格式

```
GET https://apigw-address/event-service/v2.1/alert-contents action=get&orgId=1c499110e8800000
```

## 请求参数（URI）

| 名称          | 位置（Path/Query） | 是否必须 | 数据类型 | 描述      |
|---------------|------------------|----------|-----------|--------------|
| orgId         | Query            | true     | String    | 资产所属的组织ID。[如何获取orgId信息](/docs/api/zh_CN/latest/api_faqs#orgid-orgid)                |
| contentId         | Query            | true     | String    | 告警内容ID。                |
                                                                 

## 响应参数

| 名称  | 数据类型      | 描述               |
|-------|----------------|---------------------------|
| data | AlertContent结构体Array | 告警内容|

### AlertContent结构体

| 名称  | 数据类型      | 描述               |
|----------------|-----------------------|----------|
| contentId| String           | 内容ID                 |
| contentDesc | StringI18n | 告警内容描述。为一个国际化名称结构体。详见[国际化名称结构体](/docs/api/zh_CN/latest/api_faqs.html#id3)                |
| modelId| String           | 模型ID                 |
| orgId          | String                | 资产所属的组织ID。[如何获取orgId信息](/docs/api/zh_CN/latest/api_faqs#orgid-orgid)|
| alertType  | AlertType结构体  | 告警类型               |
| subAlertType| AlertType结构体  | 子告警类型             |
| tags| Tag结构体        | 用户自定义告警内容标签 |
| updatePerson| String           | 更新人员名称           |
| updateTime| Long             | 最后一次更新时间       |



## 输入输出示例

### 请求示例

```json
GET https://apigw-address/event-service/v2.1/alert-contents?action=get &contentId=doubleContentuid&orgId=1c499110e8800000
```

### 返回示例

```json
{
	"code": 0,
	"msg": "OK",
	"requestId": "f40fbb09-ce20-463f-bb18-6659a8bd6926",
	"data": {
		"contentId": "doubleContentuid",
		"contentDesc": {
			"i18nValue": {
				"en_US": "doubleContentuid desc",
				"zh_CN": ""
			}
		},
		"modelId": "ssss",
		"orgId": "1c499110e8800000",
		"updatePerson": "yj_test_customer",
		"updateTime": 1546612131000,
		"alertType": {
			"typeId": "doubleType",
			"typeDesc": {
				"i18nValue": {
					"en_US": "doubleType desc",
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
					"en_US": "doubleType desc",
					"zh_CN": ""
				}
			},
			"tags": {
				
			},
			"updateTime": 0
		},
		"tags": {
			
		}
	}
}
```

## Java SDK调用示例

```java
1.	public void testGetAlertContent() {  
2.	        final String contentId = "doubleContentuid";  
3.	        GetAlertContentRequest request = new GetAlertContentRequest();  
4.	        request.setOrgId(orgId);  
5.	        request.setContentId(contentId);  
6.	  
7.	        try {  
8.	            GetAlertContentResponse response = Poseidon.config(PConfig.init().appKey(appKey).appSecret(appSecret).debug())  
9.	                    .url("https://apigw-address")  
10.	                    .getResponse(request, GetAlertContentResponse.class);  
11.	            Gson gson = new Gson();  
12.	            System.out.println(gson.toJson(response));  
13.	            if (response.getCode() == 0) {  
14.	                System.out.println(response.getData());  
15.	            }  
16.	        } catch (Exception e) {  
17.	            e.printStackTrace();  
18.	        }  
19.	  
20.	    }
```