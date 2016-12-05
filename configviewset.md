ConfigViewSet：获取Ceph cluster 的配置信息。包括两个方法：list\(获取configuration列表\)、retrieve\(根据id获取某个configuration\)

这两个方法开始都是获得ceph\_config，然后根据对应的请求，然后相应的数据。获取ceph\_config的流程如下：![](/assets/getConfiguration.png)

在拿到ceph\_config后，list、retrieve操作分别如下：

list: `settings = [DataObject({'key': k, 'value': v}) for (k, v) in ceph_config.items()]`

这行代码作用是先遍历ceph\_config的每个对象，将其转换为DataObject，然后将所有DataObject

放到数组中，返回数组。即得到的configuration列表。

retrieve：`setting = DataObject({'key': key, 'value': ceph_config[key]}) `

上面一行代码通过key-value的形式取出指定的configuration，然后返回。



