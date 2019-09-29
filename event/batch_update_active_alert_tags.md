# Batch Update Active Alert Tags

<!--测试了一下，99500-->

批量更新当前告警库中指定告警的标签数据。返回的结构一次说明每一条告警的更新结果。如果某一条发生了错误信息，会记录下错误信息并且继续执行余下的更新。

## 请求格式

```
POST https://{apigw-address}/event-service/v2.1/active-alerts?action=batchUpdateTags
```

## 请求参数（URI）

| 名称          | 位置（Path/Query） | 是否必须 | 数据类型 | 描述      |
|---------------|------------------|----------|-----------|--------------|
| orgId         | Query            | true     | String    | 资产所属的组织ID。[如何获取orgId信息>>](/docs/api/zh_CN/2.0.9/api_faqs#id-orgid-orgid)                |
|isPatchUpdate|Query|true|Boolean|是否全量更新。<br>当其值为true时，只更新参数中指定字段的值；<br>当其值为false时，更新所有字段的值，即未指定值的字段将被置空。|


## 请求参数（Body）
| 名称 | 是否必须 | 数据类型 | 描述 |
|------|-----------------|-----------|-------------|
| eventIds          | true    | String类型List    | 告警ID列表 |
| tags        | true     | Tags结构体    | 需要修改的标签 |


## 响应参数

| 名称  | 数据类型      | 描述               |
|-------|----------------|---------------------------|
|data|null|无|





## 示例

### 请求示例

```json
POST https://{apigw-address}/event-service/v2.1/active-alerts?action=batchUpdateTags&orgId=1c499110e8800000
{
	"eventIds": ["20190531b83331a8549e1e956f2413552eda1ec9",
	"20190615f7b3864b98d80b25e8e9a0affd6ce064"],
	"isPatchUpdate": false,
	"tags": {
		"Tag999": "999"
	}
}
```

### 返回示例

```json
{
        "code": 0,
        "msg": "OK",
        "requestId": "4873095e-621d-4cfd-bc2c-edb520f574ea",
        "data": ""
}
```
