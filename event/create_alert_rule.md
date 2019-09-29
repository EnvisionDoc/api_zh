# Create Alert Rule

创建一条告警规则。系统会检验以下输入参数的有效性：

- 模型ID（`modelId`）在组织下是否可用
- 测点（`measurepointId`）是否有效
- 告警级别（`severityId`）是否合法
- 告警内容（`contentId`）是否合法
- 查询范围（`scope`）中的作用域的节点是否合法

## 请求格式

```
POST https://{apigw-address}/event-service/v2.1/alert-rules?action=create
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




## 请求参数（Body）

.. list-table::
   :widths: auto
   :header-rows: 1

   * - 名称
     - 是否必须
     - 数据类型
     - 描述
   * - ruleId
     - true
     - String
     - 告警规则编号，由用户指定
   * - ruleDesc
     - true
     - StringI18n 
     - 告警描述
   * - modelId
     - true
     - String
     - 告警规则适用的模型
   * - measurepointId
     - true
     - String
     - 资产测点。[如何获取测点（pointId）信息>>](/docs/api/zh_CN/2.0.9/api_faqs#pointid-pointid)
   * - condition
     - true 
     - String
     - 类查询表达式。如“${temperature} = 19”表示“测点temperature的值等于19”。使用“/”表达层级关系，如“${pointA/att1} = 18”表示“测点A的att1属性值为18”。目前只支持最多向下一层。`如何使用查询表达式>> </docs/api/zh_CN/2.0.9/api_faqs.html#id1>`__
   * - severityId
     - true
     - String
     - 告警级别编号
   * - contentId
     - true
     - String
     - 告警内容编号
   * - tags
     - false
     - tags结构体 
     - 告警规则标签
   * - isEnabled
     - false
     - Boolean 
     - 是否启用，默认启用（true）
   * - isRoot
     - false
     - Boolean
     - 是否是根源告警，默认为false
   * - scope
     - true 
     - AssetNode结构体
     - 指定资产树上的节点来表明告警规则的作用域。见 `AssetNode结构体 <create_alert_rule#assetnode-assetnode>`__。
   * - source
     - false
     - String
     - 自定义数据来源，用以表明告警规则适用的数据源。若适用于EnOS Cloud，则为空；若适用于EnOS Edge，则为edge。
   * - triggeringDelayTimer
     - false
     - Integer
     - 延后告警触发时间。单位为秒，范围[60 - 10800]。当发生匹配告警规则的异常状况，且该状况在所设定的时间内仍未恢复正常时，系统才会产生告警。若设为0则表示立即触发告警。详见 `教程：设置异常持续一段时间后触发的告警 <docs.eniot.io/docs/device-connection/zh_CN/2.0.9/howto/alert/setting_alert_triggering_delay_timer.html>`__。


### AssetNode结构体 <assetnode>

.. list-table::
   :widths: auto
   :header-rows: 1

   * - 名称
     - 是否必须
     - 数据类型
     - 描述
   * - treeId
     - true
     - String
     - 资产树ID。若为“all”，则这是一个特殊的节点，代表组织下的全局
   * - assetId
     - true
     - String 
     - 资产ID。`如何获取Asset ID信息>>` </docs/api/zh_CN/2.0.9/api_faqs#asset-id-assetid-assetid>`__



## 响应参数

.. list-table::
   :widths: auto
   :header-rows: 1

   * - 名称
     - 是否必须
     - 数据类型
     - 描述
   * - data
     - String
     - ruleId




## 示例

### 请求示例

```json
POST https://{apigw-address}/event-service/v2.1/alert-rules?action=create&orgId=yourOrgId
{
    "ruleId": "user BID",
    "ruleDesc": {
        "defaultValue": "Grid is connected from converter",
        "i18nValue": {
            "en_US": "Grid is connected from converter",
            "zh_CN": "电网由变频器连接"
        }
    },
    "modelId": "EnOS_Solar_CombinerBox",
    "measurepointId": "CBX.BranchStateAttr",
    "condition": "${CBX.BranchStateAttr} = 18",
    "severityId": "WARN",
    "contentId": "planetTemperature",
    "tags": {
        "key1": "v1"
    },
    "orgId": "yourOrgId",
    "scope": [{
        "treeId": "ptde66nd",
        "assetId": "FbFy8qyz"
    }],
    "isEnabled": true,
    "isRoot": true
}

```

### 返回示例

```json
{
	"code": 0,
	"msg": "OK",
	"requestId": "4873095e-621d-4cfd-bc2c-edb520f574ea"
}
```
