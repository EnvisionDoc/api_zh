# Search Command

按照筛选条件查询云端向设备发送的指令信息。

## 请求格式

```
https://{apigw-address}/connect-service/v2.1/commands?action=search
```

## 请求参数（URI）

.. note:: 以下非必须字段中，必须提供 ``assetId`` 或 ``productKey`` + ``deviceKey`` 的组合，用于指定设备。

>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>

| 名称          | 位置（Path/Query） | 是否必须 | 数据类型 | 描述      |
|---------------|------------------|----------|-----------|--------------|
| orgId         | Query            | True     | String    | 资产所属的组织ID。[如何获取orgId信息>>](/docs/api/zh_CN/latest/api_faqs#id-orgid-orgid)                |
| assetId  | Query            | False   | String         | 资产ID。[如何获取Asset ID信息>>](/docs/api/zh_CN/latest/api_faqs.html#asset-id-assetid-assetid) |
| productKey | Query          | False       | String       | Product Key      |
| deviceKey | Query           | False      | String       | Device Key          |


## 请求参数（Body）

| 名称 | 是否必须 | 数据类型 | 描述 |
|----------------|----------|--------------------|----|
| expression     | false    | String| 查询表达式，支持类sql的查询。目前支持查询的字段是`state`、`commandName`、`createTime`。<br>`state`支持等于（=）运算符。<br>`commandName`支持模糊匹配，必须提供`locale`，如commandName.zh_CN或commandName.en_US。<br>`createTime`支持用>、=和<运算符来指定时间范围。[如何使用查询表达式>>](/docs/api/zh_CN/latest/api_faqs.html#id1) |
| pagination    | false     | Pagination请求结构体 | 分页参数。默认分页大小为100条记录。返回结果按照命令的`createTime`倒序排序。见[Pagination请求结构体>>](/docs/api/zh_CN/latest/overview.html?highlight=pagination#pagination) |
| projection  | false    | Projection结构体 | 指定对返回结果的裁剪。详见[projection参数如何对结果集做裁剪>>](/docs/api/zh_CN/latest/api_faqs.html#projection)  |



## 响应参数

| 名称 | 数据类型 | 描述         |
|-------------|-------------------|-----------------------------|
| data |    getCommand结构体        | 符合条件的信息，见[getCommand结构体>>](get_command#id3) |



## 示例 1

### 请求示例

```
POST
https://apigw-address/connect-service/v2.1/commands?action=search&deviceKey=zm_mqtt&productKey=bXuuAiku&orgId=yourOrgId
{
    "expression": "state = 2",
    "pagination": {"pageNo":1,"pageSize":5}
}
```

### 返回示例

```json
{
  "code": 0,
  "msg": "OK",
  "requestId": "df57e058-0d8b-4700-9e38-ef30132c155f",
  "data": [
    {
      "commandId": "2322417636630765568",
      "orgId": "yourOrgId",
      "productKey": "yourProductKey",
      "deviceKey": "yourDeviceKey",
      "assetId": "sxH2DD6f",
      "createTime": 1565688731159,
      "createLocaltime": "2019-08-13 09:32:11",
      "commandType": 1,
      "commandName": {
        "defaultValue": "Int_value",
        "i18nValue": {
          "en_US": "Int_value"
        }
      },
      "timeout": 30,
      "pendingTtl": 100,
      "state": 2,
      "tslIdentifier": "Int_value",
      "inputData": 111,
      "outputData": null
    },
    {
      "commandId": "2322417598073053184",
      "orgId": "yourOrgId",
      "productKey": "yourProductKey",
      "deviceKey": "yourDeviceKey",
      "assetId": "sxH2DD6f",
      "createTime": 1565688726563,
      "createLocaltime": "2019-08-13 09:32:06",
      "commandType": 2,
      "commandName": {
        "defaultValue": "service522",
        "i18nValue": {
          "en_US": "service522"
        }
      },
      "timeout": 10,
      "pendingTtl": 600,
      "state": 2,
      "tslIdentifier": "service522",
      "inputData": {
        "service_input": 555
      },
      "outputData": null
    },
    {
      "commandId": "2322417559066025984",
      "orgId": "yourOrgId",
      "productKey": "yourProductKey",
      "deviceKey": "yourDeviceKey",
      "assetId": "sxH2DD6f",
      "createTime": 1565688721913,
      "createLocaltime": "2019-08-13 09:32:01",
      "commandType": 2,
      "commandName": {
        "defaultValue": "service522",
        "i18nValue": {
          "en_US": "service522"
        }
      },
      "timeout": 10,
      "pendingTtl": 600,
      "state": 2,
      "tslIdentifier": "service522",
      "inputData": {
        "service_input": 555
      },
      "outputData": null
    },
    {
      "commandId": "2322417537678745600",
      "orgId": "yourOrgId",
      "productKey": "yourProductKey",
      "deviceKey": "yourDeviceKey",
      "assetId": "sxH2DD6f",
      "createTime": 1565688719363,
      "createLocaltime": "2019-08-13 09:31:59",
      "commandType": 1,
      "commandName": {
        "defaultValue": "Int_value",
        "i18nValue": {
          "en_US": "Int_value"
        }
      },
      "timeout": 10,
      "pendingTtl": 600,
      "state": 2,
      "tslIdentifier": "Int_value",
      "inputData": 111,
      "outputData": null
    },
    {
      "commandId": "2322417518334615552",
      "orgId": "yourOrgId",
      "productKey": "yourProductKey",
      "deviceKey": "yourDeviceKey",
      "assetId": "sxH2DD6f",
      "createTime": 1565688717057,
      "createLocaltime": "2019-08-13 09:31:57",
      "commandType": 1,
      "commandName": {
        "defaultValue": "Int_value",
        "i18nValue": {
          "en_US": "Int_value"
        }
      },
      "timeout": 10,
      "pendingTtl": 600,
      "state": 2,
      "tslIdentifier": "Int_value",
      "inputData": 111,
      "outputData": null
    }
  ],
  "pagination": {
    "sortedBy": [
      {
        "field": "createDate",
        "order": "DESC"
      }
    ],
    "pageNo": 1,
    "pageSize": 5,
    "totalSize": 547
  }
}
```

## 示例 2

### 请求示例

```
POST
https://apigw-address/connect-service/v2.1/commands?action=search&deviceKey=zm_mqtt&productKey=bXuuAiku&orgId=yourOrgId
{
  "expression": "commandName.zh_CN like \"Int_value\" AND createTime >= \"2019-08-13 09:00:00\"",
  "pagination": {
    "pageNo": 1,
    "pageSize": 5
  }
}
```

### 返回示例

```json
{
  "code": 0,
  "msg": "OK",
  "requestId": "051ab2c9-5de4-4c05-9731-042475234267",
  "data": [
    {
      "commandId": "2322417698664521728",
      "orgId": "yourOrgId",
      "productKey": "yourProductKey",
      "deviceKey": "yourDeviceKey",
      "assetId": "sxH2DD6f",
      "createTime": 1565688738554,
      "createLocaltime": "2019-08-13 09:32:18",
      "commandType": 1,
      "commandName": {
        "defaultValue": "Int_value",
        "i18nValue": {
          "en_US": "Int_value"
        }
      },
      "timeout": 30,
      "pendingTtl": 0,
      "state": 6,
      "tslIdentifier": "Int_value",
      "inputData": 111,
      "outputData": null
    },
    {
      "commandId": "2322417676665921536",
      "orgId": "yourOrgId",
      "productKey": "yourProductKey",
      "deviceKey": "yourDeviceKey",
      "assetId": "sxH2DD6f",
      "createTime": 1565688735932,
      "createLocaltime": "2019-08-13 09:32:15",
      "commandType": 1,
      "commandName": {
        "defaultValue": "Int_value",
        "i18nValue": {
          "en_US": "Int_value"
        }
      },
      "timeout": 30,
      "pendingTtl": 0,
      "state": 6,
      "tslIdentifier": "Int_value",
      "inputData": 111,
      "outputData": null
    },
    {
      "commandId": "2322417636630765568",
      "orgId": "yourOrgId",
      "productKey": "yourProductKey",
      "deviceKey": "yourDeviceKey",
      "assetId": "sxH2DD6f",
      "createTime": 1565688731159,
      "createLocaltime": "2019-08-13 09:32:11",
      "commandType": 1,
      "commandName": {
        "defaultValue": "Int_value",
        "i18nValue": {
          "en_US": "Int_value"
        }
      },
      "timeout": 30,
      "pendingTtl": 100,
      "state": 2,
      "tslIdentifier": "Int_value",
      "inputData": 111,
      "outputData": null
    },
    {
      "commandId": "2322417537678745600",
      "orgId": "yourOrgId",
      "productKey": "yourProductKey",
      "deviceKey": "yourDeviceKey",
      "assetId": "sxH2DD6f",
      "createTime": 1565688719363,
      "createLocaltime": "2019-08-13 09:31:59",
      "commandType": 1,
      "commandName": {
        "defaultValue": "Int_value",
        "i18nValue": {
          "en_US": "Int_value"
        }
      },
      "timeout": 10,
      "pendingTtl": 600,
      "state": 2,
      "tslIdentifier": "Int_value",
      "inputData": 111,
      "outputData": null
    },
    {
      "commandId": "2322417518334615552",
      "orgId": "yourOrgId",
      "productKey": "yourProductKey",
      "deviceKey": "yourDeviceKey",
      "assetId": "sxH2DD6f",
      "createTime": 1565688717057,
      "createLocaltime": "2019-08-13 09:31:57",
      "commandType": 1,
      "commandName": {
        "defaultValue": "Int_value",
        "i18nValue": {
          "en_US": "Int_value"
        }
      },
      "timeout": 10,
      "pendingTtl": 600,
      "state": 2,
      "tslIdentifier": "Int_value",
      "inputData": 111,
      "outputData": null
    }
  ],
  "pagination": {
    "sortedBy": [
      {
        "field": "createDate",
        "order": "DESC"
      }
    ],
    "pageNo": 1,
    "pageSize": 5,
    "totalSize": 6
  }
}
```

## Java SDK调用示例

```java
package com.envisioniot.enos.api.sample.connect_service.command;
 
import com.envision.apim.poseidon.config.PConfig;
import com.envision.apim.poseidon.core.Poseidon;
import com.envisioniot.enos.api.common.constant.request.Pagination;
import com.envisioniot.enos.connect_service.v2_1.service.SearchCommandRequest;
import com.envisioniot.enos.connect_service.v2_1.service.SearchCommandResponse;
 
public class SearchCommand {
 
    public static void main(String[] args) {
        String accessKey = "...";
        String secretKey = "...";
        String serverUrl = "https://...";
 
        String orgId = "yourOrgId";
        String productKey = "yourProdctKey";
        String deviceKey = "yourDeviceKey";
 
        SearchCommandRequest request = new SearchCommandRequest();
        request.setOrgId(orgId);
        request.setProductKey(productKey);
        request.setDeviceKey(deviceKey);
        request.setExpression("commandName.zh_CN like \"Int_value\" AND createTime >= \"2019-08-13 09:00:00\"");
        request.setPagination(new Pagination(5, 1, null));
        SearchCommandResponse response = Poseidon.config(PConfig.init().appKey(accessKey).appSecret(secretKey).debug())
                .url(serverUrl)
                .getResponse(request, SearchCommandResponse.class);
    }
}
```