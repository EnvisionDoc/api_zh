# 2019/08


## 接入服务

### 新增API

| API名称                          | 描述     |
|:---------------------------------|:---------|
| [Replace Device](../connect/replace_device.html) | 在资产ID（`assetId`）不改变的情况下更换一个设备的Device Key。 |

### 更新API


<table>
            <tr align="left">
                <th>API名称</th>
				<th>更新内容</th>
            </tr>
            <tr>
                <td><a href="../connect/create_product.html">Create Product</a></td>
				<td>请求参数（Body）中新增支持<code>dynamicActivateEnabled</code>、<code>productTags</code>两个可选参数。
				<ul>
				<li><code>dynamicActivateEnabled</code>：用于表示创建的产品是否允许动态激活</li>
            	<li><code>productTags</code>：用于表示产品标签</li>
				</ul>
            </td>
            </tr>
            <tr>
                <td><a href="../connect/update_product.html">Update Product</a></td>
				<td>请求参数（Body）中新增支持可选参数<code>productTags</code>，用于表示产品标签</td>
            </tr>
            
</table>



### 问题修复


| API名称                        | 修复的问题               |
|:-------------------------------|:-------------------------|
| [Create Device](../connect/create_device.html) | 传入的`deviceTags`未生效 |


## 告警服务

### 新增API

| API名称     | 描述                |
|:--------------|:---------------------|
|[Batch Update Active Alert Tags](../event/batch_update_active_alert_tags.html)| 批量更新指定告警的标签|
|[Create Alert Rule](../event/create_alert_rule.html)   |  创建一条告警规则             |
|[Update Alert Rule](../event/update_alert_rule.html)        |   更新告警规则            |
|[Delete Alert Rule](../event/delete_alert_rule.html)    |  删除组织下指定告警规则             |
|   [Create Alert Content](../event/create_alert_content.html)     |   创建告警内容            |
|  [Update Alert Content](../event/update_alert_content.html)      |    更新告警内容           |
|     [Delete Alert Content](../event/delete_alert_content.html)   |    删除告警内容           |
|    [Create Alert Severity](../event/create_alert_severity.html)    | 创建一条告警级别              |
|  [Update Alert Severity](../event/update_alert_severity.html)      |  更新告警级别             |
|     [Delete Alert Severity](../event/delete_alert_severity.html)   |   删除告警级别            |
|  [Create Alert Type](create_alert_type.html)      | 创建一条告警类型              |
|  [Update Alert Type](../event/update_alert_type.html)      |   更新告警类型            |
|  [Delete Alert Type](../event/delete_alert_type.html)      |  删除告警类型             |
|  [Create Active Alert](../event/create_active_alert.html)      | 创建当前告警              |
|   [Delete Active Alert](../event/delete_active_alert.html)     |删除指定告警               |
|   [Create History Alert](../event/create_history_alert.html) |创建历史告警|


### 更新API


<table>
            <tr align="left">
                <th>API名称</th>
				<th>更新内容</th>
            </tr>
            <tr>
                <td><a href="../event/search_active_alerts.html">Search Active Alerts</a></td>
				<td>请求参数（Body）中新增支持<code>scope</code>、<code>rootAlert</code>两个可选参数。
				<ul>
				<li><code>scope</code>：用于查询指定资产树或资产树上某资产节点下的告警，并指定是否返回被屏蔽的衍生告警。该参数不可与<code>rootAlert</code>参数同时使用。数据类型为Scope结构体。</li>
            	<li><code>rootAlert</code>：用于查询被指定根源告警屏蔽的衍生告警。该参数不可与<code>scope</code>参数同时使用。数据类型为RootAlert结构体。</li>
				</ul>
            </td>
            </tr>
            <tr>
                <td><a href="../event/search_history_alerts.html">Search History Alerts</a></td>
				<td>请求参数（Body）中新增支持<code>scope</code>、<code>rootAlert</code>两个可选参数。
				<ul>
				<li><code>scope</code>：用于查询指定资产树或资产树上某资产节点下的告警，并指定是否返回被屏蔽的衍生告警。该参数不可与<code>rootAlert</code>参数同时使用。数据类型为Scope结构体。</li>
            	<li><code>rootAlert</code>：用于查询被指定根源告警屏蔽的衍生告警。该参数不可与<code>scope</code>参数同时使用。数据类型为RootAlert结构体。</li>
				</ul>
            </td>
            </tr>
            
</table>