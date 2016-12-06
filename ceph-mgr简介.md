# _**背景：**_

ceph现有监控都是通过Ceph-mon实现，ceph-mon百分之八十的请求都是来自监控，这在很大程度上影响了monitor本身的决策、管理能力。为了改善这个情况，RedHat决定新增ceph-mgr模块，来负责ceph监控和运维。新增加的ceph-mgr与monitor处于同样的地位，都是ceph的daemon。ceph-mgr对下监控和管理ceph集群，对上提供rest api，供其程序调用。本文所研究的就是ceph-mgr rest api源码。

