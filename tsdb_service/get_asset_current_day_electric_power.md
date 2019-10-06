# Get Asset Current Day Electric Power

获取指定设备从本地时间0点开始到当前时间已累计的电量数据。

## 请求格式

```
https://{apigw-address}/tsdb-service/v2.0/electric-power/current-day?orgId={}&modelId={}&assetIds={}&measurepoints={}&accessKey={}
```

## 请求参数（URI）

| 名称          | 位置（Path/Query） | 是否必须 | 数据类型 | 描述      |
|---------------|------------------|----------|-----------|--------------|
| orgId         | Query            | true     | String    | 资产所属的组织ID。[如何获取orgId信息>>](/docs/api/zh_CN/latest/api_faqs#id-orgid-orgid)|
| modelId       | Query            | false    | String    | 资产所属模型ID。[如何获取modelId信息>>](/docs/api/zh_CN/latest/api_faqs#modelid-modelid)|
| assetIds      | Query            | true     | String    | 资产ID，支持查询多个资产，多个资产ID之间用英文逗号隔开。[如何获取Asset ID信息>>](/docs/api/zh_CN/latest/api_faqs#asset-id-assetid-assetid)|
| measurepoints | Query            | true     | String    | 资产测点，支持多测点查询，各个测点间用逗号隔开；支持查询的（设备数*测点数）上限为3000。[如何获取测点（pointId）信息>>](/docs/api/zh_CN/latest/api_faqs#pointid-pointid)|
| accessKey     | Query            | true     | String    | 应用的服务账号，应用以`accessKey`进行鉴权以获得其被授权访问的数据。[如何获取accessKey信息>>](/docs/api/zh_CN/latest/api_faqs#accesskey-accesskey-accesskey)                                                                     

## 响应参数

| 名称  | 数据类型      | 描述               |
|-------|----------------|---------------------------|
| **items** | `List<Object>` | 资产数据列表。单设备单点的返回数据按时间升序排列。其中的Object结构体中存储着参数，详见[items](/docs/api/zh_CN/latest/tsdb_service/get_asset_current_day_electric_power.html#id3)。

### items

例子：
```json
{
        "assetId": "4DXYH7nS", 			//资产ID			
        "timestamp": 1560329220000,	 //UNIX数据时间戳	        
        "opentsdb_pi_point_xxx": "10.615000000000002"  //电量的sum当天聚合与数据
}
```

| 名称        | 数据类型 | 描述                           |
|---------------|-----------|--------------------------------------|
| assetId       | Object    | 资产ID |
| pointId | Object    | 此参数是变量，表示测点的标识符与数据。 此处数据是电量pi的sum当天聚合。|
| timestamp     | Object    | 数据时间戳，UNIX时间，精确到秒 |


## 错误码
有关错误码的描述，参见[通用错误码](overview#errorcode)。

## 示例

### 请求示例
```
https://{apigw-address}/tsdb-service/v2.0/electric-power/current-day?orgId=o15504722874071&modelId=&assetIds=4DXYH7nS&measurepoints=opentsdb_pi_point_xxx&accessKey=accessKey
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
        "timestamp": 1560329220000,
        "sum(opentsdb_pi_point_xxx)": "10.615000000000002"
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
public void getAssetsCurrentDayElectricPowerTest(){
    
    //1.在EnOS Console的左边导航栏中点击应用注册。
    //2.点击需调用API的应用，查看基本信息中的AccessKey即为appKey、SecretKey即为appSecret
    String accessKey = "29b8d283-dddd-4c31f0e3a356-0f80-4fdf";
    String secretKey = "f0e3a856-0fc0-4fdf-b1e5-b34da152879c";

    //新建一个request 然后把需要的参数传进去存在query的map中，key是参数名字，value是参数值
    Request request = new Request();
    request.setQueryParam("orgId", "o15504745674071");
    request.setQueryParam("modelId", "model_xxx");
    request.setQueryParam("assetIds","4DXYH7nS");
    request.setQueryParam("measurepoints", "opentsdb_pi_point_xxx");
    request.setQueryParam("accessKey", accessKey);
    
    request.setMethod("GET");

    try {
        JSONObject response = Poseidon.config(PConfig.init().appKey(accessKey).appSecret(secretKey).debug())
                .url("http://apim-gateway/tsdb-service/v2.0/electric-power/current-day")
                .getResponse(request, JSONObject.class);
        System.out.println(response);
    } catch (Exception e) {
        e.printStackTrace();
    }
}
```
