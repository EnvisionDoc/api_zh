# Update Asset Tree

更新资产树的信息。

## 请求格式

```
https://{apigw-address}/asset-tree-service/v2.1/asset-trees?action=update
```

## 请求参数（URI）

| 名称          | 位置（Path/Query） | 是否必须 | 数据类型 | 描述      |
|---------------|------------------|----------|-----------|--------------|
| orgId         | Query            | true     | String    | 资产所属的组织ID。[如何获取orgId信息>>](/docs/api/zh_CN/latest/api_faqs#id-orgid-orgid)                |

## 请求参数（body）

| 名称          | 是否必须 | 数据类型 | 描述      |
|-----------------|---------------|-------------------|-----|
| treeUpdateInfo   | true     |   TreeUpdateVo结构体         |  更新资产树时需要提供的更新详情，见[TreeUpdateVo结构体](update_asset_tree#treeupdatevo-treeupdatevostruc)。 |


### TreeUpdateVo结构体 <treeupdatevostruc>

| 名称   | 是否必须     | 数据类型 | 描述      |
|-----------|-----------------|-------------------|-----------------------|
| treeId   | true         | String       | 资产树ID。|
| name     | true         | StringI18n   | 支持国际化的资产名称。结构请见[国际化名称结构体>>](/docs/api/zh_CN/latest/api_faqs.html#id3) |
| tags     | false        | Tag结构体    | 用户自定义标签，详情请见[标签的作用与表示方法>>](/docs/api/zh_CN/latest/api_faqs.html#id6) |



## 示例 1

### 请求示例

```
https://apigw-address/asset-tree-service/v2.1 
/asset-trees?action=update&orgId=yourOrgId
{
"treeUpdateInfo":{
    "treeId": "H4yVDl2U",
    "name": {
        "defaultValue": "aaaa"
    },
    "tags":{
        "ss":"f"
    }
}
}
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

