ConfigViewSet：获取Ceph cluster 的配置信息。包括两个方法：list\(获取configuration列表\)、retrieve\(根据id获取某个configuration\)

这两个方法开始都是获得ceph\_config，然后根据对应的请求，然后相应的数据。获取ceph\_config的流程如下：



