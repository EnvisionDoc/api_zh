# Get Asset Latest Data

获取指定设备所有测点的最新数据。

## 请求格式

```
https://{apigw-address}/tsdb-service/v2.0/latest?orgId={}&assetIds={}&measurepoints={}&timeWindow={}&accessKey={}
```

## 请求参数（URI）

| 名称          | 位置（Path/Query） | 是否必须 | 数据类型 | 描述      |
|---------------|------------------|----------|-----------|--------------|
| orgId         | Query            | true     | String    | 资产所属的组织ID。[如何获取orgId信息>>](/docs/api/zh_CN/latest/api_faqs#id-orgid-orgid) |
| assetIds      | Query            | true     | String    | 资产ID，支持查询多个资产，多个资产ID之间用英文逗号隔开。[如何获取Asset ID信息>>](/docs/api/zh_CN/latest/api_faqs#asset-id-assetid-assetid) |
| measurepoints | Query            | true     | String    | 资产测点，支持多测点查询，各个测点间用逗号隔开；支持查询的（设备数*测点数）上限为3000。[如何获取测点（pointId）信息>>](/docs/api/zh_CN/latest/api_faqs#pointid-pointid) |
| timeWindow | Query            | false     | Integer    | 返回数据时间窗口设定，单位是分钟，最小值为0，不传则不约束。 |
| accessKey     | Query            | true     | String    | 应用的服务账号，应用以`accessKey`进行鉴权以获得其被授权访问的数据。[如何获取accessKey信息>>](/docs/api/zh_CN/latest/api_faqs#accesskey-accesskey-accesskey)                                                                     


## 响应参数

| 名称  | 数据类型      | 描述               |
|-------|----------------|---------------------------|
| **items** | `List<Object>` | 资产数据列表。单设备单点的返回数据按时间升序排列。其中的Object结构体中存储着参数，详见[items](/docs/api/zh_CN/latest/tsdb_service/get_asset_latest_data.html#id3)。

### items

例子：
```json
{
        "assetId": "4DXYH7nS",  			  //资产ID     
        "opentsdb_pi_point_xxx": "1.1236", 	 //测点标识符与测点数据     
        "timestamp": 1560249312446		//UNIX数据时间戳     
}
```

| 名称        | 数据类型 | 描述                           |
|---------------|-----------|--------------------------------------|
| assetId       | Object    | 资产ID |
| pointId | Object    | 此参数是变量，表示测点的标识符与数据。 |
| timestamp     | Object    | 数据时间戳，UNIX时间，精确到秒 |

## 错误码
有关错误码的描述，参见[通用错误码](overview#errorcode)。

## 示例 1

### 请求示例
Local时间格式：
```
https://{apigw-address}/tsdb-service/v2.0/latest?orgId=o15528761854851&assetIds=4DXYH7nS&measurepoints=opentsdb_pi_point_xxx&timeWindow=&accessKey=accessKey
```

### 返回示例

```json
{
  "status": 0,
  "requestId": null,
  "msg": "success",
  "submsg": null,
  "data": {
    "items": [
      {
        "assetId": "4DXYH7nS",
        "opentsdb_pi_point_xxx": 2.123,
        "timestamp": 1560249532446
      }
    ]
  }
}
```

## Java SDK调用示例


```java
private static class Request extends PoseidonRequest{

    public void setQueryParam(String key, Object value){
        queryEncodeParams().put(key, value);
    }

    public void setMethod(String method) {
        this.method = method;
    }

    private String method;

    @Override
    public String baseUri() {
        return "";
    }

    @Override
    public String method() {
        return method;
    }
}


@Test
public void getAssetsLatestDataTest(){
    
    //1.在EnOS Console的左边导航栏中点击应用注册。
    //2.点击需调用API的应用，查看基本信息中的AccessKey即为appKey、SecretKey即为appSecret
    String accessKey = "29b8d283-dddd-4c31f0e3a356-0f80-4fdf";
    String secretKey = "f0e3a856-0fc0-4fdf-b1e5-b34da152879c";

    //新建一个request 然后把需要的参数传进去存在query的map中，key是参数名字，value是参数值
    Request request = new Request();
    request.setQueryParam("orgId", "o15504745674071");
    request.setQueryParam("timeWindow", 10);
    request.setQueryParam("assetIds","4DXYH7nS");
    request.setQueryParam("measurepoints", "opentsdb_pi_point_xxx");
    request.setQueryParam("accessKey", accessKey);
    
    request.setMethod("GET");

    try {
        JSONObject response = Poseidon.config(PConfig.init().appKey(accessKey).appSecret(secretKey).debug())
                .url("http://apim-gateway/tsdb-service/v2.0/latest")
                .getResponse(request, JSONObject.class);
        System.out.println(response);
    } catch (Exception e) {
        e.printStackTrace();
    }
}
```
