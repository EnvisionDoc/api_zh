# Close Active Alert

关闭当前告警。关闭后的告警信息将被归为历史告警数据。

## 请求格式

```
POST https://{apigw-address}/event-service/v2.1/active-alerts?action=close
```

## 请求参数（URI）

| 名称          | 位置（Path/Query） | 是否必须 | 数据类型 | 描述      |
|---------------|------------------|----------|-----------|--------------|
| orgId         | Query            | true     | String    | 资产所属的组织ID。[如何获取orgId信息>>](/docs/api/zh_CN/2.0.9/api_faqs#id-orgid-orgid)                |


## 请求参数（Body）

| 名称 | 是否必须 | 数据类型 | 描述 |
|------|-----------------|-----------|-------------|
| eventId        | true     | String    | 当前告警ID    |
| recoverTime          | true    | Long    | 触发告警的异常状况恢复正常的时间，以UTC时间表示，格式见[UTC采用的ISO8601标准时间格式>>](/docs/api/zh_CN/2.0.9/api_faqs.html#utciso8601)  |
| localRecoverTime    | false        | String       | 触发告警的异常状况恢复正常的时间，以本地时间表示，格式见[localtime采用的日期时间格式>>](/docs/api/zh_CN/2.0.9/api_faqs.html#localtime)|
| recoverReason | false         | String       | 异常状况恢复的原因|





## 响应参数

| 名称  | 数据类型      | 描述               |
|-------|----------------|---------------------------|
| data | null | 无 |



## 示例

### 请求示例

```json
POST https://{apigw-address}/event-service/v2.1/active-alerts?action=close&orgId=yourOrgId&eventId=2019060135b6df70b2de6aa2f2eb1d09e9aa1ae7&recoverTime=1559304900404

```

### 返回示例

```json
{
	"code": 0,
	"msg": "OK",
	"requestId": "4873095e-621d-4cfd-bc2c-edb520f574ea"
}
```
