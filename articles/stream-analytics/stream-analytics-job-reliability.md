---
title: "使用 Azure 流分析作业避免服务中断 | Microsoft 文档"
description: "有关生成流分析作业升级复原力的指南。"
services: stream-analytics
documentationCenter: 
authors: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 02/27/2017
ms.author: jeffstok
translationtype: Human Translation
ms.sourcegitcommit: a2892343432f7dced535efb3917d915736580dfb
ms.openlocfilehash: cf8eba0f68e1e803026079f02b91f1bbaec189da
ms.lasthandoff: 03/01/2017

---

# <a name="guarantee-stream-analytics-job-reliability-during-service-updates"></a>在服务更新期间保证流分析作业可靠性

作为完全托管服务的一部分的是快速引入新服务功能和改进的能力。 因此，流分析可以每周（或更频繁地）进行服务更新部署。 无论进行多少次测试，由于引入了 bug，仍存在现有正在运行的作业可能会中断的风险。 对于运行关键流式处理作业的客户来说，需要避免这些风险。 客户可以用来降低此风险的机制是 Azure 的**[配对区域](https://docs.microsoft.com/azure/best-practices-availability-paired-regions)**模型。 

## <a name="how-do-azure-paired-regions-address-this-concern"></a>Azure 配对区域如何解决此问题？

流分析可以保证在单独的批处理中更新配对区域中的作业。 因此，在更新之间具有足够的时间间隔来识别潜在的重大 bug 并修复它们。

_除了印度中部以外_（其配对区域（即印度南部）不存在流分析），流分析的更新部署不会同时在一组配对区域中进行。 **同一组中**多个区域中的部署可能会**同时**进行。

有关配对组的列表，请参阅下表：

组 A 区域 |  | 组 B 区域
------- | ------- | -------
日本东部 | 配对到 | 日本西部
欧洲北部 |  | 欧洲西部
美国中部 |  | 美国东部&2;
东亚 |  | 东南亚
美国中北部 |  | 美国中南部
澳大利亚东部 |  | 澳大利亚东南部
美国东部 |  | 美国西部
巴西南部 |  | 美国中南部
中国北部 |  | 中国东部
德国东北部 |  | 德国中部

建议客户将相同的作业部署到这两个配对区域。 除了流分析的内部监视外，还建议客户监视作业，就好像**这两个作业**是生产作业一样。 如果中断确定为流分析服务更新的结果，请相应地升级并将任何下游使用者故障转移到正常运行的作业输出。 升级到支持部门可防止配对区域受新部署的影响并维护配对作业的完整性。
