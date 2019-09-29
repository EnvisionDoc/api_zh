# Search Alert Rule

查询告警规则。

## 请求格式

```
POST https://{apigw-address}/event-service/v2.1/alert-rules?action=search
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
   * - modelId
     - false
     - String
     - 告警规则适用的模型
   * - measurepointId
     - false
     - String
     - 资产测点。`如何获取测点（pointId）信息>> </docs/api/zh_CN/2.0.9/api_faqs#pointid-pointid>`__
   * - expression
     - false
     - String
     - 查询表达式，支持类sql的查询。目前支持查询的字段是 ``ruleId``、``modelId``、``measurepointId``。支持的算术运算符是=和in，逻辑运算符是and和or。`如何使用查询表达式>> </docs/api/zh_CN/2.0.9/api_faqs.html#id1>`__
   * - pagination
     - false
     - Pagination请求结构体
     - 分页的参数。如未指定，默认每页10条。按照 ``updateTime`` 降序排序。见 `Pagination请求结构体>> </docs/api/zh_CN/2.0.9/overview.html?highlight=pagination#pagination>`__。



## 响应参数

.. list-table::
   :widths: auto
   :header-rows: 1

   * - 名称
     - 是否必须
     - 数据类型
     - 描述
   * - data
     - AlertRule 结构体
     - 告警规则，见 `AlertRule结构体 <search_alert_rule#alertrule-alertrule>`__。


### AlertRule结构体 <alertrule>

.. list-table::
   :widths: auto
   :header-rows: 1

   * - 名称
     - 数据类型
     - 描述
   * - orgId
     - String
     - 规则所属的组织ID
   * - ruleId
     - String
     - 告警规则编号
   * - ruleDesc
     - StringI18n
     - 国际化告警描述
   * - modelId
     - String
     - 规则适用的模型
   * - measurepointId
     - String
     - 资产测点。
   * - condition
     - String
     - 类查询表达式。如“${temperature} = 19”表示“测点temperature的值等于19”。使用“/”表达层级关系，如“${pointA/att1} = 18”表示“测点A的att1属性值为18”。目前只支持最多向下一层。
   * - isEnabled
     - Boolean
     - 是否启用
   * - severityId
     - String
     - 告警级别编号
   * - severityDesc
     - StringI18n
     - 国际化告警级别描述
   * - contentId
     - String
     - 告警内容编号
   * - contentDesc
     - StringI18n
     - 国际化告警级别描述
   * - typeId
     - String
     - 告警类型
   * - typeDesc
     - StringI18n
     - 告警类型描述
   * - tags
     - tags结构体
     - 规则标签
   * - isRoot
     - Boolean
     - 是否是根源告警
   * - scope
     - AssetNode结构体
     - 告警规则的作用域。以资产树上的节点来表示。见 `AssetNode结构体 <search_alert_rule#assetnode-assetnode>`__。
   * - source
     - String 
     - 自定义数据来源，用以表明告警规则适用的数据源。若适用于EnOS Cloud，则为空；若适用于EnOS Edge，则为edge。
   * - triggeringDelayTimer
     - Integer
     - 延后告警触发时间。单位为秒，范围[60 - 10800]。当发生匹配告警规则的异常状况，且该状况在所设定的时间内仍未恢复正常时，系统才会产生告警。当为0时表示立即触发告警。



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
     - 资产树ID。若为“all”，则这是一个特殊节点，代表组织下的全局
   * - assetId
     - true
     - String
     - 资产ID


## 示例

### 请求示例

```json
POST https://{apigw-address}/event-service/v2.1/alert-rules?action=search&orgId=yourOrgId
{
    "modelId": "EnOS_Solar_CombinerBox",
    "measurepointId": "CBX.BranchStateAttr"
}
```

### 返回示例

```json
{
    "pagination": {
        "pageNo": 1,
        "pageSize": 10,
        "totalSize": 1,
        "sortedBy": [{
            "field": "updateTime",
            "order": "DESC"
        }]
    },
    "code": 0,
    "msg": "OK",
    "requestId": "a9689b9f-0cb6-4e47-a41c-bd459b687309",
    "data": [{
        "orgId": "yourOrgId",
        "ruleId": "zh_model_struct",
        "ruleDesc": {
            "defaultValue": "Grid is connected from converter",
            "i18nValue": {
                "en_US": "Grid is connected from converter",
                "zh_CN": "电网由变频器连接"
            }
        },
        "modelId": "zh_model",
        "measurepointId": "aa",
        "condition": "${aa} = 18",
        "isEnabled": true,
        "severityId": "WARN",
        "severityDesc": {
            "defaultValue": "WARN"
        },
        "contentId": "planetTemperature",
        "contentDesc": {
            "defaultValue": "连接"
        },
        "typeId": "warning_Type",
        "typeDesc": {
            "defaultValue": "connected"
        },
        "tags": {
            "key1": "v1"
        },
        "isRoot": false,
        "scope": [{
            "treeId": "ptde66nd",
            "assetId": "FbFy8qyz"
        }]
    },{
        "orgId": "yourOrgId",
        "ruleId": "zh_model_struct2",
        "ruleDesc": {
            "defaultValue": "Grid is connected from converter",
            "i18nValue": {
                "en_US": "Grid is connected from converter",
                "zh_CN": "电网由变频器连接"
            }
        },
        "modelId": "zh_model",
        "measurepointId": "aa",
        "condition": "${aa} = 18",
        "isEnabled": true,
        "severityId": "WARN",
        "severityDesc": {
            "defaultValue": "WARN"
        },
        "contentId": "planetTemperature",
        "contentDesc": {
            "defaultValue": "连接"
        },
        "typeId": "warning_Type",
        "typeDesc": {
            "defaultValue": "connected"
        },
        "tags": {
            "key1": "v1"
        },
        "isRoot": false,
        "scope": [{
            "treeId": "ptde66nd",
            "assetId": "FbFy8qyz"
        }]
    }]
}
```
