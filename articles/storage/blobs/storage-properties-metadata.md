---
title: 在 Azure 存储中设置和检索对象属性和元数据 | Microsoft Docs
description: 在 Azure 存储中存储对象的自定义元数据，并设置和检索系统属性。
services: storage
documentationcenter: ''
author: tamram
manager: timlt
editor: tysonn
ms.assetid: 036f9006-273e-400b-844b-3329045e9e1f
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/15/2017
ms.author: tamram
ms.openlocfilehash: a3eb598b2dabd4986c72b8814926eb0944707050
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/11/2017
ms.locfileid: "23056052"
---
# <a name="set-and-retrieve-properties-and-metadata"></a>设置和检索属性与元数据

Azure 存储中的对象支持系统属性和用户定义的元数据，除了该数据以外，它们还包含： 本文介绍如何使用[适用于 .NET 的 Azure 存储客户端库](https://www.nuget.org/packages/WindowsAzure.Storage/)管理系统属性和用户定义元数据。

* **系统属性**：系统属性存在于每个存储资源上。 其中一些属性是可以读取或设置的，而另一些属性是只读的。 事实上，有些系统属性与某些标准 HTTP 标头对应。 Azure 存储客户端库会维护这些内容。

* **用户定义的元数据**：用户定义的元数据是在给定资源上以名称/值对的形式指定的元数据。 可以使用元数据存储存储资源的其他值。 这些其他元数据值仅用于自己的目的，并不会影响资源的行为方式。

检索资源的属性和元数据值的过程分为两步。 在可以读取这些值之前，你必须通过调用 FetchAttributesAsync 方法显式提取它们。

> [!IMPORTANT]
> 除非调用 FetchAttributesAsync 方法之一，否则不会填充存储资源的属性和元数据值。
>
> 如果任何名称/值对包含非 ASCII 字符，将收到 `400 Bad Request`。 元数据名称/值对是有效的 HTTP 标头，因此必须遵循控制 HTTP 标头的所有限制。 因此，对于包含非 ASCII 字符的名称和值，建议使用 URL 编码或 Base64 编码。
>

## <a name="setting-and-retrieving-properties"></a>设置和检索属性
要检索属性值，请对 blob 或容器调用 FetchAttributesAsync 方法来填充这些属性，然后读取它们的值。

要在对象上设置属性，请指定属性值，并调用 **SetProperties** 方法。

以下代码示例创建容器，然后将它的一些属性值写入到控制台窗口。

```csharp
//Parse the connection string for the storage account.
const string ConnectionString = "DefaultEndpointsProtocol=https;AccountName=account-name;AccountKey=account-key";
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(ConnectionString);

//Create the service client object for credentialed access to the Blob service.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

// Retrieve a reference to a container.
CloudBlobContainer container = blobClient.GetContainerReference("mycontainer");

// Create the container if it does not already exist.
container.CreateIfNotExists();

// Fetch container properties and write out their values.
await container.FetchAttributesAsync();
Console.WriteLine("Properties for container {0}", container.StorageUri.PrimaryUri.ToString());
Console.WriteLine("LastModifiedUTC: {0}", container.Properties.LastModified.ToString());
Console.WriteLine("ETag: {0}", container.Properties.ETag);
Console.WriteLine();
```

## <a name="setting-and-retrieving-metadata"></a>设置和检索元数据
可以在 Blob 或容器资源上指定元数据作为一个或多个名称/值对。 要设置元数据，请将名称/值对添加到资源上的 **Metadata** 集合，然后调用 **SetMetadata** 方法以将值保存到服务。

> [!NOTE]
> 元数据的名称必须符合 C# 标识符命名约定。
>
>

以下代码示例在容器上设置元数据。 一个值是使用集合的 **Add** 方法设置的。 另一个值是使用隐式键/值语法设置的。 这两种方法都有效。

```csharp
public static async Task AddContainerMetadataAsync(CloudBlobContainer container)
{
    // Add some metadata to the container.
    container.Metadata.Add("docType", "textDocuments");
    container.Metadata["category"] = "guidance";

    // Set the container's metadata.
    await container.SetMetadataAsync();
}
```

要检索元数据，请对 blob 或容器调用 **FetchAttributes** 方法以填充 **Metadata** 集合，并读取值，如下面的示例所示。

```csharp
public static async Task ListContainerMetadataAsync(CloudBlobContainer container)
{
    // Fetch container attributes in order to populate the container's properties and metadata.
    await container.FetchAttributesAsync();

    // Enumerate the container's metadata.
    Console.WriteLine("Container metadata:");
    foreach (var metadataItem in container.Metadata)
    {
        Console.WriteLine("\tKey: {0}", metadataItem.Key);
        Console.WriteLine("\tValue: {0}", metadataItem.Value);
    }
}
```

## <a name="next-steps"></a>后续步骤
* [适用于 .NET 的 Azure 存储客户端库参考](/dotnet/api/?term=Microsoft.WindowsAzure.Storage)
* [适用于 .NET NuGet 包的 Azure 存储客户端库](https://www.nuget.org/packages/WindowsAzure.Storage/)
