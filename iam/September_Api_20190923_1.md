# Get User List

获取当前账号权限下的所有用户列表。

## 请求格式

```
POST http://{apigw-address}/app-portal-service/v2.0/organization/user/list
```

## 请求参数（Header）

.. list-table::
   :widths: auto
   :header-rows: 1

   * - 名称
     - 是否必须
     - 数据类型
     - 描述
   * - Authorization
     - true
     - String
     - Access token，以Bearer Token表示。


## 请求参数（Body）

.. list-table::
   :widths: auto
   :header-rows: 1

   * - 名称
     - 是否必须
     - 数据类型
     - 描述
   * - pagination
     - false
     - Pagination请求结构体
     - 分页参数。见 `Pagination请求结构体>> </docs/api/zh_CN/2.0.9/overview.html#pagination>`__。若不提供，则默认按照每页1000条数据的格式返回第0页的数据。


## 响应参数

.. list-table::
   :widths: auto
   :header-rows: 1

   * - 名称
     - 数据类型
     - 描述
   * - data
     - data结构体
     - 以分页列表展示用户信息



### data结构体

.. list-table::
   :widths: auto
   :header-rows: 1

   * - 名称
     - 数据类型
     - 描述
   * - pagination
     - Pagination结构体
     - 分页信息
   * - users
     - UserDTO结构体
     - 用户信息列表


### Pagination结构体

.. list-table::
   :widths: auto
   :header-rows: 1

   * - 名称
     - 数据类型
     - 描述
   * - pageNo
     - Integer
     - 请求页数
   * - pageSize
     - Integer
     - 每页记录数
   * - totalElements
     - Long
     - 总记录数



### UserDTO结构体

.. list-table::
   :widths: auto
   :header-rows: 1

   * - 名称
     - 数据类型
     - 描述
   * - id
     - String
     - 用户的ID
   * - name
     - String
     - 用户名
   * - domain
     - String
     - 域名称
   * - description
     - String
     - 用户描述
   * - nickName
     - String
     - 用户昵称
   * - phoneArea
     - String
     - 用户注册电话的区号
   * - phone
     - String
     - 用户的注册手机号码
   * - email
     - String
     - 用户的注册邮箱
   * - createdTime
     - String
     - 用户账户创建时间
   * - joinTime
     - String
     - 用户加入当前组织的时间
   * - type
     - Integer
     - 用户类型，0：App Portal账号，1：第三方域账号
   * - exists
     - Boolean
     - 用户是否在当前组织，true：存在，false：不存在，null：未启用

## 示例

### 请求示例

```
POST http://{apigw-address}/app-portal-service/v2.0/organization/user/list
headers: {"Authorization":"Bearer APP_PORTAL_S_TDKKeqfYBK3m5z3LRgKVqThWDYnRBN44"}
body: {
    "pageNo":0,
    "pageSize":5,
    "sorters":[]
}
```

### 返回示例

```json
{
    "code": 200,
    "message": "",
    "data": {
        "pagination": {
            "totalElements": 81,
            "pageNo": 0,
            "pageSize": 5
        },
        "users": [
            {
                "id": "u15692059719411",
                "name": "asd@aaa.com",
                "domain": "新增域测试",
                "description": "",
                "nickName": "",
                "phoneArea": "",
                "phone": "",
                "email": "asd@aaa.com",
                "createdTime": "2019-09-23 02:32:51.0",
                "joinTime": "2019-09-23 02:32:52.0",
                "type": 1
            },
            {
                "id": "u15689619940171",
                "name": "12345@qq.com",
                "domain": "yangfantest",
                "description": "",
                "nickName": "",
                "phoneArea": "",
                "phone": "",
                "email": "12345@qq.com",
                "createdTime": "2019-09-20 06:46:34.0",
                "joinTime": "2019-09-20 06:46:34.0",
                "type": 1
            },
            {
                "id": "u15688814574861",
                "name": "435",
                "domain": "",
                "description": "",
                "nickName": "",
                "phoneArea": "",
                "phone": "",
                "email": "435@qq.com",
                "createdTime": "2019-09-19 08:24:17.0",
                "joinTime": "2019-09-19 08:24:17.0",
                "type": 0
            },
            {
                "id": "u15592020911321",
                "name": "jiajie.chen",
                "domain": "",
                "description": "",
                "nickName": "",
                "phoneArea": "",
                "phone": "",
                "email": "jiajie.chen@envision-digital.com",
                "createdTime": "2019-05-30 07:41:31.0",
                "joinTime": "2019-09-11 09:42:54.0",
                "type": 0
            },
            {
                "id": "u15578231118721",
                "name": "portal_test01",
                "domain": "",
                "description": "",
                "nickName": "quququ",
                "phoneArea": "",
                "phone": "123232323",
                "email": "portaltest01@email.com",
                "createdTime": "2019-05-14 08:38:31.0",
                "joinTime": "2019-09-06 14:09:01.0",
                "type": 0
            }
        ]
    }
}
```


# Get Asset Structure   

获取资产所在的组织的上游组织结构。



## 请求格式

```
GET http://{apigw-address}/app-portal-service/v2.0/asset/structure
```


## 请求参数（Header）


.. list-table::
   :widths: auto
   :header-rows: 1

   * - 名称
     - 是否必须
     - 数据类型
     - 描述
   * - Authorization
     - true
     - String
     - Access token，以Bearer Token表示。



## 响应参数


.. list-table::
   :widths: auto
   :header-rows: 1

   * - 名称
     - 数据类型
     - 描述
   * - data
     - data结构体
     - 组织结构



### data结构体

.. list-table::
   :widths: auto
   :header-rows: 1

   * - 名称
     - 数据类型
     - 描述
   * - structures
     - AssetStructure结构体
     - 组织结构树列表


### AssetStructure结构体

.. list-table::
   :widths: auto
   :header-rows: 1

   * - 名称
     - 数据类型
     - 描述
   * - id
     - String
     - 组织结构ID
   * - name
     - String
     - 组织结构名称
   * - description
     - String
     - 组织描述
   * - organizationId
     - String
     - 组织结构所在的组织ID
   * - children
     - AssetStructure结构体
     - 下层组织结构



## 示例

### 请求示例

```
GET http://{apigw-address}/app-portal-service/v2.0/asset/structure
headers: {"Authorization":"Bearer APP_PORTAL_S_TDKKeqfYBK3m5z3LRgKVqThWDYnRBN44"}
```


### 返回示例

```json
{
  "code": 200,
  "data": {
    "structures": [
      {
        "children": [],
        "description": "",
        "displayName": "wyf",
        "id": "sg15645784491861",
        "name": "wyf",
        "organizationId": "o15589308944781"
      }
    ]
  },
  "message": ""
}
```

# Get User Information

获得当前用户的信息。


## 请求格式

```
GET http://{apigw-address}/app-portal-service/v2.0/user/info
```


## 请求参数（Header）

.. list-table::
   :widths: auto
   :header-rows: 1

   * - 名称
     - 是否必须
     - 数据类型
     - 描述
   * - Authorization
     - true
     - String
     - Access token，以Bearer Token表示。


## 响应参数

.. list-table::
   :widths: auto
   :header-rows: 1

   * - 名称
     - 数据类型
     - 描述
   * - data
     - data结构体
     - 用户信息



### data结构体


.. list-table::
   :widths: auto
   :header-rows: 1

   * - 名称
     - 数据类型
     - 描述
   * - id
     - String
     - 用户的ID
   * - name
     - String
     - 用户名
   * - domain
     - String
     - 域名称
   * - description
     - String
     - 用户描述
   * - nickName
     - String
     - 用户昵称
   * - phoneArea
     - String
     - 用户注册电话的区号
   * - phone
     - String
     - 用户的注册手机号码 
   * - email
     - String
     - 用户的注册邮箱
   * - createdTime
     - String
     - 用户账户创建时间
   * - joinTime
     - String
     - 用户加入当前组织的时间
   * - type
     - Integer
     - 用户类型，0：App Portal账号，1：第三方域账号



## 示例

### 请求示例

```
GET http://{apigw-address}/app-portal-service/v2.0/user/info
headers: {"Authorization":"Bearer APP_PORTAL_S_TDKKeqfYBK3m5z3LRgKVqThWDYnRBN44"}
```

### 返回示例

```json
{
  "code": 200,
  "message": "",
  "data": {
    "id": "u15589316109091",
    "name": "portal_demo",
    "domain": "",
    "description": "",
    "nickName": "",
    "phoneArea": "",
    "phone": "",
    "email": "1@163.com",
    "createdTime": "2019-05-27 04:33:30.0",
    "type": 0
  }
}
```


# Get App User List

根据`appId`获得当前用户权限范围内对该应用可见的用户列表信息。


## 请求格式

```
GET http://{apigw-address}/app-portal-service/v2.0/user/list
```

## 请求参数（Header）

.. list-table::
   :widths: auto
   :header-rows: 1

   * - 名称
     - 位置
     - 是否必须
     - 数据类型
     - 描述
   * - Authorization
     - Header
     - true
     - String
     - Access token，以Bearer Token表示。
   * - appId
     - Query
     - true
     - String
     - 应用的ID 

## 响应参数

.. list-table::
   :widths: auto
   :header-rows: 1

   * - 名称
     - 数据类型
     - 描述
   * - data
     - data结构体 
     - 用户信息列表

### data结构体

.. list-table::
   :widths: auto
   :header-rows: 1

   * - 名称
     - 数据类型
     - 描述
   * - users
     - ApiUserDTO结构体 
     - 用户信息


### ApiUserDTO结构体


.. list-table::
   :widths: auto
   :header-rows: 1

   * - 名称
     - 数据类型
     - 描述
   * - userId
     - String
     - 用户ID
   * - email
     - String
     - 用户的注册邮箱
   * - phoneArea
     - String
     - 用户注册电话的区号
   * - phone
     - String
     - 用户注册手机号码
   * - name
     - String
     - 用户名


## 示例

### 请求示例

```
GET http://apim-apigw-proxy.beta-k8s-cn4.eniot.io/app-portal-service/v2.0/user/list?appId=8831c608-d17c-4132-b5e0-99547e4c4758  
```

### 返回示例

```json
{
  "code": 200,
  "message": "",
  "data": {
    "users": [
      {
        "userId": "u15665532373241",
        "email": "1123456666@Fsn.sg",
        "phoneArea": "",
        "phone": "",
        "name": "1123456666@Fsn.sg"
      },
      {
        "userId": "u15665405431611",
        "email": "1qaz@ws.sx",
        "phoneArea": "",
        "phone": "",
        "name": "1qaz"
      }
    ]
  }
}
```



# Update Messages

更新消息状态。

## 请求格式

```
POST http://{apigw-address}/app-portal-service/v2.0/message/update
```

## 请求参数（Body）

.. list-table::
   :widths: auto
   :header-rows: 1

   * - 名称
     - 是否必须
     - 数据类型
     - 描述
   * - messages
     - true
     - MessageUpdateDTO结构体
     - 需要更新的消息列表 


### MessageUpdateDTO结构体

.. list-table::
   :widths: auto
   :header-rows: 1

   * - 名称
     - 是否必须
     - 数据类型
     - 描述
   * - messageId
     - true
     - String
     - 消息ID
   * - appId
     - true
     - String
     - 应用ID
   * - state
     - true
     - int
     - 消息状态。0：未处理，1：已处理 



## 响应参数

.. list-table::
   :widths: auto
   :header-rows: 1

   * - 名称
     - 数据类型
     - 描述
   * - data
     - data结构体
     - （空）



## 示例

### 请求示例

```
POST http://{apigw-address}/app-portal-service/v2.0/message/update
{
  "messages": [
    {
      "appId": "4af99583-1c66-4fd0-ba75-0ace6da61bcd",
      "messageId": "TestMessage0150000927",
      "state": 1
    }
  ]
}
```

### 返回示例

```json
{
  "code": 200,
  "message": "",
  "data": null
}
```

# Create Message

创建消息。


## 请求格式

```
POST http://{apigw-address}/app-portal-service/v2.0/message/produce
```

## 请求参数（Body）

.. list-table::
   :widths: auto
   :header-rows: 1

   * - 名称
     - 是否必须
     - 数据类型
     - 描述
   * - messages
     - true
     - MessageProduceDTO结构体
     - 产生的消息 


### MessageProduceDTO结构体

.. list-table::
   :widths: auto
   :header-rows: 1

   * - 名称
     - 是否必须
     - 数据类型
     - 描述
   * - messageId
     - true
     - String
     - 告警消息ID
   * - type
     - false
     - int
     - 消息类型，0：普通消息，1：告警消息
   * - organizationId  
     - true
     - String
     - 组织ID
   * - appId
     - true
     - String
     - 应用ID
   * - body
     - false
     - I18nString
     - message display body, keys: en_US, zh_CN, default，消息body <!--国际化告警信息。结构请见国际化名称结构体>>-->
   * - color
     - false
     - int
     - 消息严重级别颜色标识
   * - ring
     - false
     - int
     - 消息的声音类型
   * - tags
     - false
     - I18nString 
     - 消息的标签。只展示前三个。tags, keys: en_US, zh_CN, default，标签列表 
   * - produceTime
     - true
     - String
     - message produce time, format: "yyyy-MM-dd HH:mm:ss"  告警消息生成时间，以UTC时间表示。
   * - zoneOffset
     - true
     - String
     - 时区。如"+08:00"
   * - linkedAppId
     - false
     - String
     - 与告警消息关联的应用的ID。（linkedAppId，linkedMenuCode，linkedStates三者构成跳转链接URL，如https://{apigw-address}/portal/60d110ff-f388-48f4-916b-9e637d4886af/alarmProcessing?state=site%253DeVKqg4zr,其中linkedAppId=60d110ff-f388-48f4-916b-9e637d4886af，linkedMenuCode=alarmProcessing，linkedStates=site%253DeVKqg4zr）
   * - linkedMenuCode
     - false
     - String
     - 与消息关联的应用内的菜单标识符
   * - linkedStates
     - false
     - String
     - message linked states，与消息关联的URL state
   * - feature
     - false
     - I18nString <!--StringI18n？-->
     - feature name,keys: en_US, zh_CN, default  用户自定义描述。
   * - assetId
     - false
     - String
     - 与告警消息相关的资产的ID。若告警消息与资产无关，则可不提供。
   * - authUnitId
     - true
     - String
     - 在EnOS平台的资产树中打了“auth_unit:true”标签的资产，可以是assetId，也可能是assetId的祖先节点。同步到App Portal中的资产ID，用于校验应用对此资产的权限。如一个光伏电站下有若干个光伏面板，每个光伏面板有各自的资产ID：assetId1，assetId2等。此光伏电站在EnOS平台的资产树被打了“auth_unit:true”的标签。当此光伏电站被成功同步到Application Portal后（authUnitId有效），如果某个组织拥有appId表示的应用，那么在Application Portal中对光伏面板这一资产可见的用户可以收到相应的告警消息。在此例中，assetId为某个光伏面板的ID，authUnitId为光伏电站ID。<!--另一个例子，在enos平台的资产树中某个光伏电站的id为assetId，同时这个光伏电站被打了auth_unit:true的tag，那么这个光伏电站会作为资产被同步到app-portal中，那么在调用此api时，assetId与authUnitId相同（均表示此光伏电站)，在app-portal中对此资产可见的用户会收到告警消息；一条告警消息有效的条件是：资产被同步到app-portal中并且推送消息中的ou拥有此appId的权限-->


## 响应参数

.. list-table::
   :widths: auto
   :header-rows: 1

   * - 名称
     - 数据类型
     - 描述
   * - data
     - data结构体
     - null


## 示例

### 请求示例

```
POST http://{apigw-address}/app-portal-service/v2.0/message/produce
{
  "messages": [
    {
      "zoneOffset": "+08:00",
      "linkedMenuCode": "menucode",
      "linkedAppId": "appid",
      "color": 1,
      "ring": 1,
      "messageId": "yunfan01",
      "produceTime": "24/7/2019 11:22:01",
      "body": {
        "default": "This is a test3335",
        "en_US": "This is a test3335",
        "zh_CN": "这是个测试233335"
      },
      "type": 1,
      "tags": [
        {
          "default": "Severe",
          "en_US": "Severe",
          "zh_CN": "严重"
        },
        {
          "default": "Performance Alarm",
          "en_US": "Performance Alarm",
          "zh_CN": "性能告警"
        },
        {
          "default": "Inverter",
          "en_US": "Inverter",
          "zh_CN": "逆变器"
        }
      ],
      "organizationId": "o15639623061491",
      "createdAt": "24/7/2019 10:11:18",
      "authUnitId": "7Uq6uP77",
      "deletedAt": "1/1/1970 00:00:00",
      "feature": {
        "default": "This is a feature test3343",
        "en_US": "This is a feature test3343",
        "zh_CN": "这是个特征测试1"
      },
      "assetId": "7Uq6uP77",
      "appId": "4af99583-1c66-4fd0-ba75-0ace6da61bcd",
      "state": 0,
      "linkedStates": "states",
      "updatedAt": "24/7/2019 10:11:18"
    }
  ]
}
```

### 返回示例

```json
{
  "code": 200,
  "message": "",
  "data": null
}
```

# Get Message Ringtones

获取消息提示声。

## 请求格式

```
GET http://{apigw-address}/app-portal-service/v2.0/message/enum/ringtones
```


## 响应参数


.. list-table::
   :widths: auto
   :header-rows: 1

   * - 名称
     - 数据类型
     - 描述
   * - data
     - data结构体
     - 消息提示声列表


### data结构体

.. list-table::
   :widths: auto
   :header-rows: 1

   * - 名称
     - 数据类型
     - 描述
   * - ringings
     - Ringing结构体
     - 消息提示声列表


### Ringing结构体

.. list-table::
   :widths: auto
   :header-rows: 1

   * - 名称
     - 数据类型
     - 描述
   * - id
     - int
     - 消息提示声的ID
   * - name
     - I18nString   <!--StringI18n？-->
     - 消息提示声的国际化名称


## 示例

### 请求示例

```
GET http://{apigw-address}/app-portal-service/v2.0/message/enum/ringtones
```

### 返回示例

```json
{
  "code": 200,
  "message": "",
  "data": {
    "ringings": [
      {
        "id": 0,
        "name": {
          "default": "No Sound",
          "en_US": "No Sound",
          "zh_CN": "无声音"
        }
      },
      {
        "id": 1,
        "name": {
          "default": "Alarm Sound",
          "en_US": "Alarm Sound",
          "zh_CN": "警报声"
        }
      }
    ]
  }
}
```

# Get Message Severity Indication Color

获取用于表示消息严重程度的颜色列表。


## 请求格式

```
GET http://{apigw-address}/app-portal-service/v2.0/message/enum/colors
```

## 响应参数

.. list-table::
   :widths: auto
   :header-rows: 1

   * - 名称
     - 数据类型
     - 描述
   * - data
     - data结构体
     - 颜色列表

### data结构体

.. list-table::
   :widths: auto
   :header-rows: 1

   * - 名称
     - 数据类型
     - 描述
   * - colors
     - Color结构体
     - 消息颜色列表


### Color结构体

.. list-table::
   :widths: auto
   :header-rows: 1

   * - 名称
     - 数据类型
     - 描述
   * - id
     - int
     - 表示颜色的ID
   * - name
     - I18nString   <!--StringI18n？-->
     - 颜色的国际化名称



## 示例

### 请求示例

```
GET http://{apigw-address}/app-portal-service/v2.0/message/enum/colors
```

### 返回示例

```json
{
  "code": 200,
  "message": "",
  "data": {
    "colors": [
      {
        "id": 0,
        "name": {
          "default": "red",
          "en_US": "red",
          "zh_CN": "红色"
        }
      },
      {
        "id": 1,
        "name": {
          "default": "Yellow ",
          "en_US": "Yellow ",
          "zh_CN": "黄色"
        }
      },
      {
        "id": 2,
        "name": {
          "default": "Gray",
          "en_US": "Gray",
          "zh_CN": "灰色"
        }
      }
    ]
  }
}
```


# Check Asset Permission

查看是否有资产的权限。


## 请求格式

```
POST http://{apigw-address}/app-portal-service/v2.0/user/authorization/asset/check
```

## 请求参数（Header）

.. list-table::
   :widths: auto
   :header-rows: 1

   * - 名称
     - 是否必须
     - 数据类型
     - 描述
   * - Authorization
     - true
     - String
     - Access token，以Bearer Token表示。


## 请求参数（Body）

.. list-table::
   :widths: auto
   :header-rows: 1

   * - 名称
     - 是否必须
     - 数据类型
     - 描述
   * - assetIds
     - true
     - String
     - 资产ID，支持查询多个资产，多个资产ID之间用英文逗号隔开。如何获取Asset ID信息>>


## 响应参数

.. list-table::
   :widths: auto
   :header-rows: 1

   * - 名称
     - 数据类型
     - 描述
   * - data
     - boolean
     - 对所有查询资产有权限，返回true，对部分或所有资产没有权限，则返回false



## 示例

### 请求示例

```
POST http://{apigw-address}/app-portal-service/v2.0/user/authorization/asset/check
headers: {"Authorization":"Bearer APP_PORTAL_S_TDKKeqfYBK3m5z3LRgKVqThWDYnRBN44"}
body:{
  "assetIds": [
    "rJDyH3Rm",
    "FS6c3XAH",
    "qQHC4vyw",
    "txeiiU9x",
    "adNIljjB",
    "Dqp9GZsT",
    "Mk2BVzZN"
  ]
}
```

### 返回示例
```json
{
  "code": 200,
  "message": "",
  "data": false
}
```

# Get Asset List

查询当前用户在某个应用下有权限的所有资产的资产列表。


## 请求格式

```
GET http://{apigw-address}/app-portal-service/v2.0/user/app/asset/tree
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
   * - appId
     - Query
     - true
     - String
     - 应用ID


## 请求参数（Header）

.. list-table::
   :widths: auto
   :header-rows: 1

   * - 名称
     - 是否必须
     - 数据类型
     - 描述
   * - Authorization
     - true
     - String
     - Access token，以Bearer Token表示。



## 响应参数

.. list-table::
   :widths: auto
   :header-rows: 1

   * - 名称
     - 数据类型
     - 描述
   * - data
     - data结构体
     - 资产树信息   <!--不确定-->

### data结构体

.. list-table::
   :widths: auto
   :header-rows: 1

   * - 名称
     - 数据类型
     - 描述
   * - id
     - String
     - 节点ID
   * - name
     - String
     - 节点名称
   * - tag
     - String
     - 节点标签，如果当前节点为资产，则标签为"asset"，否则此节点为组织结构节点，对应标签为null。（由于资产只能挂载到组织结构的叶子节点上，所以当此标签为"asset"时，必有父节点且父节点为组织结构节点，同时必然没有子节点。
   * - parentId
     - String
     -父节点ID
   * - children
     - data结构体列表
     - 子节点



## 示例

### 请求示例

```
GET http://{apigw-address}/app-portal-service/v2.0/user/app/asset/tree?appId=app_1
headers: {"Authorization":"Bearer APP_PORTAL_S_TDKKeqfYBK3m5z3LRgKVqThWDYnRBN44"}
```

### 返回示例

```json 
{
  "id": "sg15663523816801",
  "name": "Solar_shangHai",
  "tag": null,
  "parentId": "",
  "children": [
    {
      "id": "sg15663524029331",
      "name": "江阴",
      "tag": null,
      "parentId": "sg15663523816801",
      "children": [
        {
          "id": "zULM004t",
          "name": "Solar_Assert",
          "tag": "asset",
          "parentId": "",
          "children": null
        },
        {
          "id": "osvxGtJC",
          "name": "shangHai",
          "tag": "asset",
          "parentId": "",
          "children": null
        }
      ]
    }
  ]
}
```


# Get App Menu and Permission

获取应用的权限点及菜单列表。

## 请求格式

```
GET http://{apigw-address}/app-portal-service/v2.0/user/app/resource/info
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
   * - appId
     - Query
     - true
     - String
     - 应用ID


## 请求参数（Header）

.. list-table::
   :widths: auto
   :header-rows: 1

   * - 名称
     - 是否必须
     - 数据类型
     - 描述
   * - Authorization
     - true
     - String
     - Access token，以Bearer Token表示。



## 响应参数

.. list-table::
   :widths: auto
   :header-rows: 1

   * - 名称
     - 数据类型
     - 描述
   * - data
     - data结构体
     - 权限点和菜单列表

### data结构体

.. list-table::
   :widths: auto
   :header-rows: 1

   * - 名称
     - 数据类型
     - 描述
   * - permissions
     - Permission列表
     - 权限点列表
   * - menus
     - Menu列表
     - 菜单列表

### Permission列表

.. list-table::
   :widths: auto
   :header-rows: 1

   * - 名称
     - 数据类型
     - 描述
   * - id
     - String
     - 权限点id
   * - code
     - String
     - 权限点唯一标识符  <!--identifier? EnOS中是Identifier-->
   * - name
     - String
     - 权限点名称


### Menu列表

.. list-table::
   :widths: auto
   :header-rows: 1

   * - 名称
     - 数据类型
     - 描述
   * - id
     - String
     - 菜单ID
   * - name
     - String
     - 菜单名称
   * - code
     - String
     - 菜单唯一标识符  <!--identifier? EnOS中是Identifier-->
   * - displayOrder
     - Integer
     - 菜单展示排序，表示当前菜单在其所在层级内的排序，值为从1开始的整数，序号越小的菜单越排在上方
   * - url
     - String
     - 菜单URL
   * - parentId
     - String
     - 上级菜单
   * - children
     - Menu结构体
     - 下级菜单



## 示例

### 请求示例

```
GET http://{apigw-address}/app-portal-service/v2.0/user/app/resource/info?appId=app_1
headers: {"Authorization":"Bearer APP_PORTAL_S_TDKKeqfYBK3m5z3LRgKVqThWDYnRBN44"}
```

### 返回示例

```json
{
  "code": 200,
  "message": "",
  "data": {
    "permissions": [],
    "menus": [
      {
        "id": "4658d768-42d6-4f8f-98aa-de176c5e9d09",
        "code": "menu",
        "name": "menu",
        "url": "/a",
        "displayOrder": 1,
        "parentId": "",
        "children": []
      },
      {
        "id": "2aff0920-d1e8-4033-95fb-cb60c5adf5c8",
        "code": "menu2",
        "name": "menu2",
        "url": "/eos-wind-map/assetOverview.html",
        "displayOrder": 2,
        "parentId": "",
        "children": []
      }
    ]
  }
}
```


# Get Token Information

获取Access Token所对应的当前登录用户的相关信息。

## 请求格式

```
GET http://{apigw-address}/app-portal-service/v2.0/session/info
```

## 请求参数（Header）

.. list-table::
   :widths: auto
   :header-rows: 1

   * - 名称
     - 是否必须
     - 数据类型
     - 描述
   * - Authorization
     - true
     - String
     - Access token，以Bearer Token表示。



## 响应参数

.. list-table::
   :widths: auto
   :header-rows: 1

   * - 名称
     - 数据类型
     - 描述
   * - data
     - data结构体
     - null

### data结构体

.. list-table::
   :widths: auto
   :header-rows: 1

   * - 名称
     - 数据类型
     - 描述
   * - userId
     - String
     - 用户ID
   * - userName
     - String
     - 用户名
   * - workingOrganizationId   <!----currentOrgId?>
     - String
     - 当前组织ID
   * - workingOrganizationName   <!--currentOrgName?-->
     - String
     - 当前组织名称



## 示例

### 请求示例

```
GET http://{apigw-address}/app-portal-service/v2.0/session/info
headers: {"Authorization":"Bearer APP_PORTAL_S_TDKKeqfYBK3m5z3LRgKVqThWDYnRBN44"}
```

### 返回示例

```
{
  "code": 200,
  "message": "",
  "data": {
    "userId": "u15589316109091",
    "userName": "portal_demo",
    "workingOrganizationId": "o15589308944781",
    "workingOrganizationName": "Portal Demo"
  }
}
```


# Refresh Access Token

使用Refresh Token请求一个新的Access Token。


## 请求格式

```
GET http://{apigw-address}/app-portal-service/v2.0/token/refresh
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
   * - refreshToken
     - Query
     - true
     - String
     - Refresh Token



## 响应参数

.. list-table::
   :widths: auto
   :header-rows: 1

   * - 名称
     - 数据类型
     - 描述
   * - data
     - data结构体
     - null

### data结构体

.. list-table::
   :widths: auto
   :header-rows: 1

   * - 名称
     - 数据类型
     - 描述
   * - userId
     - String
     - 用户ID
   * - userName
     - String
     - 用户名
   * - workingOrganizationId   <!----currentOrgId?>
     - String
     - 当前组织ID
   * - workingOrganizationName    <!----currentOrgName?>
     - String
     - 当前组织名称
   * - accessToken
     - String
     - 新的Access token，以Bearer Token表示
   * - refreshToken
     - String
     - 新的Refresh Token
   * - refreshTokenExpire
     - String
     - Refresh Token过期时间   <!--固定的时间,the difference, measured in milliseconds, between the current time and midnight, January 1, 1970 UTC.-->


## 示例

### 请求示例

```
GET http://{apigw-address}/app-portal-service/v2.0/token/refresh?refreshToken=xxx
headers: {"Authorization":"Bearer APP_PORTAL_S_TDKKeqfYBK3m5z3LRgKVqThWDYnRBN44"}
```

### 返回示例


```json
{
  "code": 200,
  "message": "",
  "data": {
    "userId": "u15589316109091",
    "userName": "portal_demo",
    "workingOrganizationId": "o15589308944781",
    "workingOrganizationName": "Portal Demo",
    "accessToken": "APP_PORTAL_S_w35R99d92ZX4McYQJQvWp42ydjdj3MjK",
    "refreshToken": "eyJhbGciOiJIUzI1NiJ9.eyJzdWIiOiJ1MTU1ODkzMTYxMDkwOTEiLCJhZG1pbkxldmVsIjoyLCJpc3MiOiJBUFAtUE9SVEFMIiwid29ya2luZ09yZ2FuaXphdGlvbklkIjoibzE1NTg5MzA4OTQ0NzgxIiwidXNlck5hbWUiOiJwb3J0YWxfZGVtbyIsIndvcmtpbmdPcmdhbml6YXRpb25OYW1lIjoiUG9ydGFsIERlbW8iLCJleHAiOjE1NzEzNjgzMTUsInVzZXJJZCI6InUxNTU4OTMxNjEwOTA5MSIsImlhdCI6MTU2ODc3NjMxNSwianRpIjoiand0X2lkIn0.XmFet0419rGX6EgKoNjjek6JlYPbeCXWdRrKxY9wwWs",
    "refreshTokenExpire": 1571368315000
  }
}
```


# Choose Organization

用户在登录后选择账号所在组织。

## 请求格式

```
POST http://{apigw-address}/app-portal-service/v2.0/session/set
```

## 请求参数（Header）

.. list-table::
   :widths: auto
   :header-rows: 1

   * - 名称
     - 是否必须
     - 数据类型
     - 描述
   * - Authorization
     - true
     - String
     - Access token，以Bearer Token表示。


## 请求参数（Body）

.. list-table::
   :widths: auto
   :header-rows: 1

   * - 名称
     - 是否必须
     - 数据类型
     - 描述
   * - organizationId
     - true
     - String
     - 组织ID



## 响应参数


.. list-table::
   :widths: auto
   :header-rows: 1

   * - 名称
     - 数据类型
     - 描述
   * - data
     - data结构体
     - 组织信息

### data结构体

.. list-table::
   :widths: auto
   :header-rows: 1

   * - 名称
     - 数据类型
     - 描述
   * - userId
     - String
     - 用户ID
   * - userName
     - String
     - 用户名
   * - workingOrganizationId   <!----currentOrgId?>
     - String
     - 当前组织ID
   * - workingOrganizationName    <!----currentOrgName?>
     - String
     - 当前组织名称
   * - accessToken
     - String
     - 请求中的 Access Token
   * - refreshToken
     - String
     - 新的Refresh Token
   * - refreshTokenExpire
     - String
     - Refresh Token过期时间    <!--单位？秒？还是一个固定的时间点？--> <!--同上-->



## 示例

### 请求示例

```
POST http://{apigw-address}/app-portal-service/v2.0/session/set
headers: {"Authorization":"Bearer APP_PORTAL_S_TDKKeqfYBK3m5z3LRgKVqThWDYnRBN44"}
body:{"organizationId":"o15589308944781"}
```

### 返回示例

```json
{
  "code": 200,
  "message": "",
  "data": {
    "userId": "u15589316109091",
    "userName": "portal_demo",
    "workingOrganizationId": "o15589308944781",
    "workingOrganizationName": "Portal Demo",
    "accessToken": "APP_PORTAL_S_tsNqGkfWGj9AW6qSHADEW4wuxAHQN3dN",
    "refreshToken": "eyJhbGciOiJIUzI1NiJ9.eyJzdWIiOiJ1MTU1ODkzMTYxMDkwOTEiLCJhZG1pbkxldmVsIjoyLCJpc3MiOiJBUFAtUE9SVEFMIiwid29ya2luZ09yZ2FuaXphdGlvbklkIjoibzE1NTg5MzA4OTQ0NzgxIiwidXNlck5hbWUiOiJwb3J0YWxfZGVtbyIsIndvcmtpbmdPcmdhbml6YXRpb25OYW1lIjoiUG9ydGFsIERlbW8iLCJleHAiOjE1NzAwMTg5NTgsInVzZXJJZCI6InUxNTU4OTMxNjEwOTA5MSIsImlhdCI6MTU2NzQyNjk1OCwianRpIjoiand0X2lkIn0.Ql1vNVvb0ok2uWzzU1jiBzAyvRdBOkzzfnHD4PLsi1E",
    "refreshTokenExpire": 1570018958000
  }
}
```

# List Organizations

根据Access Token列出当前用户所在的组织列表。

## 请求格式

```
GET http://{apigw-address}/app-portal-service/v2.0/user/organization/list
```

## 请求参数（Header）

.. list-table::
   :widths: auto
   :header-rows: 1

   * - 名称
     - 是否必须
     - 数据类型
     - 描述
   * - Authorization
     - true
     - String
     - Access token，以Bearer Token表示。


## 响应参数

.. list-table::
   :widths: auto
   :header-rows: 1

   * - 名称
     - 数据类型
     - 描述
   * - data
     - data结构体
     - 组织列表

### data结构体

.. list-table::
   :widths: auto
   :header-rows: 1

   * - 名称
     - 数据类型
     - 描述
   * - organizations
     - IdNamePair结构体
     - 组织列表详情

### IdNamePair结构体

.. list-table::
   :widths: auto
   :header-rows: 1

   * - 名称
     - 数据类型
     - 描述
   * - id
     - String
     - 组织ID
   * - name
     - String
     - 组织名称



## 示例

### 请求示例

```
GET http://{apigw-address}/app-portal-service/v2.0/user/organization/list
headers: {"Authorization":"Bearer APP_PORTAL_S_TDKKeqfYBK3m5z3LRgKVqThWDYnRBN44"}
```

### 返回示例

```json
{
  "code": 200,
  "message": "",
  "data": {
    "organizations": [
      {
        "id": "o15641320370691",
        "name": "rm_0726_001"
      },
      {
        "id": "o15589308944781",
        "name": "Portal Demo"
      }
    ]
  }
}
```


# Login
登录账号。

## 请求格式

```
POST http://{apigw-address}/app-portal-service/v2.0/login
```


## 请求参数（Body）

.. list-table::
   :widths: auto
   :header-rows: 1

   * - 名称
     - 是否必须
     - 数据类型
     - 描述
   * - account
     - true
     - String
     - 用户名
   * - password
     - true
     - String
     - 登录密码



## 响应参数


.. list-table::
   :widths: auto
   :header-rows: 1

   * - 名称
     - 数据类型
     - 描述
   * - data
     - data结构体
     - 用户信息

### data结构体

.. list-table::
   :widths: auto
   :header-rows: 1

   * - 名称
     - 数据类型
     - 描述
   * - organizations
     - IdNamePair结构体
     - 用户所在的组织列表
   * - user
     - IdNamePair结构体
     - 用户信息
   * - accessToken
     - String
     - Access token，以Bearer Token表示。

### IdNamePair结构体

.. list-table::
   :widths: auto
   :header-rows: 1

   * - 名称
     - 数据类型
     - 描述
   * - id
     - String
     - 用户ID
   * - name
     - String
     - 用户名




## 示例

### 请求示例

```
POST http://{apigw-address}/app-portal-service/v2.0/login
{"account":"portal_demo","password":"Test1234"}
```

### 返回示例

```json
{
  "code": 200,
  "data": {
    "accessToken": "APP_PORTAL_S_WX89rC4pqsMc478tyP6gb9zFmT9qYaW7",
    "organizations": [
      {
        "id": "o15589308944781",
        "name": "Portal Demo"
      },
      {
        "id": "o15641320370691",
        "name": "rm_0726_001"
      }
    ],
    "user": {
      "id": "u15589316109091",
      "name": "portal_demo"
    }
  },
  "message": ""
}
```




# Logout

登出账号。

## 请求格式

```
POST http://{apigw-address}/app-portal-service/v2.0/logout
```

## 请求参数（Headers）

.. list-table::
   :widths: auto
   :header-rows: 1

   * - 名称
     - 是否必须
     - 数据类型
     - 描述
   * - Authorization
     - true
     - String
     - Access token，以Bearer Token表示。



## 响应参数

.. list-table::
   :widths: auto
   :header-rows: 1

   * - 名称
     - 数据类型
     - 描述
   * - data
     - Boolean
     - null



## 示例

### 请求示例

```
POST http://{apigw-address}/app-portal-service/v2.0/logout
headers: {"Authorization":"Bearer APP_PORTAL_S_TDKKeqfYBK3m5z3LRgKVqThWDYnRBN44"}
```

### 返回示例

```
{
  "code":200,
  "message":"",
  "data":null
}
```

## Revoke Refresh Token

撤销用户所有Refresh Token。<!--这个销毁了有啥用？用户就不能继续访问portal了？--> <!--可以通过refreshToken来换取表示登陆态的accessToken，免去用户输入密码的步骤，可参考微信不用输密码一直登陆的场景。但是，当用户主动登出时，要使之前颁发出的refreshToken失效，防止安全问题-->

## 请求格式

```
POST http://{apigw-address}/app-portal-service/v2.0/refreshToken/revokeAll
```

## 请求参数（Header）

.. list-table::
   :widths: auto
   :header-rows: 1

   * - 名称
     - 是否必须
     - 数据类型
     - 描述
   * - Authorization
     - true
     - String
     - Access token，以Bearer Token表示。
   * - Content-Type
     - false
     - String
     - 返回内容的类型为application/x-www-form-urlencoded

<!--数据类型到底是String还是application/x-www-form-urlencoded？--> 
<!--类型是String，值是application/x-www-form-urlencoded-->

## 请求参数（Body）

.. list-table::
   :widths: auto
   :header-rows: 1

   * - 名称
     - 是否必须
     - 数据类型
     - 描述
   * - refreshToken
     - true
     - String
     - Refresh Token



## 响应参数

.. list-table::
   :widths: auto
   :header-rows: 1

   * - 名称
     - 数据类型
     - 描述
   * - data
     - Boolean
     - null



## 示例

### 请求示例

```
POST http://{apigw-address}/app-portal-service/v2.0/refreshToken/revokeAll
headers: {"Authorization":"Bearer APP_PORTAL_S_TDKKeqfYBK3m5z3LRgKVqThWDYnRBN44"}
body:{"refreshToken":"eyJhbGciOiJIUzI1NiJ9.eyJzdWIiOiJ1MTU1ODkzMTYxMDkwOTEiLCJhZG1pbkxldmVsIjoyLCJpc3MiOiJBUFAtUE9SVEFMIiwid29ya2luZ09yZ2FuaXphdGlvbklkIjoibzE1NTg5MzA4OTQ0NzgxIiwidXNlck5hbWUiOiJwb3J0YWxfZGVtbyIsIndvcmtpbmdPcmdhbml6YXRpb25OYW1lIjoiUG9ydGFsIERlbW8iLCJleHAiOjE1NzE0NTg4MTYsInVzZXJJZCI6InUxNTU4OTMxNjEwOTA5MSIsImlhdCI6MTU2ODg2NjgxNiwianRpIjoiand0X2lkIn0.QQRnhZt8xA_H1ScqpO6bKumXydJgyWTc7ItoZGbujj8"}
```

### 返回示例

```json
{
  "code":200,
  "message":"",
  "data":null
}
```
