# Get Asset DI Data

获取指定设备在某段时间内的状态（DI）数据。

该API可获取一段时间内特定资产的状态数据，并只返回反映资产状态变化的数据。例如，一段时间内的原始数据如下所示：

```
Time       Status
10:01:14    0
10:01:30    0
10:03:45    0
10:12:23    1
10:13:34    0
10:15:24    1
10:17:25    1
```

返回的结果是：

```
Time       Status
10:01:14    0
10:12:23    1
10:13:34    0
10:15:24    1
```

## 请求格式

```
https://{apigw-address}/tsdb-service/v2.0/di?orgId={}&modelId={}&assetIds={}&measurepoints={}&startTime={}&endTime={}&accessKey={}
```

## 请求参数（URI）

| 名称          | 位置（Path/Query） | 是否必须 | 数据类型 | 描述      |
|---------------|------------------|----------|-----------|--------------|
| orgId         | Query            | true     | String    | 资产所属的组织ID。[如何获取orgId信息](/docs/api/zh_CN/latest/api_faqs#id-orgid-orgid)                                                                                                                                                                                                                            |
| modelId       | Query            | false    | String    | 资产所属模型ID。[如何获取modelId信息](/docs/api/zh_CN/latest/api_faqs#modelid-modelid)                                                                                                                                                                                                                           |
| assetIds      | Query            | true     | String    | 资产ID，支持查询多个资产，多个资产ID之间用英文逗号隔开。[如何获取Asset ID信息](/docs/api/zh_CN/latest/api_faqs#asset-id-assetid-assetid)                                                                                                                                                                                |
| measurepoints | Query            | true     | String    | 资产测点，支持多测点查询，各个测点间用逗号隔开；支持查询的（设备数*测点数）上限为3000。[如何获取pointId信息](/docs/api/zh_CN/latest/api_faqs#pointid-pointid)                                                                                                                                                                           |
| startTime     | Query            | true     | String    | 采样数据开始时间，支持UTC时间格式和local时间格式。 local时间格式为YYYY-MM-DD HH:MM:SS。当格式为本地时间时，应用按照设备所在地的当地时间进行查询。 UTC时间格式需要加入时区信息，例如：2019-06-01T00:00:00+08:00；当格式为UTC格式时，应用对所有资产按照统一的开始时间戳和结束时间戳进行查询。 |
| endTime       | Query            | true     | String    | 采样数据结束时间，格式必须与开始时间保持一致|
| accessKey     | Query            | true     | String    | 应用的服务账号，应用以`accessKey`进行鉴权以获得其被授权访问的数据。[如何获取accessKey信息](/docs/api/zh_CN/latest/api_faqs#accesskey-accesskey-accesskey)                                                                     


## 响应参数

| 名称  | 数据类型      | 描述               |
|-------|----------------|---------------------------|
| **items** | `List<Object>` | 资产数据列表。单设备单点的返回数据按时间升序排列。其中的Object结构体中存储着参数，详见[items](/docs/api/zh_CN/latest/tsdb_service/get_asset_di_data.html#id3)。

### items

例子：
```json
{
        "assetId": "4DXYH7nS",  			   //资产ID   
        "timestamp": 1560249312446,			   //数据时间戳
        "opentsdb_di_point_xxx": "1", 	   //测点标识符与测点数据
        "localtime": "2019-06-11 18:35:12"	  //数据本地时间标记
}
```

| 名称        | 数据类型 | 描述                           |
|---------------|-----------|--------------------------------------|
| localtime     | Object    | 数据本地时间标记，精确到秒，当入参时间格式为UTC格式时，该值为null。 |
| assetId       | Object    | 资产ID。                                             |
| pointId | Object    | 此参数是变量，表示测点的标识符与数据。                                    |
| timestamp     | Object    | 数据时间戳，UNIX时间，精确到秒。                                    |

## 错误码
有关错误码的描述，参见[通用错误码](overview#errorcode)。

## 示例 1

### 请求示例
Local时间格式：
```
https://{apigw-address}/tsdb-service/v2.0/di?orgId=o15504722874071&modelId=&assetIds=4DXYH7nS&measurepoints=opentsdb_di_point_xxx&startTime=2019-06-01%2000:00:00&endTime=2019-06-11%2023:00:00&accessKey=accessKey
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
        "opentsdb_di_point_xxx": "0",
        "timestamp": 1560249312446,
        "localtime": "2019-06-11 18:35:12"
      }
    ]
  }
}

```


## 示例 2

### 请求示例
UTC时间格式：
```
https://{apigw-address}/tsdb-service/v2.0/di?accessKey=accessKey&assetIds=4DXYH7nS&orgId=o15504722874071&measurepoints=opentsdb_di_point_xxx&startTime=2019-06-01T00:00:00%2B08:00&endTime=2019-06-11T23:00:00%2B08:00
```

### 返回示例

```json
{
    "status": 0,
    "requestId": "088a4bdc14ff4e1a8882a814ab539a9f",
    "msg": "success",
    "submsg": null,
    "data": {
        "items": [
            {
                "localtime": null,
                "opentsdb_di_point_xxx": "0",
                "assetId": "4DXYH7nS",
                "timestamp": 1560249312446
            }
        ]
    }
}

```

## Java SDK调用示例

```java
private static class Request extends PoseidonRequest{

    public void setQueryParam(String key, Object value){
        queryParams().put(key, value);
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
public void getAssetsStatusDataTest(){
    
    //1.在EnOS Console的左边导航栏中点击应用注册。
    //2.点击需调用API的应用，查看基本信息中的AccessKey即为appKey、SecretKey即为appSecret
    String accessKey = "29b8d283-dddd-4c31f0e3a356-0f80-4fdf";
    String secretKey = "f0e3a856-0fc0-4fdf-b1e5-b34da152879c";

    //新建一个request 然后把需要的参数传进去存在query的map中，key是参数名字，value是参数值
    Request request = new Request();
    request.setQueryParam("orgId", "o15504745674071");
    request.setQueryParam("modelId", "opentsdb_model_xxx");
    request.setQueryParam("assetIds","4DXYH7nS");
    request.setQueryParam("measurepoints", "opentsdb_di_point_xxx");
    request.setQueryParam("startTime", "2019-06-01 00:00:00"); //UTC时间格式为：2019-06-01T00:00:00%2B08:00
    request.setQueryParam("endTime", "2019-06-11 23:00:00");  //UTC时间格式为：2019-06-11T23:00:00%2B08:00
    request.setQueryParam("accessKey", accessKey);
    
    request.setMethod("GET");

    try {
        EnOSResponse<JSONObject> response = Poseidon.config(PConfig.init().appKey(accessKey).appSecret(secretKey).debug())
                .url("http://apim-gateway/tsdb-service/v2.0/di")
                .getResponse(request, EnOSResponse.class);
        System.out.println(response);
    } catch (Exception e) {
        e.printStackTrace();
    }
}
```
