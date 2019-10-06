# Update Alert Rule

更新告警规则。所有请求参数（Body）中包含的参数，只要不是null，都可以被更新。需要进行校验的字段有：模型ID（`modelId`）、测点（`measurepointId`）、告警级别（`severityId`）、告警内容（`contentId`）、查询范围（`scope`）。

## 请求格式

```
POST https://{apigw-address}/event-service/v2.1/alert-rules?action=update
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
     - 资产所属的组织ID。`如何获取orgId信息>> </docs/api/zh_CN/latest/api_faqs#id-orgid-orgid>`__
   * - isPatchUpdate
     - Query
	   - true
	   - Boolean
	   - 是否全量更新。
	     当其值为true时，只更新参数中指定字段的值；
		   当其值为false时，更新所有字段的值，即未指定值的字段将被置空。


## 请求参数（Body）

.. list-table::
   :widths: auto
   :header-rows: 1

   * - 名称
     - 是否必须
     - 数据类型
     - 描述
   * - alertRule
     - true
	   - alertRule结构体
	   - 告警规则，见 `alertRule结构体 <update_alert_rule#alertrule-alertrule>`__。


### alertRule结构体 <alertrule>

.. list-table::
   :widths: auto
   :header-rows: 1

   * - 名称
     - 是否必选（特指在isPatchUpdate=false的情况下）
     - 数据类型
     - 描述
   * - ruleId
     - true
	   - String
	   - 告警规则编号，由用户指定，是用于定位需要更新的告警规则的唯一标识。
   * - ruleDesc
     - true
	   - StringI18n
	   - 国际化告警描述，只支持全量更新。结构请见 `国际化名称结构体>> </docs/api/zh_CN/latest/api_faqs.html#id3>`__
   * - modelId
     - true
	   - String
	   - 规则适用的模型。`如何获取modelId信息>> </docs/api/zh_CN/latest/api_faqs#modelid-modelid>`__
   * - measurepointId
     - true
	   - String
	   - 资产测点。`如何获取测点（pointId）信息>> </docs/api/zh_CN/latest/api_faqs#pointid-pointid>`__
   * - condition
     - true
	   - String
	   - 类查询表达式。如“${temperature} = 19”表示“测点temperature的值等于19”。使用“/”表达层级关系，如“${pointA/att1} = 18”表示“测点A的att1属性值为18”。目前只支持最多向下一层。`如何使用查询表达式>> </docs/api/zh_CN/latest/api_faqs.html#id1>`__ 
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
	   - 规则标签，只支持全量更新
   * - scope
     - true
	   - AssetNode结构体
	   - 指定资产树上的节点来表明告警规则的作用域。见 `AssetNode结构体>> <update_alert_rule#assetnode-assetnode>`__
   * - isEnabled
     - false
	   - Boolean
	   - 是否启用，默认启用（true）
   * - source
     - false
	   - String
	   - 自定义数据来源，用以表明告警规则适用的数据源。若适用于EnOS Cloud，则为空；若适用于EnOS Edge，则为edge。
   * - triggeringDelayTimer
     - false
	   - Integer
	   - 延后告警触发时间。单位为秒，范围[60 - 10800]。当发生匹配告警规则的异常状况，且该状况在所设定的时间内仍未恢复正常时，系统才会产生告警。若设为0则表示立即触发告警。详见 `教程：设置异常持续一段时间后触发的告警 <docs.eniot.io/docs/device-connection/zh_CN/latest/howto/alert/setting_alert_triggering_delay_timer.html>`__。

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
	   - 资产树ID。若为“all”，则这是一个特殊的节点，代表组织下的全局。
   * - assetId
     - true
	   - String
	   - 资产ID。`如何获取Asset ID信息>> </docs/api/zh_CN/latest/api_faqs#asset-id-assetid-assetid>`__


## 响应参数

.. list-table::
   :widths: auto
   :header-rows: 1

   * - 名称
     - 是否必须
     - 数据类型
     - 描述
   * - data
     - null
	   - 无



## 示例

### 请求示例

```json
POST https://{apigw-address}/event-service/v2.1/alert-rules?action=update&orgId=1c499110e8800000&isPatchUpdate=false
{
	"alertRule": {
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
		"orgId": "1c499110e8800000",
		"scope": [{
			"treeId": "ptde66nd",
			"assetId": "FbFy8qyz"
		}],
		"isEenabled": true
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
