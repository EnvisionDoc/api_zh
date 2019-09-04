# Get Organization

获取组织信息。

## 请求格式

```
POST https://{apigw-address}/iam/v1/api/open/organization/get
```

## 请求参数(URI)

| 名称 | 位置 | 是否必须 | 数据类型 | 描述      |
|---------------|------------------|----------|-----------|--------------|
| Authorization | Header | True | String | Bearer Token   |
| Content-Type | Header |True |application/json| 返回内容的内容类型|

## 请求参数(Body)

| 名称          | 是否必须 | 数据类型 | 描述      |
|------------------|---------------|----------|---|
| id  | True | String | 资产所属的组织ID。[如何获取orgId信息>>](/docs/api/zh_CN/latest/api_faqs#id-orgid-orgid)  |


## 响应参数

| 名称| 数据类型 | 描述         |
|-------------|---------|----------------|
| organization |   Organization结构体 |    组织信息，见[Organization结构体](get_org#organization-org)。 |  


### Organization结构体 <org>

| 名称| 数据类型 | 描述         |
|-------------|---------------|---------------|
| code  |String |组织标识符，如营业执照号码 |
| createTime   | String    | 组织的创建时间    |
| createdByUserId   | String    | 组织创建者的用户ID  |
| description  |String |组织描述 |
| domain  |String |大数据平台账号 |
| id  |String | 组织ID |
| name  | String| 组织名称 |
| ownerId   | String    | 组织所有者的用户ID    |




## 示例

### 请求示例

```
POST https://{apigw-address}/iam/v1/api/open/organization/get
requestBody: {"id":"yourOrgId"}
header:{
        "Authorization":"yourBearerToken",
        "Content-Type":"application/json"
        }
```

### 返回示例

```json
{
  "code": 200,
  "failed": false,
  "message": "",
  "organization": {
    "code": "",
    "createTime": "2019-05-14 08:33:18.0",
    "createdByUserId": "u15440200922941",
    "description": "",
    "domain": "db_portal_test01",
    "id": "yourOrgId",
    "name": "portal_test01",
    "ownerId": "u15578227990211"
  },
  "status": 0,
  "successful": true
}
```

## Java SDK调用示例

```java
public class GetOrganization{

    public static String SESSION_ID = "yourBearerToken";

    public static final String ORGANIZATIONID = "yourOrgId";

    public static void main(String[] args) {
        System.out.println("ListOrganization Test");
        OrganizationGetRequest organizationGetRequest = new OrganizationGetRequest(SESSION_ID, ORGANIZATIONID);
        OrganizationGetResponse response = getPoseidon().getResponse(organizationGetRequest, OrganizationGetResponse.class);

        System.out.println("OrganizationGetResponse res; " + JSON.toJSONString(response));
        assertNotNull("Response should not be null", response);

    }
}
```
