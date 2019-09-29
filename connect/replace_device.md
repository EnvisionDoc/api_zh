# Replace Device

在资产ID（`assetId`）不改变的情况下更换一个设备。该接口将注销已注册设备的原始Device Key及Device Secret，为其重新分配Device Key，生成新的Device Secret，并重置设备为未激活状态。新设备可以通过更换后的Device Key连接EnOS，新旧设备的数据将通过资产ID进行关联。

## 请求格式

```
POST https://{apigw-address}/connect-service/v2.1/devices?action=replaceDevice
```

## 请求参数（URI）

.. note:: 以下非必须字段中，必须提供 ``assetId`` 或 ``productKey`` + ``deviceKey`` 的组合，用于指定设备。

>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>

| 名称          | 位置（Path/Query） | 是否必须 | 数据类型 | 描述      |
|---------------|------------------|----------|-----------|--------------|
| orgId         | Query            | True     | String    | 资产所属的组织ID。[如何获取orgId信息>>](/docs/api/zh_CN/2.0.9/api_faqs#id-orgid-orgid)                |
| assetId  | Query          | False      | String        | 资产ID。[如何获取Asset ID信息>>](/docs/api/zh_CN/2.0.9/api_faqs.html#asset-id-assetid-assetid) |
| productKey | Query         | False      | String         | Product Key      |
| deviceKey | Query         | False     | String          | Device Key          |



## 请求参数（Body）

| 名称          | 是否必须 | 数据类型 | 描述      |
|----------------|---------------|--------------------------|---|
|newDeviceKey|True|String|新设备的Device Key。支持英文字母、数字、连字符（-）、下划线（_）、圆点（.）及冒号（:），长度限制4~64。|



## 响应参数

| 名称 | 数据类型 | 描述         |
|-------------|-------------------|-----------------------------|
| data |    DeviceReplaceResult结构体        | 设备替换结果信息，见[DeviceReplaceResult结构体>>](replace_device#devicereplaceresult-devicereplaceresult)|


### DeviceReplaceResult结构体 <DeviceReplaceResult>

| 名称           | 数据类型 | 描述      |
|---------------|-----------|--------------|
| assetId    | String        | 资产ID|
| productKey   | String         | Product Key      |
| deviceKey  | String          | Device Key          |
| deviceSecret  | String          | 由系统分配的新设备的密钥          |


## 错误码

| 代码           | 描述      |
|----------------|--------------|
|11704|新旧Device Key相同|
|11702|新的Device Key在数据库中已存在|



## 示例 1

### 请求示例

```
POST http://{apigw-address}/connect-service/v2.1/devices?action=replaceDevice&orgId=1c499110e8800000&assetId=FsTV44kr
{
    "newDeviceKey":"yourNewDeviceKey"
}
```

### 返回示例

```json
{
    "code":0,
    "msg":"OK",
    "requestId":"fa377585-8240-4d1e-ad9d-a8d820873142",
    "data":{
        "assetId":"FsTV44kr",
        "productKey":"O658R5li",
        "deviceKey":"yourNewDeviceKey",
        "deviceSecret":"QbgsPK6eFyue2BRlCr3r"
    }
}
```

## Java SDK调用示例

```java
public class ReplaceDevice {
 
    public static void main(String[] args) {
 
        final String appKey = "4ced4f38-1ced-476e0a446215-a602-4307";
        final String appSecret = "0a446215-a602-4307-9ff2-3feed3e983ce";
        final String serverUrl = "http://{apigw-address}";
        final String orgId = "yourOrgId";
        final String assetId = "FsTV44kr";
 
        String newDeviceKey = "abcdefg123";
 
        ReplaceDeviceRequest request = new ReplaceDeviceRequest();
        request.setOrgId(orgId);
        request.setAssetId(assetId);
        request.setNewDeviceKey(newDeviceKey);
 
        ReplaceDeviceResponse response = Poseidon.config(PConfig.init().appKey(appKey).appSecret(appSecret).debug())
                .url(serverUrl)
                .getResponse(request, ReplaceDeviceResponse.class);
 
        DeviceReplaceResult replaceResult = response.getData();
        String newDeviceSecret = replaceResult.getDeviceSecret();
        System.out.println(newDeviceSecret);
        System.out.println(response);
        System.out.println(response.getData()); 
    } 
}
```