﻿## 操作场景

[扩容云硬盘](https://intl.cloud.tencent.com/document/product/362/5747) 完成后，需要将扩容部分的容量划分至已有分区内，或者将扩容部分的容量格式化成一个独立的新分区。

- 若您在云硬盘连接在云服务器上并且该云服务为正常运行状态时执行了硬盘扩容操作，需要先执行【重新扫描磁盘】操作来识别扩容后的硬盘空间。
- 若您在硬盘待挂载状态/硬盘挂载但服务器已经关机执行了扩容操作，扩容后的硬盘空间将自动识别。

## 前提条件
>- 扩容文件系统操作不慎可能影响已有数据，因此强烈建议您在操作前手动 [创建快照](https://intl.cloud.tencent.com/document/product/362/5755) 备份数据。
>- 扩容文件系统需要 重启实例 或重新扫描磁盘，将导致一定时间的业务中断，建议您选择合适的时间谨慎操作。
>
>- 已 [扩容云硬盘](https://intl.cloud.tencent.com/document/product/362/5747)  空间。
- 该云硬盘已 [挂载](https://intl.cloud.tencent.com/document/product/362/5745) 到 Windows 云服务器且已创建文件系统。
- 已 登录 待扩展分区及文件系统的 Windows 云服务器。

## 操作步骤
>- 如果 [扩容云硬盘](https://intl.cloud.tencent.com/document/product/362/5747) 时，挂载该盘的云服务器正处于正常运行状态，则需要 [重新扫描磁盘](#Scaning) 待识别扩容后的云硬盘空间后再 [扩展卷](#Extending)。
>- 如果 [扩容云硬盘](https://intl.cloud.tencent.com/document/product/362/5747) 时，该盘处于待挂载状态或者挂载该盘的云服务器正处于关机状态，直接 [扩展卷](#Extending) 即可。
>- 本文将以 Windows Server 2012 操作系统为例，不同操作系统的扩容操作可能不同，本文仅供参考。

<span id="Scaning"></span>
### （可选）重新扫描磁盘

1. 打开【计算机管理】。
2. 在左侧导航栏中，选择【存储】>【磁盘管理】。
3. 右键单击 【磁盘管理】，选择 【重新扫描磁盘】。如下图所示：
![](https://main.qcloudimg.com/raw/4dcdd9f42a942cba2352c730090ba049.png)
4. 扫描完成后，查看数据盘是否已经变为扩容后的大小（本例中执行扫描操作后识别到硬盘由原来的10GB扩容到了20GB）。如下图所示：
![](https://main.qcloudimg.com/raw/6cbf3575b9ee5fd1a3620ddf87105789.jpg)

<span id="Extending"></span>
### 扩展卷

1. 右键单击磁盘空间的任一空白处，选择【扩展卷】。
2. 根据扩展卷向导的指引完成扩展卷操作。完成后新增的数据盘空间将会合入原有卷中。如下图所示：
![](https://main.qcloudimg.com/raw/a561eba48c0fb8e903981f2ea82ae6be.png)

## 相关操作
[扩展分区及文件系统（Linux）](https://intl.cloud.tencent.com/document/product/362/6734)