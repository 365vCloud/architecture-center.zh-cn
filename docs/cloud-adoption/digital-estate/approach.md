---
title: 数字资产规划方法
titleSuffix: Enterprise Cloud Adoption
description: 介绍一些数字资产规划方法
author: BrianBlanchard
ms.date: 12/10/2018
ms.openlocfilehash: 5803447ff87e733aa5a9c24ac626bba665b8394a
ms.sourcegitcommit: e7f8676bbffe500fc4d6deb603b7c0b7ba1884a6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/10/2018
ms.locfileid: "53179602"
---
# <a name="enterprise-cloud-adoption-approaches-to-digital-estate-planning"></a><span data-ttu-id="f1fdc-103">企业云采用：数字资产规划方法</span><span class="sxs-lookup"><span data-stu-id="f1fdc-103">Enterprise Cloud Adoption: Approaches to digital estate planning</span></span>

<span data-ttu-id="f1fdc-104">数字资产规划可以采用多种形式，具体取决于所需的成果和现有资产的大小。</span><span class="sxs-lookup"><span data-stu-id="f1fdc-104">Digital estate planning can take a number of shapes, depending on the desired outcomes and size of the existing estate.</span></span> <span data-ttu-id="f1fdc-105">在方法方面，也有许多选项可供使用。</span><span class="sxs-lookup"><span data-stu-id="f1fdc-105">There are also a number of options regarding the approach taken.</span></span> <span data-ttu-id="f1fdc-106">必须在规划周期提前规定有关方法的期望。</span><span class="sxs-lookup"><span data-stu-id="f1fdc-106">It's important to set expectations regarding the approach early in planning cycles.</span></span> <span data-ttu-id="f1fdc-107">如果期望不明确，在执行额外的库存收集活动时往往会导致延迟。</span><span class="sxs-lookup"><span data-stu-id="f1fdc-107">Unclear expectations often lead to delays associated with additional inventory gathering exercises.</span></span> <span data-ttu-id="f1fdc-108">本文概述三种分析方法。</span><span class="sxs-lookup"><span data-stu-id="f1fdc-108">This article outlines three approaches to analysis.</span></span>

## <a name="workload-driven-approach"></a><span data-ttu-id="f1fdc-109">工作负荷驱动的方法</span><span class="sxs-lookup"><span data-stu-id="f1fdc-109">Workload-driven approach</span></span>

<span data-ttu-id="f1fdc-110">自上而下的评估方法会评估安全方面，例如数据分类（高、中、低业务影响）、合规性、主权和安全风险要求。</span><span class="sxs-lookup"><span data-stu-id="f1fdc-110">The top-down assessment approach evaluates the security aspects, such as the categorization of data (high, medium, or low business impact), compliance, sovereignty, and security risk requirements.</span></span> <span data-ttu-id="f1fdc-111">然后，此方法会评估高层面的体系结构复杂性，并评估身份验证、数据结构、延迟要求、依赖关系和应用程序寿命预期等方面。</span><span class="sxs-lookup"><span data-stu-id="f1fdc-111">This approach then assesses high-level architectural complexity, evaluating aspects such as authentication, data structure, latency requirements, dependencies, and application life expectancy.</span></span> <span data-ttu-id="f1fdc-112">接下来，自上而下的方法将衡量应用程序的运行要求，例如服务级别、集成、维护时段、监视和见解。</span><span class="sxs-lookup"><span data-stu-id="f1fdc-112">Next, the top-down approach measures the operational requirements of the application, such as service levels, integration, maintenance windows, monitoring, and insight.</span></span> <span data-ttu-id="f1fdc-113">分析并考虑到所有这些方面后，结果是一个评分，它反映了将此应用程序迁移到以下每种云平台的相对难度：IaaS、PaaS 和 SaaS。</span><span class="sxs-lookup"><span data-stu-id="f1fdc-113">When all of these aspects have been analyzed and taken into consideration, the result is a score that reflects the relative difficulty to migrate this application to each of the cloud platforms: IaaS, PaaS, and SaaS.</span></span>

<span data-ttu-id="f1fdc-114">其次，自上而下的评估方法会评估应用程序的财务收益，例如运营效率、TCO、投资回报，或其他任何相应的财务指标。</span><span class="sxs-lookup"><span data-stu-id="f1fdc-114">Second, the top-down assessment evaluates the financial benefits of the application, such as operational efficiencies, TCO, return on investment, or any other appropriate financial metrics.</span></span> <span data-ttu-id="f1fdc-115">此外，该评估还会检查应用程序的季节性（在年度的某些时间是否会出现需求高峰）和总体计算负载。</span><span class="sxs-lookup"><span data-stu-id="f1fdc-115">In addition, the assessment also examines the seasonality of the application (are there times of the year when demand spikes) and overall compute load.</span></span> <span data-ttu-id="f1fdc-116">此外，它还会检查该应用程序支持的用户类型（业余/专家、一直登录/偶尔登录），因而也会检查所需的可伸缩性和弹性。</span><span class="sxs-lookup"><span data-stu-id="f1fdc-116">Also, it looks at the types of users it supports (casual/expert, always/occasionally logged on), and consequently the required scalability and elasticity.</span></span> <span data-ttu-id="f1fdc-117">最后，该评估会检查应用程序可能存在的业务连续性和复原能力要求，以及在发生服务中断时运行该应用程序所需的依赖项，并依此作出结论。</span><span class="sxs-lookup"><span data-stu-id="f1fdc-117">Finally, the assessment concludes by examining business continuity and resiliency requirements that the application might have, as well as dependencies to run the application if a disruption of service should occur.</span></span>

> [!TIP]
> <span data-ttu-id="f1fdc-118">此方法需要与业务和技术利益干系人会面，并需要他们的非正式反馈。</span><span class="sxs-lookup"><span data-stu-id="f1fdc-118">This approach requires interviews and anecdotal feedback from business and technical stakeholders.</span></span> <span data-ttu-id="f1fdc-119">重要人员是否有空是能否按时完成的最大决定因素。</span><span class="sxs-lookup"><span data-stu-id="f1fdc-119">Availability of key individuals is the biggest risk to timing.</span></span> <span data-ttu-id="f1fdc-120">数据源的不稳定性使得生成准确成本或时间预测变得更加困难。</span><span class="sxs-lookup"><span data-stu-id="f1fdc-120">The anecdotal nature of the data sources makes it more difficult to produce accurate cost or timing estimates.</span></span> <span data-ttu-id="f1fdc-121">提前做好计划并验证收集到的所有数据。</span><span class="sxs-lookup"><span data-stu-id="f1fdc-121">Plan schedules in advance and validate any data collected.</span></span>

## <a name="asset-driven-approach"></a><span data-ttu-id="f1fdc-122">资产驱动的方法</span><span class="sxs-lookup"><span data-stu-id="f1fdc-122">Asset-driven approach</span></span>

<span data-ttu-id="f1fdc-123">资产驱动的方法根据支持迁移应用程序的资产提供计划。</span><span class="sxs-lookup"><span data-stu-id="f1fdc-123">The asset-driven approach provides a plan based on the assets that support an application to migrate.</span></span> <span data-ttu-id="f1fdc-124">在此方法中，将从配置管理数据库 (CMDB) 或其他基础结构评估工具提取使用情况统计数据。</span><span class="sxs-lookup"><span data-stu-id="f1fdc-124">In this approach, statistical usage data is pulled from a Configuration Management Database (CMDB) or other infrastructure assessment tools.</span></span> <span data-ttu-id="f1fdc-125">此方法通常假设将 IaaS 部署模型用作基准。</span><span class="sxs-lookup"><span data-stu-id="f1fdc-125">This approach usually assumes an IaaS model of deployment as a baseline.</span></span> <span data-ttu-id="f1fdc-126">在此过程中，分析功能将评估每个资产的属性：内存、处理器（CPU 核心）数目、操作系统存储空间、数据驱动器、网络接口卡 (NIC)、IPv6、网络负载均衡、群集、操作系统版本、数据库版本（如果需要）、支持的域、第三方组件或软件包，等等。</span><span class="sxs-lookup"><span data-stu-id="f1fdc-126">In this process, the analysis evaluates the attributes of each asset: memory, number of processors (CPU cores), operating system storage space, data drives, network interface cards (NICs), IPv6, network load balancing, clustering, version of the operating system, version of the database (if required), domains supported, and third-party components or software packages, among others.</span></span> <span data-ttu-id="f1fdc-127">然后，将此方法盘点的资产与工作负荷或应用程序保持一致，以实现分组和依赖项映射目的。</span><span class="sxs-lookup"><span data-stu-id="f1fdc-127">The assets inventoried in this approach are then aligned with workloads or applications for grouping and dependency mapping purposes.</span></span>

> [!TIP]
> <span data-ttu-id="f1fdc-128">此方法需要丰富的使用情况统计数据源。</span><span class="sxs-lookup"><span data-stu-id="f1fdc-128">This approach requires a rich source of statistical usage data.</span></span> <span data-ttu-id="f1fdc-129">扫描库存和收集数据所需的时间是能否按时完成的最大决定因素。</span><span class="sxs-lookup"><span data-stu-id="f1fdc-129">The time to scan the inventory and collect data is the biggest risk to timing.</span></span> <span data-ttu-id="f1fdc-130">低级别的数据源可能在资产或应用程序之间缺少依赖关系。</span><span class="sxs-lookup"><span data-stu-id="f1fdc-130">The low-level data sources can miss dependencies between assets or applications.</span></span> <span data-ttu-id="f1fdc-131">计划至少花费一个月时间来扫描库存。</span><span class="sxs-lookup"><span data-stu-id="f1fdc-131">Plan for at least one month to scan the inventory.</span></span> <span data-ttu-id="f1fdc-132">部署之前验证依赖关系。</span><span class="sxs-lookup"><span data-stu-id="f1fdc-132">Validate dependencies before deployment.</span></span>

## <a name="incremental-approach"></a><span data-ttu-id="f1fdc-133">增量方法</span><span class="sxs-lookup"><span data-stu-id="f1fdc-133">Incremental approach</span></span>

<span data-ttu-id="f1fdc-134">与使用企业云采用框架时一样，我们强烈建议运用增量方法。</span><span class="sxs-lookup"><span data-stu-id="f1fdc-134">Like much of the Enterprise Cloud Adoption framework, an incremental approach is highly suggested.</span></span> <span data-ttu-id="f1fdc-135">在进行数字资产规划时，此方法相当于一个多阶段过程，如下所述：</span><span class="sxs-lookup"><span data-stu-id="f1fdc-135">In the case of digital estate planning, that equates to a multi-phase process, as follows:</span></span>

- <span data-ttu-id="f1fdc-136">初始成本分析：如果需要执行财务验证，请先应用如上所述的资产驱动的方法，以获取整个数字资产的初始成本计算结果（未经过合理化）。</span><span class="sxs-lookup"><span data-stu-id="f1fdc-136">Initial cost analysis: If financial validation is required, start with an asset-driven approach, described above, to get an initial cost calculation for the entire digital estate, with no rationalization.</span></span> <span data-ttu-id="f1fdc-137">这样可以建立最坏情况的基准。</span><span class="sxs-lookup"><span data-stu-id="f1fdc-137">This establishes a worst-case scenario benchmark.</span></span>

- <span data-ttu-id="f1fdc-138">迁移规划：分配云策略团队后，使用工作负荷驱动的方法，只根据团队的集体知识和有限的利益干系人面谈，来生成初始迁移积压工作。</span><span class="sxs-lookup"><span data-stu-id="f1fdc-138">Migration planning: Once a Cloud Strategy team has been assigned, build an initial migration backlog using a workload-driven approach, based solely on their collective knowledge and limited stakeholder interviews.</span></span> <span data-ttu-id="f1fdc-139">此方法可以快速生成轻型工作负荷评估来促进协作。</span><span class="sxs-lookup"><span data-stu-id="f1fdc-139">This approach quickly builds a light-weight workload assessment to foster collaboration.</span></span>

- <span data-ttu-id="f1fdc-140">版本规划：在每个版本中，迁移积压工作将被清除并重新设置优先级，以专注于最相关的业务影响。</span><span class="sxs-lookup"><span data-stu-id="f1fdc-140">Release planning: At each release, the migration backlog is pruned and re-prioritized to focus on the most relevant business impact.</span></span> <span data-ttu-id="f1fdc-141">在此过程中，将接下来的 5&ndash;10 个工作负荷选作优先版本。</span><span class="sxs-lookup"><span data-stu-id="f1fdc-141">During this process, the next 5&ndash;10 workloads would be selected as prioritized releases.</span></span> <span data-ttu-id="f1fdc-142">此时，云策略团队会投入时间来完成穷举式工作负荷驱动的方法。</span><span class="sxs-lookup"><span data-stu-id="f1fdc-142">At this point, the Cloud Strategy team would invest the time in completing an exhaustive workload-driven approach.</span></span> <span data-ttu-id="f1fdc-143">将此项评估延迟到与版本相符为止可以更好地配合利益干系人的时间。</span><span class="sxs-lookup"><span data-stu-id="f1fdc-143">Delaying this assessment until a release is aligned, better respects the time of stakeholders.</span></span> <span data-ttu-id="f1fdc-144">它还会将全面分析的投入延迟到业务部门开始查看前期工作的结果为止。</span><span class="sxs-lookup"><span data-stu-id="f1fdc-144">It also delays the investment in full analysis until the business starts to see results from earlier efforts.</span></span>

- <span data-ttu-id="f1fdc-145">执行分析：在迁移、现代化或复制任何资产之前，应该单独评估并在统一发布过程中评估资产。</span><span class="sxs-lookup"><span data-stu-id="f1fdc-145">Execution analysis: Prior to the migration, modernization, or replication of any asset, the asset should be assessed individually and as part of a collective release.</span></span> <span data-ttu-id="f1fdc-146">此时，可以审查初始资产驱动的方法提供的数据，以确保大小和运行约束准确。</span><span class="sxs-lookup"><span data-stu-id="f1fdc-146">At this point, the data from the initial asset-driven approach can be scrutinized to ensure accurate sizing and operational constraints.</span></span>

> [!TIP]
> <span data-ttu-id="f1fdc-147">此增量方法可以简化规划，并加速取得结果。</span><span class="sxs-lookup"><span data-stu-id="f1fdc-147">This incremental approach allows for streamlined planning and accelerated results.</span></span> <span data-ttu-id="f1fdc-148">所有参与方必须知道延迟决策的方法，这一点极其重要。</span><span class="sxs-lookup"><span data-stu-id="f1fdc-148">It is very important that all parties involved understand the approach to delayed decision making.</span></span> <span data-ttu-id="f1fdc-149">同样重要的是，应该记录每个阶段做出的假设，以避免详细信息丢失。</span><span class="sxs-lookup"><span data-stu-id="f1fdc-149">It is equally important that assumptions made at each stage be documented to avoid loss of details.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f1fdc-150">后续步骤</span><span class="sxs-lookup"><span data-stu-id="f1fdc-150">Next steps</span></span>

<span data-ttu-id="f1fdc-151">选择一种方法后，可以收集库存。</span><span class="sxs-lookup"><span data-stu-id="f1fdc-151">Once an approach is selected, the inventory can be collected.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="f1fdc-152">收集库存数据</span><span class="sxs-lookup"><span data-stu-id="f1fdc-152">Gather inventory data</span></span>](inventory.md)