---
title: 在本地开发并运行 Azure Functions | Microsoft Docs
description: 了解如何在本地计算机上对 Azure 函数进行编码和测试，然后在 Azure Functions 中运行。
services: functions
documentationcenter: na
author: ggailey777
manager: cfowler
editor: ''
ms.assetid: 242736be-ec66-4114-924b-31795fd18884
ms.service: functions
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: multiple
ms.topic: article
ms.date: 06/03/2018
ms.author: glenga
ms.openlocfilehash: 5613b6b30d97b88bdfa6b00f90e334f1756ad614
ms.sourcegitcommit: 6f6d073930203ec977f5c283358a19a2f39872af
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/11/2018
ms.locfileid: "35294469"
---
# <a name="code-and-test-azure-functions-locally"></a>在本地对 Azure Functions 进行编码和测试

虽然 [Azure 门户]提供了一整套用于开发和测试 Azure Functions 的工具，但许多开发人员更喜欢本地开发体验。 Azure Functions 方便用户使用其喜欢的代码编辑器和本地开发工具在本地计算机上开发和测试函数。 其函数可在 Azure 中触发事件，并且用户可以在本地计算机上调试 C# 和 JavaScript 函数。 

如果是 Visual Studio C# 开发人员，Azure Functions 还可以[与 Visual Studio 2017 集成](functions-develop-vs.md)。

>[!IMPORTANT]  
> 不要将本地开发和门户开发混合在同一函数应用中。 从本地项目创建和发布函数时，不应尝试维护或修改门户中的项目代码。

## <a name="install-the-azure-functions-core-tools"></a>安装 Azure Functions Core Tools

[Azure Functions Core Tools] 是 Azure Functions 运行时的本地版本，可在本地开发计算机上运行。 它既不是仿真器，也不是模拟器。 它与在 Azure 中运行的 Functions 运行时相同。 有两个版本的 Azure Functions Core Tools：

+ [1.x 版](#v1)：支持 1.x 版运行时。 此版本仅在 Windows 计算机上受支持，是从 [npm 包](https://docs.npmjs.com/getting-started/what-is-npm)安装的。
+ [2.x 版](#v2)：支持 2.x 版运行时。 此版本支持 [Windows](#windows-npm)、[macOS](#brew) 和 [Linux](#linux)。 使用特定于平台的包管理器或 npm 进行安装。 

### <a name="v1"></a>1.x 版

工具的原始版本使用 Functions 1.x 运行时。 此版本使用 .NET Framework (4.7.1)，仅在 Windows 计算机上受支持。 在安装 1.x 版工具之前，必须[安装 NodeJS](https://docs.npmjs.com/getting-started/installing-node)，其中包含 npm。

使用以下命令安装 1.x 版工具：

```bash
npm install -g azure-functions-core-tools
```

### <a name="v2"></a>2.x 版

>[!NOTE]
> Azure Functions 运行时 2.0 处于预览版阶段，目前 Azure Functions 的全部功能并非都可受到支持。 有关详细信息，请参阅 [Azure Functions 版本](functions-versions.md)。 

2.x 版工具使用构建在 .NET Core 之上的 Azure Functions 运行时 2.x。 .NET Core 2.x 支持的所有平台（包括 [Windows](#windows-npm)、[macOS](#brew) 和 [Linux](#linux)）都支持此版本。

#### <a name="windows-npm"></a>Windows

以下步骤使用 npm 在 Windows 上安装 Core Tools。 也可使用 [Chocolatey](https://chocolatey.org/)。 有关详细信息，请参阅 [Core Tools 自述文件](https://github.com/Azure/azure-functions-core-tools/blob/master/README.md#windows)。

1. 安装[用于 Windows 的 .NET Core 2.0](https://www.microsoft.com/net/download/windows)。

2. 安装 [Node.js]，其中包括 npm。 对于 2.x 版工具，仅支持 Node.js 8.5 和更高版本。

3. 安装 Core Tools 包：

    ```bash
    npm install -g azure-functions-core-tools@core
    ```

#### <a name="brew"></a>带 Homebrew 的 MacOS

以下步骤使用 Homebrew 在 macOS 上安装 Core Tools。

1. 安装[用于 macOS 的 .NET Core 2.0](https://www.microsoft.com/net/download/macos)。

2. 安装 [Homebrew](https://brew.sh/)（如果尚未安装）。

3. 安装 Core Tools 包：

    ```bash
    brew tap azure/functions
    brew install azure-functions-core-tools 
    ```

#### <a name="linux"></a> 带 APT 的 Linux (Ubuntu/Debian)

以下步骤使用 [APT](https://wiki.debian.org/Apt) 在 Ubuntu/Debian Linux 发行版上安装 Core Tools。 有关其他 Linux 发行版，请参阅 [Core Tools 自述文件](https://github.com/Azure/azure-functions-core-tools/blob/master/README.md#linux)。

1. 安装[用于 Linux 的 .NET Core 2.0](https://www.microsoft.com/net/download/linux)。

2. 将 Microsoft 产品密钥注册为受信任的密钥：

    ```bash
    curl https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > microsoft.gpg
    sudo mv microsoft.gpg /etc/apt/trusted.gpg.d/microsoft.gpg
    ```

3. 验证你的 Ubuntu 服务器正在运行下表中的合适版本之一。 若要添加 apt 源，请运行：

    ```bash
    sudo sh -c 'echo "deb [arch=amd64] https://packages.microsoft.com/repos/microsoft-ubuntu-$(lsb_release -cs)-prod $(lsb_release -cs) main" > /etc/apt/sources.list.d/dotnetdev.list'
    sudo apt-get update
    ```

    | Linux 分发版 | 版本 |
    | --------------- | ----------- |
    | Ubuntu 17.10    | `artful`    |
    | Ubuntu 17.04    | `zesty`     |
    | Ubuntu 16.04/Linux Mint 18    | `xenial`  |

4. 安装 Core Tools 包：

    ```bash
    sudo apt-get install azure-functions-core-tools
    ```

## <a name="run-azure-functions-core-tools"></a>运行 Azure Functions Core Tools

Azure Functions Core Tools 添加了以下命令别名：

+ func
+ azfun
+ azurefunctions

在示例中显示的 `func` 位置，可以使用其中的任何别名。

```bash
func init MyFunctionProj
```

## <a name="create-a-local-functions-project"></a>创建本地 Functions 项目

在本地运行时，Functions 项目是包含 [host.json](functions-host-json.md) 和 [local.settings.json](#local-settings-file) 的目录。 此目录相当于 Azure 中的一个函数应用。 若要深入了解 Azure Functions 文件夹结构，请参阅 [Azure Functions 开发人员指南](functions-reference.md#folder-structure)。

在终端窗口中或者在命令提示符下，运行以下命令创建项目和本地 Git 存储库：

```bash
func init MyFunctionProj
```

输出如以下示例所示：

```output
Writing .gitignore
Writing host.json
Writing local.settings.json
Created launch.json
Initialized empty Git repository in D:/Code/Playground/MyFunctionProj/.git/
```

若要创建不包含本地 Git 存储库的项目，请使用 `--no-source-control [-n]` 选项。

## <a name="register-extensions"></a>注册扩展

在版本 2.x 的 Azure Functions 运行时中，必须显式注册在函数应用中使用的绑定扩展（绑定类型）。

[!INCLUDE [Register extensions](../../includes/functions-core-tools-install-extension.md)]

有关详细信息，请参阅 [Azure Functions 触发器和绑定概念](functions-triggers-bindings.md#register-binding-extensions)。

## <a name="local-settings-file"></a>本地设置文件

文件 local.settings.json 存储 Azure Functions Core Tools 的应用设置、连接字符串和设置。 其结构如下：

```json
{
  "IsEncrypted": false,   
  "Values": {
    "AzureWebJobsStorage": "<connection-string>", 
    "AzureWebJobsDashboard": "<connection-string>",
    "MyBindingConnection": "<binding-connection-string>"
  },
  "Host": {
    "LocalHttpPort": 7071, 
    "CORS": "*" 
  },
  "ConnectionStrings": {
    "SQLConnectionString": "Value"
  }
}
```

| 设置      | 说明                            |
| ------------ | -------------------------------------- |
| IsEncrypted | 设置为“true”时，使用本地计算机密钥加密所有值。 与 `func settings` 命令配合使用。 默认值为“false”。 |
| **值** | 在本地运行时使用的应用程序设置和连接字符串的集合。 这些值对应于 Azure 中你的函数应用中的应用设置，例如 **AzureWebJobsStorage** 和 **AzureWebJobsDashboard**。 许多触发器和绑定都有一个引用连接字符串应用设置的属性，例如 [Blob 存储触发器](functions-bindings-storage-blob.md#trigger---configuration)的 **Connection**。 对于此类属性，你需要一个在 **Values** 数组中定义的应用程序设置。 <br/>对于 HTTP 之外的触发器，**AzureWebJobsStorage** 是一个必需的应用设置。 当在本地安装了 [Azure 存储仿真器](../storage/common/storage-use-emulator.md)时，可以将 **AzureWebJobsStorage** 设置 `UseDevelopmentStorage=true`，核心工具使用此仿真器。 这在开发期间非常有用，但是在部署之前，应当使用实际的存储连接进行测试。 |
| **主机** | 在本地运行时，本部分中的设置会自定义 Functions 主机进程。 |
| LocalHttpPort | 设置运行本地 Functions 主机时使用的默认端口（`func host start` 和 `func run`）。 `--port` 命令行选项优先于此值。 |
| **CORS** | 定义[跨域资源共享 (CORS)](https://en.wikipedia.org/wiki/Cross-origin_resource_sharing)可以使用的来源。 以逗号分隔的列表提供来源，其中不含空格。 支持通配符值 (\*)，它允许使用任何来源的请求。 |
| ConnectionStrings | 不要将此集合用于函数绑定使用的连接字符串。 此集合仅供必须从配置文件的 **ConnectionStrings** 部分获取连接字符串的框架使用，例如[实体框架](https://msdn.microsoft.com/library/aa937723(v=vs.113).aspx)。 此对象中的连接字符串添加到提供者类型为 System.Data.SqlClient[](https://msdn.microsoft.com/library/system.data.sqlclient(v=vs.110).aspx) 的环境中。 此集合中的项不使用其他应用设置发布到 Azure 中。 必须显式将这些值添加到你的函数应用的**应用程序设置**的**连接字符串**部分中。 |

还可以在代码中将函数应用设置值读取为环境变量。 有关详细信息，请参阅以下特定于语言的参考主题的“环境变量”部分：

+ [预编译 C#](functions-dotnet-class-library.md#environment-variables)
+ [C# 脚本 (.csx)](functions-reference-csharp.md#environment-variables)
+ [F#](functions-reference-fsharp.md#environment-variables)
+ [Java](functions-reference-java.md#environment-variables) 
+ [JavaScript](functions-reference-node.md#environment-variables)

只有在本地运行时，Functions工具才使用 local.settings.json 文件中的设置。 默认情况下，将项目发布到 Azure 时，这些设置不会自动迁移。 [发布时](#publish)使用 `--publish-local-settings` 开关确保已将这些设置添加到 Azure 中的函数应用。 **ConnectionStrings** 中的值永远不会发布。

如果没有为 **AzureWebJobsStorage** 设置有效的存储连接字符串并且没有使用仿真器，则会显示以下错误消息：  

>local.settings.json 中的 AzureWebJobsStorage 缺少值。 该值对除 HTTP 以外的所有触发器都是必需的。 可运行“func azure functionapp fetch-app-settings <functionAppName>”或在 local.settings.json 中指定连接字符串。

### <a name="get-your-storage-connection-strings"></a>获取存储连接字符串

即使在使用存储仿真器进行开发时，你也可能希望使用实际的存储连接进行测试。 假设已[创建了存储帐户](../storage/common/storage-create-storage-account.md)，则可以通过下列方式之一获取有效的存储连接字符串：

+ 通过 [Azure 门户]。 导航到你的存储帐户，在“设置”中选择“访问密钥”，然后复制其中一个**连接字符串**值。

  ![从 Azure 门户复制连接字符串](./media/functions-run-local/copy-storage-connection-portal.png)

+ 使用 [Azure 存储资源管理器](http://storageexplorer.com/)连接到你的 Azure 帐户。 在“资源管理器”中，展开你的订阅，选择你的存储帐户，然后复制主或辅助连接字符串。 

  ![从存储资源管理器复制连接字符串](./media/functions-run-local/storage-explorer.png)

+ 使用核心工具通过下列命令之一从 Azure 下载连接字符串：

    + 从现有函数应用下载所有设置：

    ```bash
    func azure functionapp fetch-app-settings <FunctionAppName>
    ```
    + 获取特定存储帐户的连接字符串。

    ```bash
    func azure storage fetch-connection-string <StorageAccountName>
    ```
    
    这两个命令都要求首先登录到 Azure。

<a name="create-func"></a>
## <a name="create-a-function"></a>创建函数

若要创建函数，请运行以下命令：

```bash
func new
``` 
`func new` 支持以下可选参数：

| 参数     | 说明                            |
| ------------ | -------------------------------------- |
| **`--language -l`** | C#、F# 或 JavaScript 等模板编程语言。 |
| **`--template -t`** | 模板名称。 |
| **`--name -n`** | 函数名称。 |

例如，若要创建 JavaScript HTTP 触发器，运行：

```bash
func new --language JavaScript --template "Http Trigger" --name MyHttpTrigger
```

若要创建由队列触发的函数，运行：

```bash
func new --language JavaScript --template "Queue Trigger" --name QueueTriggerJS
```bash
<a name="start"></a>
## Run functions locally

To run a Functions project, run the Functions host. The host enables triggers for all functions in the project:

```bash
func host start
```

`func host start` 支持以下选项：

| 选项     | 说明                            |
| ------------ | -------------------------------------- |
|**`--port -p`** | 要侦听的本地端口。 默认值：7071。 |
| **`--debug <type>`** | 选项为 `VSCode` 和 `VS`。 |
| **`--cors`** | 以逗号分隔的 CORS 来源列表，其中不包含空格。 |
| **`--nodeDebugPort -n`** | 节点调试程序要使用的端口。 默认值：launch.json 中的值或 5858。 |
| **`--debugLevel -d`** | 控制台跟踪级别（关闭、详情、信息、警告或错误）。 默认：信息。|
| **`--timeout -t`** | Functions 主机启动的超时时间（以秒为单位）。 默认值：20 秒。|
| **`--useHttps`** | 绑定到 https://localhost:{port}，而不是绑定到 http://localhost:{port}。 默认情况下，此选项会在计算机上创建可信证书。|
| **`--pause-on-error`** | 退出进程前，暂停增加其他输入。 十分适用于从集成开发环境 (IDE) 启动 Azure Functions Core Tools 的情况。|

Functions 主机启动时，会输出 HTTP 触发的函数的 URL：

```bash
Found the following functions:
Host.Functions.MyHttpTrigger

Job host started
Http Function MyHttpTrigger: http://localhost:7071/api/MyHttpTrigger
```

### <a name="vs-debug"></a>在 VS Code 或 Visual Studio 中进行调试

若要附加调试程序，请传递 `--debug` 参数。 若要调试 JavaScript 函数，请使用 Visual Studio Code。 对于 C# 函数，请使用 Visual Studio。

若要调试 C# 函数，请使用 `--debug vs`。 还可使用 [Azure Functions Visual Studio 2017 Tools](https://blogs.msdn.microsoft.com/webdev/2017/05/10/azure-function-tools-for-visual-studio-2017/)。 

若要启动主机并设置 JavaScript 调试，运行：

```bash
func host start --debug vscode
```

> [!IMPORTANT]
> 对于调试，仅支持 Node.js 8.x。 不支持 Node.js 9.x。 

然后，在 Visual Studio Code 中的“调试”视图中，选择“附加到 Azure Functions”。 可附加断点、检查变量和逐步执行代码。

![使用 Visual Studio Code 调试 JavaScript](./media/functions-run-local/vscode-javascript-debugging.png)

### <a name="passing-test-data-to-a-function"></a>将测试数据传递给函数

若要在本地测试函数，请[启动 Functions 主机](#start)，并在本地服务器上使用 HTTP 请求调用终结点。 你调用的终结点要取决于函数的类型。 

>[!NOTE]  
> 本主题中的示例使用 cURL 工具从终端或命令提示符发送 HTTP 请求。 你可以使用所选的工具将 HTTP 请求发送到本地服务器。 默认情况下，在基于 Linux 的系统上提供 cURL 工具。 在 Windows 上，必须先下载并安装 [cURL 工具](https://curl.haxx.se/)。

有关测试函数的更多常规信息，请参阅[在 Azure Functions 中测试代码的策略](functions-test-a-function.md)。

#### <a name="http-and-webhook-triggered-functions"></a>HTTP 和 webhook 触发的函数

调用以下终结点，以在本地运行 HTTP 和 webhook 触发的函数：

    http://localhost:{port}/api/{function_name}

请确保使用相同的服务器名称和 Functions 主机正在侦听的端口。 在启动 Function 主机时所生成的输出中可以看到该信息。 可以使用触发器所支持的任何 HTTP 方法来调用此 URL。 

以下 cURL 命令使用查询字符串中传递的 name 参数从 GET 请求触发 `MyHttpTrigger` quickstart 函数。 

```bash
curl --get http://localhost:7071/api/MyHttpTrigger?name=Azure%20Rocks
```
下面的示例是在请求主体中传递 name 的 POST 请求中调用的相同函数：

```bash
curl --request POST http://localhost:7071/api/MyHttpTrigger --data '{"name":"Azure Rocks"}'
```

可以从在查询字符串中传递数据的浏览器发出 GET 请求。 对于所有其他 HTTP 方法，必须使用 cURL、Fiddler、Postman 或类似的 HTTP 测试工具。  

#### <a name="non-http-triggered-functions"></a>非 HTTP 触发的函数
对于 HTTP 触发器和 webhook 以外的所有类型函数，你可以通过调用管理终结点在本地测试函数。 在本地服务器上通过 HTTP POST 请求调用此终结点会触发该函数。 可以选择通过 POST 请求正文将测试数据传递给执行。 此功能类似于 Azure 门户中的“测试”选项卡。  

可以调用以下管理员终结点以触发非 HTTP 函数：

    http://localhost:{port}/admin/functions/{function_name}

若要将测试数据传递给函数的管理员终结点，必须在 POST 请求消息的正文中提供数据。 消息正文需要具有以下 JSON 格式：

```JSON
{
    "input": "<trigger_input>"
}
```` 
`<trigger_input>` 值包含函数所需格式的数据。 下面的 cURL 示例是指向 `QueueTriggerJS` 函数的 POST。 在这种情况下，输入是一个字符串，等同于期望在队列中找到的消息。      

```bash
curl --request POST -H "Content-Type:application/json" --data '{"input":"sample queue data"}' http://localhost:7071/admin/functions/QueueTriggerJS
```

#### <a name="using-the-func-run-command-in-version-1x"></a>在版本 1.x 中使用 `func run` 命令

>[!IMPORTANT]  
> 该工具的 2.x 版本不支持 `func run` 命令。 有关详细信息，请参阅主题[如何指向 Azure Functions 运行时版本](set-runtime-version.md)。

也可以使用 `func run <FunctionName>` 直接调用函数并为函数提供输入数据。 此命令类似于在 Azure 门户中使用“测试”选项卡运行函数。 

`func run` 支持以下选项：

| 选项     | 说明                            |
| ------------ | -------------------------------------- |
| **`--content -c`** | 内联内容。 |
| **`--debug -d`** | 运行函数前，将调试程序附加到主机进程。|
| **`--timeout -t`** | 本地 Functions 主机准备就绪前的等待时间（以秒为单位）。|
| **`--file -f`** | 要用作内容的文件名。|
| **`--no-interactive`** | 不提示输入。 适用于自动化方案。|

例如，若要调用 HTTP 触发的函数并传递内容正文，请运行以下命令：

```bash
func run MyHttpTrigger -c '{\"name\": \"Azure\"}'
```

### <a name="viewing-log-files-locally"></a>在本地查看日志文件

[!INCLUDE [functions-local-logs-location](../../includes/functions-local-logs-location.md)]

## <a name="publish"></a>发布到 Azure

若要将 Functions 项目发布到 Azure 中的函数应用，使用 `publish` 命令：

```bash
func azure functionapp publish <FunctionAppName>
```

可以使用以下选项：

| 选项     | 说明                            |
| ------------ | -------------------------------------- |
| **`--publish-local-settings -i`** |  将 local.settings.json 中的设置发布到 Azure，如果该设置已存在，则提示进行覆盖。 如果在使用存储仿真器，则将应用设置更改为[实际的存储连接](#get-your-storage-connection-strings)。 |
| **`--overwrite-settings -y`** | 必须与 `-i` 一起使用。 如果不同，则使用本地值覆盖 Azure 中的 AppSettings。 默认为提示。|

此命令发布到 Azure 中的现有函数应用。 如果订阅中不存在 `<FunctionAppName>`，会发生错误。 若要了解如何使用 Azure CLI 从命令提示符或终端窗口创建函数应用，请参阅[为无服务器执行创建函数应用](./scripts/functions-cli-create-serverless.md)。

`publish` 命令上传 Functions 项目目录的内容。 如果在本地删除文件，`publish` 命令不会将文件从 Azure 中删除。 可以使用 [Azure 门户]中的 [Kudu 工具](functions-how-to-use-azure-function-app-settings.md#kudu)删除 Azure 中的文件。  

>[!IMPORTANT]  
> 在 Azure 中创建函数应用时，该应用默认使用 1.x 版函数运行时。 若要让函数应用使用 2.x 版运行时，请添加应用程序设置 `FUNCTIONS_EXTENSION_VERSION=beta`。  
使用以下 Azure CLI 代码将此设置添加到函数应用： 
```azurecli-interactive
az functionapp config appsettings set --name <function_app> \
--resource-group myResourceGroup \
--settings FUNCTIONS_EXTENSION_VERSION=beta   
```

## <a name="next-steps"></a>后续步骤

Azure Functions Core Tools 是[开源工具且托管在 GitHub 上](https://github.com/azure/azure-functions-cli)。  
若要提交 bug 或功能请求，[请打开 GitHub 问题](https://github.com/azure/azure-functions-cli/issues)。 

<!-- LINKS -->

[Azure Functions Core Tools]: https://www.npmjs.com/package/azure-functions-core-tools
[Azure 门户]: https://portal.azure.com 
[Node.js]: https://docs.npmjs.com/getting-started/installing-node#osx-or-windows
