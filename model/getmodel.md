# Get Thing Model

根据模型标识符（`modelId`）获取模型。

## 请求格式

```
https://{apigw-address}/model-service/v2.1/thing-models?action=get
```

## 请求参数（URI）

| 名称          | 位置（Path/Query） | 是否必须 | 数据类型 | 描述      |
|-------|-------------|-----|------|----------|
| orgId   | Query            | True     | String    | 资产所属的组织ID。[如何获取orgId信息>>](/docs/api/zh_CN/latest/api_faqs#id-orgid-orgid) |
| scope   | Query            | False    | Integer   | 查询范围。 0：只从`orgId`指定的组织搜索； 1：从`orgId`指定的组织和公有模型所在的组织搜索。默认为1。 |
| modelId | Query            | True     | String    | 资产所属模型ID。[如何获取modelId信息>>](/docs/api/zh_CN/latest/api_faqs.html#modelid-modelid)|



## 响应参数

|名称|数据类型|描述|
|-----------|-----------|----------|
|data|Object|物模型，见[ThingModel结构体>>](/docs/api/zh_CN/latest/model/searchmodel.html#thingmodel-thingmodel)|



## 错误码

见[公共返回码（接入服务）](/docs/api/zh_CN/latest/overview.html#id8)。



## 示例

### 请求示例

```
GET https://{apigw-address}/model-service/v2.1/thing-models?action=get&orgId=1c499110e8800000&modelId=planet
```

### 返回示例

```json
{
    "code": 0,
    "msg": "OK",
    "requestId": "fa11232e-7e45-4176-a382-963c1240a27f",
    "data": {
                "modelId": "planet",
                "modelIdPath": "/planet",
                "orgId": "yourOrgId",
                "name": {
                    "defaultValue": "行星",
                    "i18nValue": {
                        "en_US": "planet"
                    }
                },
                "desc": "test",
                "tags": {},
                "attributes": {
                    "starsystem": {
                        "identifier": "starsystem",
                        "name": {
                            "defaultValue": "星系",
                            "i18nValue": {
                                "en_US": "star system"
                            }
                        },
                        "desc": "",
                        "tags": {},
                        "dataType": "STRING",
                        "unit": null,
                        "isRequired": false
                    }
                },
                "measurepoints": {
                    "temperature": {
                        "identifier": "temperature",
                        "name": {
                            "defaultValue": "temperature",
                            "i18nValue": {
                                "en_US": "temperature"
                            }
                        },
                        "desc": "temperature",
                        "tags": {},
                        "dataType": "FLOAT",
                        "hasQuality": false,
                        "signalType": "Generic",
                        "unit": {
                            "unitId": "°C",
                            "multiplier": "ONE"
                        }
                    }
                },
                "services": {
                    "speedup": {
                        "identifier": "speedup",
                        "name": {
                            "defaultValue": "speedup",
                            "i18nValue": {
                                "en_US": "speedup"
                            }
                        },
                        "desc": "t",
                        "tags": {},
                        "outputData": [
                            {
                                "identifier": "delta",
                                "name": {
                                    "defaultValue": "delta",
                                    "i18nValue": {
                                        "en_US": "delta"
                                    }
                                },
                                "desc": "",
                                "tags": {},
                                "dataType": "INT",
                                "unit": null
                            }
                        ],
                        "inputData": [
                            {
                                "identifier": "delta",
                                "name": {
                                    "defaultValue": "delta",
                                    "i18nValue": {
                                        "en_US": "delta"
                                    }
                                },
                                "desc": "",
                                "tags": {},
                                "dataType": "INT",
                                "unit": {
                                    "unitId": "rpm",
                                    "multiplier": "ONE"
                                }
                            }
                        ],
                        "callType": "ASYNC"
                    }
                },
                "events": {
                    "alert": {
                        "identifier": "alert",
                        "name": {
                            "defaultValue": "alert",
                            "i18nValue": {
                                "en_US": "alert"
                            }
                        },
                        "desc": "e",
                        "tags": {},
                        "outputData": [
                            {
                                "identifier": "event1",
                                "name": {
                                    "defaultValue": "event1",
                                    "i18nValue": {
                                        "en_US": "event1"
                                    }
                                },
                                "desc": "",
                                "tags": {},
                                "dataType": "INT",
                                "unit": null
                            }
                        ],
                        "eventType": "ERROR"
                    }
                }
            }
}
```


## Java SDK调用示例

```java
public class GetThingModel {
    private static String accessKey = "4ced4f38-1ced-476e0a446215-a602-4307";
    private static String secretKey = "0a446215-a602-4307-9ff2-3feed3e983ce";
    private static String orgId = "1c499110e8800000";
    private static String url = "https://{apigw-address}";
    public static void main(String[] args) {
        GetThingModelRequest request = new GetThingModelRequest();
        request.setOrgId(orgId);
        request.setModelId("planet");
        request.setScope(1);
        GetThingModelResponse response = Poseidon.config(PConfig.init().appKey(accessKey).appSecret(secretKey).debug())
                .url(url)
                .getResponse(request, request.getResponseClass());
        System.out.println(response.getData());
    }
}
```