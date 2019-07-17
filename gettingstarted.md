# EnOS API 快速入门

该教程通过一个例子带着你完成你的第一个EnOS API调用任务。

## 前提条件

调用EnOS API需完成以下准备：

**获取服务账号**

已获取用于调用API时，用于身份授权的服务账号。详细步骤，参考 [API鉴权](overview#authentication)。

**获取资源权限**

服务账号已取得系统中相关资源的访问权限。详细信息，参考 [管理服务账号](/docs/iam/zh_CN/latest/howto/service_account/managing_service_account.html)。

**准备开发环境**

安装EnOS提供的SDK，准备调用API的基础环境。参考以下详细介绍：

### 使用Java调用SDK
使用Java调用SDK，需要安装Java core SDK（Poseidon）V0.1.7及以上版本。Poseidon支持Java 7及以上版本。

使用Java core SDK调用接入和资产等服务，需要安装Device And Asset API Pojo SDK V0.2.0及以上版本。

#### 安装方法
**Java core SDK（Poseidon）**

访问 [Maven仓库](https://mvnrepository.com/artifact/com.envisioniot/apim-poseidon/0.1.7)，下载Poseidon Jar安装包，在应用中引入Jar安装包。如果应用使用 `pom` 工程，则在 `pom.xml` 文件中加入以下依赖：

```xml
<dependency>
  <groupId>com.envisioniot</groupId>
  <artifactId>apim-poseidon</artifactId>
  <version>0.1.7</version>
</dependency>
```
**Device And Asset API Pojo SDK**

访问 [Maven仓库](https://search.maven.org/artifact/com.envisioniot/enos-dm-api-pojo/0.2.0/jar)，下载Jar安装包，在应用中引入Jar安装包。如果应用使用 `pom` 工程，则在 `pom.xml` 文件中加入以下依赖：

```
<dependency>
  <groupId>com.envisioniot</groupId>
  <artifactId>enos-dm-api-pojo</artifactId>
  <version>0.2.0</version>
</dependency>
```

#### 使用方法

**同步请求**

1. 关闭API日志功能，调用API后仅返回调用结果。示例代码如下：

   ```
   Poseidon.config(PConfig.init().appKey(accessKey).appSecret(secretKey))
           .url("https://{apigw-address}/{service-name}/{api-version}/{api_name}?{param1=value1&param2=value2}")
           .method("GET")
           .sync();
   ```

2. 开启API日志功能，调用API后返回带时间戳的调用参数和调用结果。示例代码如下：

   ```
   Poseidon.config(PConfig.init().appKey(accessKey).appSecret(secretKey).debug())
           .url("https://{apigw-address}/{service-name}/{api-version}/{api_name}?{param1=value1&param2=value2}")
           .method("GET")
           .sync();
   ```

3. POST请求，示例代码如下：

   ```
   Poseidon.config(PConfig.init().appKey(accessKey).appSecret(secretKey).debug())
               .url("https://{service-name}/{api-version}/{api_name}?{param1=value1&param2=value2}")
               .method("POST")
               .header("Content-Type", "application/json")
               .requestBody(
                   "{\n" + "  \"op\": \"pl\",\n" + "  \"offset\": 0,\n" + "  \"limit\": 10\n" + "}")
               .sync();
   ```

   .. note:: Request header为可选，可按需将请求内容的类型等规范包含在header中。

   

**异步请求**

示例代码如下：

```java
Poseidon.config(PConfig.init().appKey(accessKey).appSecret(secretKey))
        .url("https://{apigw-address}/{service-name}/{api-version}/{api_name}?{param1=value1&param2=value2}")
        .method("GET").async( new PoseidonListener() {
              @Override
              public void onFailure(String errorMessage) {
                // TODO
              }

              @Override
              public void onResponse(String body) {
                // TODO
              }
            });
```

**支持Request和Response**

Request内置支持Header，Query，RequestBody，Path参数。Request和Response的使用方法，参考[示例3 - 使用Request和Response](gettingstarted#id9)。

**异常处理**

调用API的异常情况，可捕获PoseidonException异常查看具体问题。API服务报错，可根据错误码，参考各API的说明文档。

PoseidonException返回的常见报错信息和说明如下：

| 错误码 | 错误码描述            | 错误信息                           | 错误原因             |
| ------ | --------------------- | ---------------------------------- | -------------------- |
| 401    | Unauthorized          | Invalid authentication credentials | 身份验证失败         |
| 400    | Bad Request           | Cannot process request body        | 获取request body失败 |
| 403    | Forbidden             | Your IP address is not allowed     | IP地址不允许访问     |
| 413    | Payload Too Large     | Request size limit exceeded        | 超出请求大小限制     |
| 429    | Too Many Requests     | API rate limit exceeded            | 超出API请求次数限制  |
| 500    | Internal Server Error | An unexpected error occurred       | 查询缓存失败         |
| 503    | Service unavailable   | Service unavailable                | 服务禁止访问         |

### 使用Python调用SDK
使用Python调用SDK，需要安装Python core SDK（Athena）V0.1.1及以上版本。Athena支持Python 3.6及以上版本。

#### 安装方法

通过以下pip命令安装：

```
pip install aphrodite
```

#### 使用方法

**Query** 

```python
from poseidon import poseidon

accessKey = 'accessKey'
secretKey = 'secretKey'

url = 'https://{apigw-address}/{service-name}/{api-version}/{api_name}?{param1=value1&param2=value2}'

req = poseidon.urlopen(accessKey, secretKey, url)
print(req)
```
**Header**

```python
from poseidon import poseidon

accessKey = 'accessKey'
secretKey = 'secretKey'

url = 'https://{apigw-address}/{service-name}/{api-version}/{api_name}?{param1=value1&param2=value2}'

header={}

req = poseidon.urlopen(accessKey, secretKey, url, None, header)
print(req)
```

**Body**

```python
from poseidon import poseidon

accessKey = 'accessKey'
secretKey = 'secretKey'

url = 'https://{apigw-address}/{service-name}/{api-version}/{api_name}?{param1=value1&param2=value2}'

data = {"username": "abc", "password": "123"}

req = poseidon.urlopen(accesskey, secretkey, url, data)
print(req)
```

## 调用EnOS API

开发环境准备完成后，参考各API接口文档中的参数说明和调用示例，调用API。

### 示例1 - GET方法 

以下示例为使用Java core SDK调用*Get Asset* API获取资产详细信息（关闭API日志功能）：

```java
import com.envision.apim.poseidon.config.PConfig;
import com.envision.apim.poseidon.core.Poseidon;

public class GetAsset {
    public static void main(String[] args) {

        String accessKey = "{access_key_of_the_application}";
        String secretKey = "{secret_key_of_the_application}";

        String response = Poseidon.config(PConfig.init().appKey(accessKey).appSecret(secretKey))
                .url("https://{apigw-address}/asset-service/v2.1/assets?action=get&orgId={org_id}&assetId={asset_id}")
                .method("GET")
                .sync();
        System.out.println(response);
        }
    }
```

以上示例代码运行完成后，返回数据示例为：

```
{
  "msg": OK,
  "code": 0,
  "data": {
    "modelId": "model_id",
    "assetId": "asset_id",
    "timezone": "+08:00",
    "name": {
      "i18nValue": {},
      "defaultValue": "asset_name"
    },
    "attributes": {
      "system": "System"
    },
    "modelIdPath": null,
    "orgId": "yourOrgId",
    "desc": null,
    "tags": {}
  },
  "requestId": "9a5cfbac-b2f8-4a37-b38d-8bccdd77d073"
}
```

### 示例2 - POST方法

以下示例为使用Java core SDK调用*Update Asset* API更新资产的名称、描述、属性、时区、标签信息（开启API日志功能）：

```java
import com.envision.apim.poseidon.config.PConfig;
import com.envision.apim.poseidon.core.Poseidon;

public class UpdateAsset {
    public static void main(String[] args) {

        String accessKey = "{access_key_of_the_application}";
        String secretKey = "{secret_key_of_the_application}";
        
        String data = "{\"asset\":{\"assetId\":\"{asset_id}\",\"name\":{\"defaultValue\":\"Device_Name\",\"i18nValue\":{\"en_US\":\"Device_Name\",\"zh_CN\":\"Chinese name\"}},\"description\":\"Device_Description\",\"attributes\":{\"Brand\":\"Brand_Name\"},\"timezone\":\"+07:00\",\"tags\":{\"year\":\"2019\",\"site\":\"Site_Name\"}}}";

        String response = Poseidon.config(PConfig.init().appKey(accessKey).appSecret(secretKey).debug())
                .url("https://{apigw-address}/asset-service/v2.1/assets?action=update&orgId={org_id}")
                .method("POST")
                .requestBody(data)
                .sync();
        System.out.println(response);
    }
}
```

以上示例代码运行完成后，返回数据示例为：

```
2019-7-10 16:35:12 [Poseidon] url: https://{apigw-address}/asset-service/v2.1/assets?action=update&orgId={org_id}
2019-7-10 16:35:12 [Poseidon] method: POST
2019-7-10 16:35:12 [Poseidon] headers: {}
2019-7-10 16:35:12 [Poseidon] requestBody: {"asset":{"assetId":"{asset_id}","name":{"defaultValue":"Device_Name","i18nValue":{"en_US":"Device_Name","zh_CN":"Chinese name"}},"description":"Device_Description","attributes":{"Brand":"Brand_Name"},"timezone":"+07:00","tags":{"year":"2019","site":"Site_Name"}}}
2019-7-10 16:35:13 [Poseidon] responseBody: {"code":0,"msg":"OK","requestId":"9d6b9869-4ffd-4964-a8ff-d150a0d1a91f","data":null}
```

### 示例3 - 使用Request和Response

以下示例为使用Java core SDK和Device And Asset API Pojo SDK调用*Update Asset* API更新资产的描述、属性、时区信息（开启API日志功能）：

```java
import com.envision.apim.poseidon.config.PConfig;
import com.envision.apim.poseidon.core.Poseidon;
import com.envisioniot.enos.asset_service.v2_1.UpdateAssetRequest;
import com.envisioniot.enos.asset_service.v2_1.UpdateAssetResponse;
import com.envisioniot.enos.asset_service.vo.AssetUpdateVo;

import java.util.HashMap;
import java.util.Map;

public class UpdateAsset {
    private static String accessKey = "{access_key_of_the_application}";
    private static String secretKey = "{secret_key_of_the_application}";
    private static String orgId = "{org_id}";
    private static String url = "https://{apigw-address}";

    public static void main(String[] args) {
        UpdateAssetRequest request = new UpdateAssetRequest();
        request.setOrgId(orgId);

        AssetUpdateVo asset = new AssetUpdateVo();
        asset.setAssetId("{asset_id}");
        Map<String, Object> newAttrs = new HashMap<>();
        newAttrs.put("Brand","Brand_Name");
        asset.setAttributes(newAttrs);
        asset.setDescription("Device_Description");
        asset.setTimezone("+08:00");

        request.setAsset(asset);
        request.setIsPatchUpdate(true);

        UpdateAssetResponse response = Poseidon.config(PConfig.init().appKey(accessKey).appSecret(secretKey).debug())
                .url(url)
                .getResponse(request, request.getResponseClass());
        System.out.println(response);
    }
}
```

以上示例代码运行完成后，返回数据示例为：

```
2019-7-10 16:45:00 [Poseidon] url: https://{apigw-address}/asset-service/v2.1/assets?action=update&isPatchUpdate=true&orgId={org_id}
2019-7-10 16:45:00 [Poseidon] method: POST
2019-7-10 16:45:00 [Poseidon] headers: {}
2019-7-10 16:45:00 [Poseidon] requestBody: {"asset":{"assetId":"{asset_id}","attributes":{"Brand":"Brand_Name"},"description":"Device_Description","timezone":"+08:00"}}
2019-7-10 16:45:01 [Poseidon] responseBody: {"code":0,"msg":"OK","requestId":"4c1a6da8-bd89-4001-b8fd-5fa65ab816f2","data":null}
```

