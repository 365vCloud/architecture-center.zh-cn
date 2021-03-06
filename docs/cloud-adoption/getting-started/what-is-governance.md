---
title: 企业云的采用：什么是云资源调控？
description: 解释 Azure 中的资源访问调控的概念
author: petertaylor9999
ms.date: 09/10/2018
ms.openlocfilehash: fb01b2e2823c16e32f8ded696de0b6faf1d2e610
ms.sourcegitcommit: e7f8676bbffe500fc4d6deb603b7c0b7ba1884a6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/10/2018
ms.locfileid: "53179274"
---
# <a name="enterprise-cloud-adoption-what-is-cloud-resource-governance"></a>企业云的采用：什么是云资源调控？

在 [Azure 的工作原理](what-is-azure.md)中我们已了解到，Azure 是代表用户运行虚拟化硬件和软件的服务器与网络硬件的集合。 Azure 可让组织根据需要轻松创建、读取、更新和删除资源，使开发工作和 IT 部门变得更加轻盈。

但是，为开发人员授予不受限制的资源访问权限可能会使他们变得随心所欲，此外还可能导致意外的成本。 例如，某个开发团队获批部署一组用于测试的资源，但完成测试后忘记删除这些资源。 这些资源会不断加大成本，即使其用途不再受批准，或者不再有需要。 

解决此问题的方法就是采用资源访问**调控**。 调控是指根据组织的目标和要求，对 Azure 资源的使用持续进行管理、监视和审核的过程。 

> [!VIDEO https://www.microsoft.com/en-us/videoplayer/embed/RE2ii94] 

每家组织的目标和要求都是独特的，因此，不存在以一应百的调控方法。 Azure 实施两个主要的管理工具：**基于角色的访问控制 (RBAC)** 和**资源策略**，每家组织可以使用这些工具设计自己的调控模型。

RBAC 定义角色，而角色定义获得该角色的用户的功能。 例如，**所有者**角色可以资源的所有功能（创建、读取、更新和删除），**读取者**角色只能启用读取功能。 可以使用应用到许多资源类型的宽泛范围定义角色，也可以使用应用到少量资源类型的狭窄范围定义角色。 

资源策略定义有关创建资源的规则。 例如，资源策略可将 VM 的 SKU 限制为特定的预批准大小。 或者，在发出创建资源的请求时，资源策略可以强制添加包含成本中心的标记。 

配置这些工具时，一个重要的考虑因素是在调控与组织灵活性之间实现平衡。 也就是说，调控策略的限制性越强，开发人员和 IT 工作人员的灵活性就越低。 这是因为，限制性的调控策略可能需要更多的手动步骤，例如，要求开发人员填写表单，或者将电子邮件发送到管理团队中的某人，以手动创建资源。 调控团队的功能有限，可能会积压工作，导致工作效率不高的开发团队等待创建其资源，并且在等待删除不需要的资源过程中，这些资源持续产生成本。

## <a name="next-steps"></a>后续步骤

了解云资源治理的概念后，接下来请详细了解在准备学习如何设计[单个团队](../governance/governance-single-team.md)或[多个团队](../governance/governance-multiple-teams.md)的治理模型之前，[如何管理资源访问](azure-resource-access.md)。

> [!div class="nextstepaction"]
> [了解 Azure 中的资源访问](azure-resource-access.md)
