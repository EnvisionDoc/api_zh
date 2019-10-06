# API鉴权

EnOS API身份验证采用服务账号SA（service account）作为应用或者开发者的身份。在REST API请求中将SA发送到EnOS服务，通过它验证用户身份并执行所需的授权访问。 

## 获取服务账号

服务账号SA由应用的 `AccessKey` 和 `SecretKey` 组成，需要通过在EnOS控制台注册应用生成，具体步骤如下：

1. 登录EnOS控制台，在左侧导航栏中选择 **应用注册**。
2. 点击 **创建应用** 按钮，输入新应用的详细信息后，点击 **确认**。
3. 应用注册完成之后，在 **组织应用** 标签下，点击应用名称，打开 **应用详情** 页面，查看应用的 `AccessKey` 和 `SecretKey` 。

## 授权服务账号

必须对服务账号进行授权之后，应用程序才有权访问EnOS上被授权的资源。对服务账号授权的详细步骤，请参考[管理服务账号](/docs/enos/zh_CN/latest/iam/howto/service_account/managing_service_account.html)。

## API操作权限

在授权服务账号前，需创建相应的权限策略。各API接口需要访问的资源和相应的操作权限说明如下：

| 接口名称                       | 所需授权              | 所需操作权限 |
| ------------------------------ | --------------------- | ------------ |
| Get Electric Power             | Asset                 | Read         |
| Get Current Day Electric Power | Asset                 | Read         |
| Filter Latest Data             | Asset                 | Read         |
| Get Latest Data                | Asset                 | Read         |
| Get Generic Data               | Asset                 | Read         |
| Get DI Data                    | Asset                 | Read         |
| Get AI Normalized Data         | Asset                 | Read         |
| Get AI Data                    | Asset                 | Read         |
| Get Raw Data                   | Asset                 | Read         |
| Get TSDB Storage Policy        | Asset                 | Read         |
| UpdateAsset                    | Asset                 | Write        |
| AssociateAssetNode             | Asset Tree Management | Full-Access  |
| DeleteAssetNode                | Asset Tree Management | Full-Access  |
| CreateAssetNode                | Asset Tree Management | Full-Access  |
| Cancel Command                 | Device Management     | Full-Access  |
| Set Measurepoint               | Asset                 | Control      |
| Invoke Service                 | Asset                 | Control      |
| Create Product                 | Device Management     | Full-Access  |
| Update Product                 | Device Management     | Full-Access  |
| Delete Product                 | Device Management     | Full-Access  |
| Disable Device                 | Device Management     | Full-Access  |
| Enable Device                  | Device Management     | Full-Access  |
| Delete Device                  | Device Management     | Full-Access  |
| Create Device                  | Device Management     | Full-Access  |
| Update Device                  | Device Management     | Full-Access  |
| Add Sub-device                 | Device Management     | Full-Access  |
| Remove Sub-device              | Device Management     | Full-Access  |

创建权限策略的详细步骤，请参考[创建和管理策略](/docs/iam/zh_CN/latest/howto/managing_policies.html)。