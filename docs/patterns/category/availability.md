---
title: 可用性模式
titleSuffix: Cloud Design Patterns
description: 可用性定义系统正常工作的时间所占的比例。 它会受系统错误、基础结构问题、恶意攻击和系统负载的影响。 通常通过运行时间百分比衡量。 云应用程序通常向用户提供服务级别协议 (SLA)，这意味着必须以最大程度确保可用性的方式设计和实现应用程序。
keywords: 设计模式
author: dragon119
ms.date: 06/23/2017
ms.custom: seodec18
ms.openlocfilehash: d256ddd39ca3e8a452162b7b75d67f26f7bb22c2
ms.sourcegitcommit: 680c9cef945dff6fee5e66b38e24f07804510fa9
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/04/2019
ms.locfileid: "54009808"
---
# <a name="availability-patterns"></a>可用性模式

[!INCLUDE [header](../../_includes/header.md)]

可用性定义系统正常工作的时间所占的比例。 它会受系统错误、基础结构问题、恶意攻击和系统负载的影响。 通常通过运行时间百分比衡量。 云应用程序通常向用户提供服务级别协议 (SLA)，这意味着必须以最大程度确保可用性的方式设计和实现应用程序。

|                            模式                             |                                                           摘要                                                            |
|----------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------|
| [运行状况终结点监视](../health-endpoint-monitoring.md) | 在应用程序中实施可让外部工具通过公开终结点定期访问的功能检查。 |
|  [基于队列的负载调控](../queue-based-load-leveling.md)  | 使用队列在任务与所调用的服务之间充当缓冲，从而缓解间歇性负载过大现象。  |
|                 [限制](../throttling.md)                 |   控制应用程序实例、单个租户或整个服务对资源的消耗。    |
