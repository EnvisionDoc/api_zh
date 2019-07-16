# Get Asset

根据资产ID获取资产数据。

## 请求格式

```
https://{apigw-address}/asset-service/v2.1/assets?action=get
```

## 请求参数（URI）

| 名称          | 位置（Path/Query） | 是否必须 | 数据类型 | 描述      |
|---------------|------------------|----------|-----------|--------------|
| orgId         | Query            | true     | String    | 资产所属的组织ID。[如何获取orgId信息](/docs/api/zh_CN/latest/api_faqs#id-orgid-orgid)                |
| assetId       | Query            | true    | String    | 资产ID。[如何获取Asset ID信息](/docs/api/zh_CN/latest/api_faqs.html#asset-id-assetid-assetid)        |


## 响应参数

| 名称  | 数据类型 | 描述 |
|------|------------|-----------|-------------|
| data    |asset结构体 | 资产。见[asset结构体](/docs/api/zh_CN/latest/asset/get_asset.html#id3)。    |


### asset结构体

| 名称  |  数据类型      | 描述               |
|-------|---------|---------------------------|
| assetId |  String | 资产ID|
| orgId      | String    | 资产所属的组织ID|
| name | StringI18n |该资产的各语言名称|
| description   | String | 资产描述|
|attributes   |Map  |资产所属的模型属性。<br>`Key`为属性ID，String类型。Value的类型取决于模型中这个属性的定义|
|timezone  |  String  |时区|
|modelId|String|资产所属模型ID|
|modelIdPath|String|模型继承路径。<br>例如：/Turbine/Double_Feed_Turbine|
|tags|Map<br>（Key为String, Value为String）|用户自定义标签|


## 错误码

见[公共返回码](/docs/api/zh_CN/latest/overview.html#id8)。



## 示例 1

### 请求示例

```
GET
https://{apigw-address}/asset-service/v2.1/assets?action=get&orgId=1c499110e8800000&assetId=TZ8AOlJU

```

### 返回示例

```json
{
  "msg": "OK",
  "code": 0,
  "data": {
    "modelId": "planet",
    "assetId": "TZ8AOlJU",
    "timezone": "+00:00",
    "name": {
      "i18nValue": {
        "en_US": "English name ",
        "zh_CN": "Chinese name"
                   }
      "defaultValue": "venus!"
            },
    "attributes": {
      "system": "Solar System"
                  },
    "modelIdPath": "/planet",
    "orgId": "yourOrgId",
    "desc": null,
    "tags": {}
           },
  "requestId": "9a5cfbac-b2f8-4a37-b38d-8bccdd77d073"
}
```


## Java SDK调用示例

```java
public class GetAsset {
    private static String accessKey = "4ced4f38-1ced-476e0a446215-a602-4307";
    private static String secretKey = "0a446215-a602-4307-9ff2-3feed3e983ce";
    private static String orgId = "1c499110e8800000";
    private static String url = "https://{apigw-address}";

    public static void main(String[] args) {
        GetAssetRequest request = new GetAssetRequest();
        request.setOrgId(orgId);
        request.setAssetId("XBOBqC1O");

        GetAssetResponse response = Poseidon.config(PConfig.init().appKey(accessKey)
                .appSecret(secretKey).debug())
                .url(url)
                .getResponse(request, request.getResponseClass());
        System.out.println(response.getCode());
    }
}
```
