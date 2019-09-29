# Delete Asset Tree

删除一个资产树。

## 请求格式

```
https://{apigw-address}/asset-tree-service/v2.1/asset-trees?action=delete

```

## 请求参数（URI）

| 名称          | 位置（Path/Query） | 是否必须 | 数据类型 | 描述      |
|---------------|------------------|----------|-----------|--------------|
| orgId         | Query            | true     | String    | 资产所属的组织ID。[如何获取orgId信息>>](/docs/api/zh_CN/2.0.9/api_faqs#id-orgid-orgid)                |
| treeId        | Query            | true    | String    | 需要删除的资产树ID。[如何获取资产树信息ID>>](/docs/api/zh_CN/2.0.9/api_faqs#id)        |



##错误码

| 代码 | 描述    |
|-----------|-----------------------------|
| 99800| 资产树根节点下存在子节点，不能被删除。 |




## 示例 1

### 请求示例

```
POST https://apigw-address/asset-tree-service/v2.1 
/asset-trees?action=delete&orgId=yourOrgId&treeId=H4yVDl2U
```

### 返回示例

```json
{
  "code": 0,
  "msg": "OK",
  "requestId": "01b5477a-374e-49a0-8b68-7dbfe8f0b74f",
  "data": null
}
```

