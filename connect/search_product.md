# Search Product

搜索满足条件的产品。

## 请求格式

```
https://{apigw-address}/connect-service/v2.1/products?action=search
```

## 请求参数（URI）

| 名称          | 位置（Path/Query） | 是否必须 | 数据类型 | 描述      |
|---------------|------------------|----------|-----------|--------------|
| orgId         | Query            | true     | String    | 资产所属的组织ID。[如何获取orgId信息>>](/docs/api/zh_CN/latest/api_faqs#id-orgid-orgid)                |


## 请求参数（Body）

| 名称         | 是否必须 | 数据类型 | 描述      |
|-------------------|----------|-----------|--------------|
| expression         | false    | String   | 查询表达式，支持类sql的查询。目前支持查询的字段是`productKey`、`modelId`。支持的算术运算符是=、in，逻辑运算符是and和or。[如何使用查询表达式>>](/docs/api/zh_CN/latest/api_faqs.html#id1)|
| pagination     | false     | String   | 分页参数。如未指定，默认每页10条。见[Pagination请求结构体>>](/docs/api/zh_CN/latest/overview.html?highlight=pagination#pagination) |


## 响应参数

| 名称| 数据类型 | 描述         |
|-------------|-----------------------------------|-----------------------------|
| data| Product结构体                           | 查询得到的产品列表，见[Product结构体>>](/docs/api/zh_CN/latest/connect/get_product.html#product-productstruc)                |




## 示例 1

### 请求示例

```
POST: /connect-service/v2.1/products?action=search&orgId=abc 
{
	"expression":"modelId=\"AlterTest0615\"",
	"pagination":{
		"pageNo":1,
		"pageSize":5
	}
}
```

### 返回示例

```json
{
	"code":0,
	"msg":"OK",
	"requestId":"a82752bb-9eb0-4cd5-b0c6-0c1aeb35f6d2",
	"data":[
		{
			"orgId":"yourOrgId",
			"productKey":"yourProductKey",
			"productName":{
				"defaultValue":"openapi_sdk_8",
				"i18nValue":{}
			},
			"productSecret":"yourProductSecret",
			"productDesc":"test_sdk_update",
			"productType":"Device",
			"dataFormat":"Custom",
			"productTags":{},
			"modelId":"AlterTest0615",
			"dynamicActiveEnabled":false,
			"biDirectionalAuth":true
		},
		{
			"orgId":"yourOrgId",
			"productKey":"yourProductKey",
			"productName":{
				"defaultValue":"AlterTest0615_Product",
				"i18nValue":{}
			},
			"productSecret":"yourProductSecret",
			"productDesc":"",
			"productType":"Device",
			"dataFormat":"Json",
			"productTags":{},
			"modelId":"AlterTest0615",
			"dynamicActiveEnabled":false,
			"biDirectionalAuth":false
		}
	],
	"pagination":{
		"sortedBy":null,
		"pageNo":1,
		"pageSize":5,
		"totalSize":2
	}
}
```

