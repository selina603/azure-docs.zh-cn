---
title: Linux 上的 Azure 应用服务常见问题解答 | Microsoft Docs
description: Linux 上的 Azure 应用服务常见问题解答。
keywords: Azure 应用服务, Web 应用, 常见问题解答, Linux, oss
services: app-service
documentationCenter: ''
author: ahmedelnably
manager: cfowler
editor: ''
ms.assetid: ''
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/18/2018
ms.author: msangapu
ms.openlocfilehash: 5b3b3d3946b56ff53ad74c2ab93a646baa787d05
ms.sourcegitcommit: 16ddc345abd6e10a7a3714f12780958f60d339b6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36222971"
---
# <a name="azure-app-service-on-linux-faq"></a>Linux 上的 Azure 应用服务常见问题解答

随着 Linux 应用服务的发布，我们正在努力添加功能和改进我们的平台。 本文提供客户最近提出的问题的解答。

如果你有问题，请对本文发表评论。

## <a name="built-in-images"></a>内置映像

**我想对平台提供的内置 Docker 容器进行分叉。在哪里可以找到这些文件？**

可以在 [GitHub](https://github.com/azure-app-service) 上找到所有 Docker 文件。 可以在 [Docker Hub](https://hub.docker.com/u/appsvc/) 上找到所有 Docker 容器。

**配置运行时堆栈时，“启动文件”部分的所需值是什么？**

对于 Node.js，指定 PM2 配置文件或脚本文件。 对于 .NET Core，以 `dotnet <myapp>.dll` 的形式指定已编译的 DLL 名称。 对于 Ruby，可以指定要用于初始化应用的 Ruby 脚本。

## <a name="management"></a>管理

**在 Azure 门户中按下“重启”按钮时，会发生什么情况？**

此操作等同于 Docker 重启。

**可以使用安全外壳 (SSH) 连接到应用容器虚拟机 (VM) 吗？**

是的，可以通过源代码管理 (SCM) 站点实现此操作。

> [!NOTE]
> 还可以使用 SSH、SFTP 或 Visual Studio Code（用于实时调试 Node.js 应用）直接从本地开发计算机连接到应用容器。 有关详细信息，请参阅[远程调试和通过 SSH 登录到 Linux 上的应用服务](https://aka.ms/linux-debug)。
>

**如何通过 SDK 或 Azure 资源管理器模板创建 Linux 应用服务计划？**

应将应用服务的“保留”字段设置为 *true*。

## <a name="continuous-integration-and-deployment"></a>持续集成和部署

**更新 Docker Hub 上的映像后，我的 Web 应用仍使用旧的 Docker 容器映像。是否支持自定义容器的持续集成和部署？**

支持，若要设置 Azure 容器注册表或 DockerHub 的持续集成/部署，请查阅以下文章：[使用用于容器的 Web 应用进行持续部署](./app-service-linux-ci-cd.md)。 对于专用注册表，可以通过先停止然后启动 Web 应用来刷新容器。 或者，可以更改或添加虚拟应用程序设置，从而强制刷新容器。

**是否支持过渡环境？**

是的。

**是否可以使用 *Web 部署*来部署 Web 应用？**

可以，需要将名为 `WEBSITE_WEBDEPLOY_USE_SCM` 的应用设置设置为 *false*。

**使用 Linux Web 应用时，应用程序的 Git 部署失败。如何解决此问题？**

如果 Linux Web 应用的 Git 部署失败，可选择以下选项之一部署应用程序代码：

- 使用持续交付（预览版）功能：可将应用的源代码存储在 Team Services Git 存储库或 GitHub 存储库中，以使用 Azure 持续交付。 有关详细信息，请参阅[如何为 Linux Web 应用配置持续交付](https://blogs.msdn.microsoft.com/devops/2017/05/10/use-azure-portal-to-setup-continuous-delivery-for-web-app-on-linux/)。

- 使用 [ZIP 部署 API](https://github.com/projectkudu/kudu/wiki/Deploying-from-a-zip-file)：若要使用此 API，请[通过 SSH 连接到 Web 应用](https://docs.microsoft.com/azure/app-service/containers/app-service-linux-ssh-support#making-a-client-connection)，并转到要在其中部署代码的文件夹。 运行以下代码：

   ```bash
   curl -X POST -u <user> --data-binary @<zipfile> https://{your-sitename}.scm.azurewebsites.net/api/zipdeploy
   ```

   如果有错误指出找不到 `curl` 命令，请确保在运行前一条 `curl` 命令之前使用 `apt-get install curl` 安装 curl。

## <a name="language-support"></a>语言支持

**我想要在 Node.js 应用程序中使用 Web 套接字，要设置什么特殊设置或配置吗？**

需要，请在服务器端 Node.js 代码中禁用 `perMessageDeflate`。 例如，如果要使用 socket.io，请使用以下代码：

```nodejs
var io = require('socket.io')(server,{
  perMessageDeflate :false
});
```

**是否支持未编译的 .NET Core 应用？**

是的。

**是否支持将 Composer 用作 PHP 应用的依赖关系管理器？**

支持，在 Git 部署过程中，Kudu 应检测到正在部署 PHP 应用程序（这得益于 composer.lock 文件的存在），然后触发 composer 安装。

## <a name="custom-containers"></a>自定义容器

**我使用的是我自己的自定义容器。我希望平台将 SMB 共享装载到 `/home/` 目录。**

可以通过将 `WEBSITES_ENABLE_APP_SERVICE_STORAGE` 应用设置设为 *true* 来实现此目的。 请记住，此操作将导致容器在平台存储发生变动时重新启动。

>[!NOTE]
>如果 `WEBSITES_ENABLE_APP_SERVICE_STORAGE` 设置未指定或设为 *false*，则 `/home/` 目录将不跨规模实例共享，且重启后其中写入的文件不会保留。

**自定义容器需要很长时间才能启动，并且平台在它完成启动之前便重启了容器。**

可以配置该平台在重启容器之前的等待时间。 为此，可将 `WEBSITES_CONTAINER_START_TIME_LIMIT` 应用设置设为所需的值。 默认值为 230 秒，最大值为 1800 秒。

**专用注册表服务器 URL 的格式是什么？**

提供完整注册表 URL，包括 `http://` 或 `https://`。

**专用注册表选项中的映像名称的格式是什么？**

添加完整映像名称，包括专用注册表 URL（例如 myacr.azurecr.io/dotnet:latest）。 使用自定义端口的映像名称[无法通过门户输入](https://feedback.azure.com/forums/169385-web-apps/suggestions/31304650)。 若要设置 `docker-custom-image-name`，请使用 [`az` 命令行工具](https://docs.microsoft.com/cli/azure/webapp/config/container?view=azure-cli-latest#az_webapp_config_container_set)。

**是否可以在自定义容器映像上公开多个端口？**

目前不支持公开多个端口。

**可以自带存储吗？**

目前不支持自带存储。

**为何无法从 SCM 站点浏览自定义容器的文件系统或正在运行的进程？**

SCM 站点在单独的容器中运行。 用户无法查看应用容器的文件系统或正在运行的进程。

**我的自定义容器侦听除端口 80 以外的端口。如何配置我的应用将请求路由到该端口？**

我们提供自动端口检测。 也可以指定名为 *WEBSITES_PORT* 的应用设置，并为其提供所需的端口号值。 以前，平台使用 *PORT* 应用设置。 我们计划弃用此应用设置，改为独占使用 *WEBSITES_PORT*。

**是否需要在自定义容器中实现 HTTPS？**

不需要，平台会处理共享前端上的 HTTPS 终止。

## <a name="pricing-and-sla"></a>定价和 SLA

**服务正式版的定价是多少？**

根据 Azure 应用服务常规定价，按照应用运行小时数计费。

## <a name="other-questions"></a>其他问题

**应用程序设置名称中支持的字符有哪些？**

应用程序设置只能使用字母（A-Z、a-z）、数字 (0-9) 和下划线字符 (_)。

**可在何处请求新功能？**

可以在 [Web 应用反馈论坛](https://aka.ms/webapps-uservoice)提交看法。 请将“[Linux]”添加到建议的标题中。

## <a name="next-steps"></a>后续步骤

- [什么是 Linux 上的 Azure 应用服务？](app-service-linux-intro.md)
- [设置 Azure 应用服务中的过渡环境](../../app-service/web-sites-staged-publishing.md?toc=%2fazure%2fapp-service%2fcontainers%2ftoc.json)
- [使用用于容器的 Web 应用进行持续部署](./app-service-linux-ci-cd.md)
