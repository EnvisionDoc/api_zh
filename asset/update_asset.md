# Update Asset

全量或部分更新资产信息。

## 请求格式

```
https://{apigw-address}/asset-service/v2.1/assets?action=update
```

## 请求参数（URI）

.. list-table::
   :widths: auto
   :header-rows: 1

   * - 名称
     - 位置（Path/Query）
     - 是否必须
     - 数据类型
     - 描述
   * - orgId
     - Query
     - true
     - String
     - 资产所属的组织ID。`如何获取orgId信息>> </docs/api/zh_CN/2.0.9/api_faqs#id-orgid-orgid>`__
   * - isPatchUpdate
     - Query
     - false
     - Boolean
     - 是否是局部更新，默认为true。
     
       + 当其值为true时，只更新参数中指定字段的值；
       + 当其值为false时，更新所有字段的值，即未指定值的字段将被置空。


## 请求参数（Body）

.. list-table::
   :widths: auto
   :header-rows: 1

   * - 名称
     - 是否必须
     - 数据类型
     - 描述
   * - asset
     - true
     - ``AssetUpdate`` 结构体
     - 用于资产更新。
       当 ``isPatchUpdate`` 为true时，只更新 ``asset`` 参数中指定的字段；当 ``isPatchUpdate`` 为false时，更新 ``asset`` 所有字段值，即未指定值的字段将被置空。结构见 `AssetUpdate结构体>> </docs/api/zh_CN/2.0.9/asset/update_asset.html#id2>`__


### AssetUpdate结构体


.. list-table::
   :widths: auto
   :header-rows: 1

   * - 名称
     - 是否必须
     - 数据类型
     - 描述
   * - assetId
     - true
     - String
     - 资产ID。`如何获取Asset ID信息>> </docs/api/zh_CN/2.0.9/api_faqs.html#asset-id-assetid-assetid>`__
   * - name
     - false
     - StringI18n
     - 该资产的各语言名称。结构请见 `国际化名称结构体>> </docs/api/zh_CN/2.0.9/api_faqs.html#id3>`__
   * - description
     - false
     - String
     - 资产描述
   * - attributes
     - false
        (如果 ``isPatchUpdate`` 为false，``attributes`` 必填)
     - Map
     - 资产所属的模型属性。
        ``Key`` 为属性ID，String类型。Value的类型取决于模型中这个属性的定义。详情请见 `attributes的表示方法>> </docs/api/zh_CN/2.0.9/api_faqs.html#attributes>`__
   * - timezone
     - false
     - String
     - 时区。详情请见 `时区表示方法>> </docs/api/zh_CN/2.0.9/api_faqs.html#id4>`__
   * - modelId
     - false（如果 ``isPatchUpdate`` 为false，``modelId`` 必填）
     - String
     - 模型ID
   * - tags
     - false
     - Map
        （Key为String, Value为String）
     - 用户自定义标签，详情请见 `标签的作用与表示方法>> </docs/api/zh_CN/2.0.9/api_faqs.html#id6>`__


## 错误码

.. list-table::
   :widths: auto
   :header-rows: 1

   * - 代码
     - 描述
   * - 11958
     - 由于资产属性校验失败导致更新失败


## 示例 1

### 请求示例

```json
POST https://{apigw-address}/asset-service/v2.1/assets?action=update&orgId=o15475450989191
{
  "asset": {
       "assetId": "Instance_cshan_001",
       "name": {
           "defaultValue": "daniu",
           "i18nValue": {
                    "en_US": "English name ",
                    "zh_CN": "Chinese name"
                        }
               },
       "description": "hahdesc",
       "attributes": {},
       "modelId": "cshan111602",
       "timezone": "+08:00",
       "tags": {
           "year": "2000",
           "author": "cshan"
               }
           }
}
```

### 返回示例

```json
{
  "code": 0,
  "msg": "OK"，
  "requestId": "fa11232e-7e45-4176-a382-963c1240a27f"
}

```


## Java SDK调用示例

```java
public class UpdateAsset {
    private static String accessKey = "4ced4f38-1ced-476e0a446215-a602-4307";
    private static String secretKey = "0a446215-a602-4307-9ff2-3feed3e983ce";
    private static String orgId = "1c499110e8800000";
    private static String url = "https://{apigw-address}";

    public static void main(String[] args) {
        UpdateAssetRequest request = new UpdateAssetRequest();
        request.setOrgId(orgId);

        AssetUpdateVo asset = new AssetUpdateVo();
        asset.setAssetId("XBOBqC1O");
        Map<String, Object> newAttrs = new HashMap<>();
        newAttrs.put("doubleTest",123.45);
        asset.setAttributes(newAttrs);

        request.setAsset(asset);
        request.setIsPatchUpdate(true);

        UpdateAssetResponse response = Poseidon.config(PConfig.init().appKey(accessKey).appSecret(secretKey).debug())
                .url(url)
                .getResponse(request, request.getResponseClass());
        System.out.println(response);
    }
}
```
