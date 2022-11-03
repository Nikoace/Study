## 概要

AWS CDK[应用程序](https://docs.aws.amazon.com/cdk/v2/guide/apps.html)是用 TypeScript、JavaScript、Python、Java、C# 或 Go 编写的应用程序，它使用 AWS CDK 定义 AWS 基础设施。一个应用程序定义一个或多个[堆栈](https://docs.aws.amazon.com/cdk/v2/guide/stacks.html)。堆栈（相当于 AWS CloudFormation 堆栈）包含[结构](https://docs.aws.amazon.com/cdk/v2/guide/constructs.html)。每个构造定义一个或多个具体的 AWS 资源，例如 Amazon S3 存储桶、Lambda 函数或 Amazon DynamoDB 表。

构造（以及堆栈和应用程序）在您选择的编程语言中表示为类（类型）。您在堆栈中实例化构造以向 AWS 声明它们，并使用定义明确的接口将它们相互连接。

AWS CDK 包括 CDK 工具包（也称为 CLI），这是一个用于处理您的 AWS CDK 应用程序和堆栈的命令行工具。除其他功能外，工具包还提供执行以下操作的能力：

-   将一个或多个 AWS CDK 堆栈转换为 AWS CloudFormation 模板和相关资产（称为_综合_的过程）
-   将您的堆栈部署到 AWS 账户

AWS CDK 包含一个名为 AWS Construct Library 的 AWS 构造库，它被组织成各种模块。该库包含每个 AWS 服务的构造。主 CDK 包称为`aws-cdk-lib`，它包含 AWS Construct Library 的大部分内容。它还包含在大多数 CDK 应用程序中使用的`Stack`和 类似的基类。`App`

## 安装及引导启动AWS账户（Node.js） V1

-  安装 AWS CDK CLI
``` bash
npm install -g aws-cdk
```

- 验证安装
``` bash
cdk --version
```

- 引导启动 AWS 账户
``` bash
# Get the account ID 
aws sts get-caller-identity 
# Bootstrap the account 
cdk bootstrap aws://ACCOUNT-NUMBER/REGION
```

## 创建应用程序

- 新建工程文件夹
- 使用`cdk init app --language <language> ` 初始化工程。在有`git`环境时，初始化工程会自动创建为git工程
- 工程结构
![[Pasted image 20221030112742.png]]
hello-cdk-stack.ts
![[Pasted image 20221030113025.png]]

## 部署工程

``` shell
cdk deploy
```

``` shell
cdk destroy
```

## 最佳实践

借助 AWS CDK，开发人员或管理员可以使用受支持的编程语言定义他们的云基础设施。CDK 应用程序应组织成逻辑单元，例如 API、数据库和监控资源，并可选择具有用于自动化部署的管道。逻辑单元应作为结构实现，包括以下内容：

-   基础设施（例如 Amazon S3 存储桶、Amazon RDS 数据库或 Amazon VPC 网络）
-   运行时代码（例如 AWS Lambda 函数）
-   配置代码

堆栈定义了这些逻辑单元的部署模型。有关 CDK 背后概念的更详细介绍，请参阅[AWS CDK 入门](https://docs.aws.amazon.com/cdk/v2/guide/getting_started.html)。

AWS CDK 反映了对我们客户和内部团队的需求以及复杂云应用程序的部署和持续维护期间经常出现的故障模式的仔细考虑。我们发现故障通常与未经过全面测试的应用程序的“带外”更改有关，例如配置更改。因此，我们围绕一个模型开发了 AWS CDK，在该模型中，您的整个应用程序都在代码中定义，不仅包括业务逻辑，还包括基础设施和配置。这样，可以仔细审查提议的更改，在不同程度上类似于生产的环境中进行全面测试，并在出现问题时完全回滚。