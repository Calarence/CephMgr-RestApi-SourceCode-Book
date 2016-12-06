# _**背景：**_

ceph现有监控都是通过Ceph-mon实现，ceph-mon百分之八十的请求都是来自监控，这在很大程度上影响了monitor本身的决策、管理能力。为了改善这个情况，RedHat决定新增ceph-mgr模块，来负责ceph监控和运维。新增加的ceph-mgr与monitor处于同样的地位，都是ceph的daemon。ceph-mgr对下监控和管理ceph集群，对上提供rest api，供其程序调用。本文所研究的就是ceph-mgr rest api源码。

# 现状：

ceph-mgr于11.0版本合并到主干，现有api 22个\(完全从calamari移植\)，只有监控和少量运维功能，所涵盖的对象包括OsdMap、config、MonMap、FsMap、PgSummary、Health、MonStatus;与openstack结合时，所用到的rbd api则需要自己开发，ceph-mgr rest api的测试脚本将移植Calamari的，现在还未合并到主干;ceph-mgr daemon的测试脚本已经进入主干；ceph-mgr现在还没有权限认证以及用户角色管理。

## 监控管理平台\(图形界面\)：

ceph-mgr主要作者推荐的是[Tendrl](https://github.com/Tendrl)，Tendrl愿景是为所有的存储系统提供监控和运维功能，现在也是RedHat工程师负责维护。现阶段在github上可以看到其基本架构和设计文档，几乎每天都在更新；[tendrl\_frontend](https://github.com/Tendrl/tendrl_frontend)为Tendrl的图形界面，通过rest api与Tendrl api server通信。

## ceph测试平台：

ceph测试平台Teuthology: Teuthology是使用Python编写的自动化测试工具，适用于分布式系统测试。Teuthology分为两种角色，调度者和执行者，调度者通过配置文件的形式确定测试案例和执行者，然后将任务推送到执行者；执行者运行测试脚本，将测试结果返回，并进行图形化展示。



