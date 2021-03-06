---
title: 用于在 Azure Log Analytics 中创建和编辑日志查询的门户 | Microsoft Docs
description: 本文介绍可用于在 Azure Log Analytics 中创建和编辑日志搜索的门户。
services: log-analytics
documentationcenter: ''
author: bwren
manager: carmonm
editor: ''
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 06/11/2018
ms.author: magoedte; bwren
ms.component: na
ms.openlocfilehash: e2ea0bf1fb3f1c63f4e6f037e465e8fdfd9a4374
ms.sourcegitcommit: 5892c4e1fe65282929230abadf617c0be8953fd9
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/29/2018
ms.locfileid: "37133251"
---
# <a name="portals-for-creating-and-editing-log-queries-in-azure-log-analytics"></a>用于在 Azure Log Analytics 中创建和编辑日志查询的门户

在 Log Analytics 中多处使用日志搜索来从工作区检索数据。  除交互处理返回数据外，实际创建和编辑查询有如下所示两种方法。  

## <a name="log-search"></a>日志搜索 
日志搜索页面可从 Azure 门户进行访问。  它适合创建可通过单行创建的基本查询。  可在不启动外部门户的情况下使用日志搜索，并可将其用于执行日志搜索的多种函数，例如创建警报规则、创建计算机组和导出查询结果。  

日志搜索提供的多种功能可在无需完全掌握查询语言的情况下编辑查询。  有关这些功能概要，请参阅[在 Azure Log Analytics 中使用日志搜索创建日志搜索](log-analytics-log-search-log-search-portal.md)。


![日志搜索页面](media/log-analytics-log-search-portals/log-search-portal.png)

## <a name="advanced-analytics-portal"></a>高级分析门户
高级分析门户是一个专用门户，提供从 Azure 门户访问的日志搜索中不可用的高级功能。  这些功能包括在多行上编辑查询、选择性地执行代码、上下文相关 Intellisense 和智能分析。  高级分析门户最适合设计保存为日志搜索或复制粘贴到其他 Log Analytics 元素的复杂查询。  通过日志搜索页面上的链接可启动高级分析门户。

![高级分析门户](media/log-analytics-log-search-portals/advanced-analytics-portal.png)


这些高级功能使得高级分析门户通常作为创建和编辑查询的主要工具。  确定查询按预期方式运行后，可将其粘贴复制到日志搜索页面或视图设计器等其他地方。  

### <a name="firewall-requirements"></a>防火墙要求
浏览器需要访问以下地址才能访问高级分析门户。  如果浏览器通过防火墙访问 Azure 门户，则必须允许访问这些地址。

| Uri | IP | 端口 |
|:---|:---|:---|
| portal.loganalytics.io | 动态 | 80,443 |
| api.loganalytics.io    | 动态 | 80,443 |
| docs.loganalytics.io   | 动态 | 80,443 |


## <a name="next-steps"></a>后续步骤

- 完成有关使用[日志搜索](log-analytics-tutorial-viewdata.md)的教程，了解如何使用查询语言创建查询
- 试用[高级分析门户](https://go.microsoft.com/fwlink/?linkid=856587)，创建复杂查询并将其用作日志搜索的开发环境。

