---
title: 在 Azure 上运行 Linux VM
titleSuffix: Azure Reference Architectures
description: 在 Azure 上运行 Linux 虚拟机的最佳做法。
author: telmosampaio
ms.date: 12/13/2018
ms.custom: seodec18
ms.openlocfilehash: 2989cd812c7a3ac6c9e7b8fbf23639b2a95d0b41
ms.sourcegitcommit: 032f402482762f4e674aeebbc122ad18dfba11eb
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/14/2018
ms.locfileid: "53396430"
---
# <a name="run-a-linux-virtual-machine-on-azure"></a>在 Azure 上运行 Linux 虚拟机

除 VM 本身以外，在 Azure 中预配虚拟机 (VM) 还需要其他一些组件，包括网络和存储资源。 本文介绍在 Azure 上运行 Linux VM 的最佳做法。

![Azure 中的 Linux VM](./images/single-vm-diagram.png)

## <a name="resource-group"></a>资源组

[资源组][resource-manager-overview]是保存相关 Azure 资源的逻辑容器。 一般情况下，可根据资源的生存期及其管理者将资源分组。

将共享相同生命周期、密切相关的资源放入同一[资源组][resource-manager-overview]。 资源组可让你以组的形式部署和监视资源，并按资源组跟踪计费成本。 还可以删除作为集的资源，这适用于测试部署。 指定有意义的资源名称，以便简化特定资源的查找并了解其角色。 有关详细信息，请参阅 [Azure 资源的建议命名约定][naming-conventions]。

## <a name="virtual-machine"></a>虚拟机

可以通过发布的映像列表或上传到 Azure Blob 存储的自定义托管映像或虚拟硬盘 (VHD) 文件来预配 VM。  Azure 支持运行大量常用的 Linux 分发，包括 CentOS、Debian、Red Hat Enterprise、Ubuntu 和 FreeBSD。 有关详细信息，请参阅 [Azure 和 Linux][azure-linux]。

Azure 提供多种不同的虚拟机大小。 有关详细信息，请参阅 [Azure 中虚拟机的大小][virtual-machine-sizes]。 如果要将现有工作负荷转移到 Azure，开始时请先使用与本地服务器最匹配的 VM 大小。 然后从 CPU、内存和每秒磁盘输入/输出操作次数 (IOPS) 等方面测量实际工作负荷的性能，并根据需要调整大小。 

通常选择离内部用户或客户最近的 Azure 区域。 并非所有 VM 大小都可在所有区域中使用。 有关详细信息，请参阅[每个区域的服务][services-by-region]。 要获取特定区域中可用 VM 大小的列表，请从 Azure 命令行接口 (CLI) 运行以下命令：

```azurecli
az vm list-sizes --location <location>
```

要了解如何选择发布的 VM 映像，请参阅[查找 Linux VM 映像][select-vm-image]。

## <a name="disks"></a>磁盘

为获得最佳磁盘 I/O 性能，建议使用[高级存储][premium-storage]，它在固态硬盘 (SSD) 上存储数据。 成本取决于预配磁盘的容量。 IOPS 和吞吐量（即数据传输速率）也取决于磁盘大小，因此在预配磁盘时，请全面考虑三个因素（容量、IOPS 和吞吐量）。

我们还建议使用[托管磁盘][managed-disks]。 托管磁盘可代你处理存储，简化磁盘管理。 托管磁盘不需要存储帐户。 只需指定磁盘的大小和类型，就可以将它部署为高度可用的资源

OS 磁盘是存储在 [Azure 存储][azure-storage]中的 VHD，因此即使主机关闭，OS 磁盘也仍然存在。  对于 Linux VM，OS 磁盘是 `/dev/sda1`。 我们还建议创建一个或多个[数据磁盘][data-disk]（用于保存应用程序数据的持久性 VHD）。

刚创建的 VHD 尚未格式化， 登录到 VM 对磁盘进行格式化。 在 Linux shell 中，数据磁盘显示为 `/dev/sdc`、`/dev/sdd` 等。 可以运行 `lsblk` 以列出块设备，包括磁盘。 要使用数据磁盘，请创建一个分区和文件系统，并装载磁盘。 例如：

```bash
# Create a partition.
sudo fdisk /dev/sdc     # Enter 'n' to partition, 'w' to write the change.

# Create a file system.
sudo mkfs -t ext3 /dev/sdc1

# Mount the drive.
sudo mkdir /data1
sudo mount /dev/sdc1 /data1
```

在添加数据磁盘时，将为磁盘分配逻辑单元号 (LUN) ID。 或者，可以指定 LUN ID &mdash; 例如，若要更换磁盘并保留相同的 LUN ID，或者应用程序要查找特定 LUN ID。 但请记住，每个磁盘的 LUN ID 必须唯一。

可能会需要更改 I/O 计划程序，以便针对 SSD 的性能进行优化，因为使用高级存储帐户的 VM 的磁盘是 SSD。 常见的建议是对 SSD 使用 NOOP 计划程序，但应使用 [iostat] 等工具来监视工作负荷的磁盘 I/O 性能。

使用临时磁盘创建 VM。 此磁盘存储在主机的物理驱动器上。 它并非保存在 Azure 存储中，并且在重启期间以及发生其他 VM 生命周期事件期间可能会被删除。 只使用此磁盘存储临时数据，如页面文件或交换文件。 对于 Linux VM，临时磁盘是 `/dev/sdb1`，并在 `/mnt/resource` 或 `/mnt` 中装入。

## <a name="network"></a>网络

网络组件包括以下资源：

- 虚拟网络。 每个 VM 都会部署到可细分为多个子网的虚拟网络中。

- **网络接口 (NIC)**。 NIC 使 VM 能够与虚拟网络进行通信。 如果 VM 需要多个 NIC，请注意每种 [VM 大小][vm-size-tables]都定义了最大 NIC 数量。

- **公共 IP 地址**。 须使用公共 IP 地址才能与 VM 通信 &mdash; 例如，通过远程桌面 (RDP)。 公共 IP 地址可以是动态的或静态的。 默认是动态的。

- 如果需要不会更改的固定 IP 地址 &mdash; 例如，如果需要创建 DNS 'A' 记录或将 IP 地址添加到安全列表，请保留[静态 IP 地址][static-ip]。
- 还可以为 IP 地址创建完全限定域名 (FQDN)。 然后，可在 DNS 中注册指向 FQDN 的 [CNAME 记录][cname-record]。 有关详细信息，请参阅[在 Azure 门户中创建完全限定的域名][fqdn]。

- **网络安全组 (NSG)**。 [网络安全组][nsg]用于允许或拒绝向 VM 传送网络流量。 NSG 可与子网或单个 VM 实例相关联。

所有 NSG 都包含一组[默认规则][nsg-default-rules]，其中包括阻止所有入站 Internet 流量的规则。 无法删除默认规则，但其他规则可以覆盖它们。 要启用 Internet 流量，请创建允许特定端口的入站流量的规则 &mdash; 例如，将端口 80 用于 HTTP。 要启用 SSH，请添加允许 TCP 端口 22 的入站流量的 NSG 规则。

## <a name="operations"></a>操作

**SSH**。 在创建 Linux VM 之前，生成 2048 位 RSA 公共/专用密钥对。 创建 VM 时，使用公钥文件。 有关详细信息，请参阅[如何在 Azure 中将 SSH 与 Linux 和 Mac 配合使用][ssh-linux]。

**诊断**。 启用监视和诊断，包括基本运行状况指标、诊断基础结构日志和[启动诊断][boot-diagnostics]。 如果 VM 陷入不可启动状态，启动诊断有助于诊断启动故障。 创建用于存储日志的 Azure 存储帐户。 标准的本地冗余存储 (LRS) 帐户足以存储诊断日志。 有关详细信息，请参阅[启用监视和诊断][enable-monitoring]。

**可用性**。 VM 可能会受到[计划内维护][planned-maintenance]或[计划外停机][manage-vm-availability]的影响。 可以使用 [VM 重新启动日志][reboot-logs]来确定 VM 重新启动是否是由计划内维护导致的。 为了提高可用性，请在[可用性集](/azure/virtual-machines/linux/manage-availability#configure-multiple-virtual-machines-in-an-availability-set-for-redundancy)中部署多个 VM。 此配置提供更高的[服务级别协议 (SLA)][vm-sla]。

**备份** 为了防止数据意外丢失，请使用 [Azure 备份](/azure/backup/)服务将 VM 备份到异地冗余存储。 Azure 备份提供应用程序一致性备份。

**停止 VM**。 Azure 对“已停止”和“已解除分配”状态做了区分。 当 VM 状态为已停止时（而不是当 VM 已解除分配时）将向你收费。 在 Azure 门户中，“停止”按钮可解除分配 VM。 如果在已登录时通过 OS 关闭，VM 会停止，但不会解除分配，因此仍会产生费用。

**删除 VM**。 如果删除 VM，则不会删除 VHD。 这意味着可以安全地删除 VM，而不会丢失数据。 但是，仍将向你收取存储费用。 若要删除 VHD，请从 [Blob 存储][blob-storage]中删除相应的文件。 要防止意外删除，请使用[资源锁][resource-lock]锁定整个资源组或锁定单个资源（如 VM）。

## <a name="security-considerations"></a>安全注意事项

使用 [Azure 安全中心][security-center]可在一个中心视图中获得 Azure 资源的安全状态。 安全中心监视潜在的安全问题，并全面描述了部署的安全运行状况。 安全中心针对每个 Azure 订阅进行配置。 根据[将 Azure 订阅载入安全中心标准版][security-center-get-started]中所述启用安全数据收集。 启用数据收集后，安全中心会自动扫描该订阅下创建的所有 VM。

**修补程序管理**。 如果启用，安全中心会检查是否缺少任何安全更新和关键更新。 使用 VM 上的[组策略设置][group-policy]可启用自动系统更新。

**反恶意软件**。 如果启用，安全中心会检查是否已安装反恶意软件。 还可以使用安全中心从 Azure 门户中安装反恶意软件。

**访问控制**。 使用[基于角色的访问控制 (RBAC)][rbac] 来控制对 Azure 资源的访问。 RBAC 允许将授权角色分配给开发运营团队的成员。 例如，“读者”角色可以查看 Azure 资源，但不能创建、管理或删除这些资源。 某些权限特定于 Azure 资源类型。 例如，“虚拟机参与者”角色可以执行重启或解除分配 VM、重置管理员密码、创建新的 VM 等操作。 可能对此体系结构有用的其他[内置 RBAC 角色][rbac-roles]包括[开发测试实验室用户][rbac-devtest]和[网络参与者][rbac-network]。

> [!NOTE]
> RBAC 不限制已登录到 VM 的用户可以执行的操作。 这些权限由来宾 OS 上的帐户类型决定。

**审核日志**。 使用[审核日志][audit-logs]可查看预配操作和其他 VM 事件。

**数据加密**。 如果需要加密 OS 磁盘和数据磁盘，请使用 [Azure 磁盘加密][disk-encryption]。

## <a name="next-steps"></a>后续步骤

- 若要预配 Linux VM，请参阅[使用 Azure CLI 创建和管理 Linux VM](/azure/virtual-machines/linux/tutorial-manage-vm)
- 如需 Linux VM 上的完整 N 层体系结构，请参阅 [Azure 中包含 Apache Cassandra 的 Linux N 层应用程序](./n-tier-cassandra.md)。

<!-- links -->
[audit-logs]: https://azure.microsoft.com/blog/analyze-azure-audit-logs-in-powerbi-more/
[azure-linux]: /azure/virtual-machines/virtual-machines-linux-azure-overview
[azure-storage]: /azure/storage/storage-introduction
[blob-storage]: /azure/storage/storage-introduction
[boot-diagnostics]: https://azure.microsoft.com/blog/boot-diagnostics-for-virtual-machines-v2/
[cname-record]: https://en.wikipedia.org/wiki/CNAME_record
[data-disk]: /azure/virtual-machines/virtual-machines-linux-about-disks-vhds
[disk-encryption]: /azure/security/azure-security-disk-encryption
[enable-monitoring]: /azure/monitoring-and-diagnostics/insights-how-to-use-diagnostics
[fqdn]: /azure/virtual-machines/virtual-machines-linux-portal-create-fqdn
[iostat]: https://en.wikipedia.org/wiki/Iostat
[manage-vm-availability]: /azure/virtual-machines/virtual-machines-linux-manage-availability
[managed-disks]: /azure/storage/storage-managed-disks-overview
[naming-conventions]: ../../best-practices/naming-conventions.md
[nsg]: /azure/virtual-network/virtual-networks-nsg
[nsg-default-rules]: /azure/virtual-network/virtual-networks-nsg#default-rules
[planned-maintenance]: /azure/virtual-machines/virtual-machines-linux-planned-maintenance
[premium-storage]: /azure/virtual-machines/linux/premium-storage
[rbac]: /azure/active-directory/role-based-access-control-what-is
[rbac-roles]: /azure/active-directory/role-based-access-built-in-roles
[rbac-devtest]: /azure/active-directory/role-based-access-built-in-roles#devtest-labs-user
[rbac-network]: /azure/active-directory/role-based-access-built-in-roles#network-contributor
[reboot-logs]: https://azure.microsoft.com/blog/viewing-vm-reboot-logs/
[resource-lock]: /azure/resource-group-lock-resources
[resource-manager-overview]: /azure/azure-resource-manager/resource-group-overview
[security-center]: /azure/security-center/security-center-intro
[security-center-get-started]: /azure/security-center/security-center-get-started
[select-vm-image]: /azure/virtual-machines/virtual-machines-linux-cli-ps-findimage
[services-by-region]: https://azure.microsoft.com/regions/#services
[ssh-linux]: /azure/virtual-machines/virtual-machines-linux-mac-create-ssh-keys
[static-ip]: /azure/virtual-network/virtual-networks-reserved-public-ip
[virtual-machine-sizes]: /azure/virtual-machines/virtual-machines-linux-sizes
[visio-download]: https://archcenter.blob.core.windows.net/cdn/vm-reference-architectures.vsdx
[vm-size-tables]: /azure/virtual-machines/virtual-machines-linux-sizes
[vm-sla]: https://azure.microsoft.com/support/legal/sla/virtual-machines
