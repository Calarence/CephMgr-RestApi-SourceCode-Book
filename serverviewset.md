ServerViewSet包括两个方法：retrieve\(request,fqdn\)：根据fqdn获取指定的server；list\(request\):获取server列表。

代码如下：

`def retrieve(self, request, fqdn):`

`return Response(`

`self.serializer_class(`

`DataObject(self.client.server_get(fqdn))).data`

`)`

代码调用流程图如下：

![](/assets/getServer.png)

通过上图可以发现，这个过程比较简单，依然是从ceph\_state取数据。

---

list代码如下

`def list(self, request):`

`        servers = self.client.server_list()`

`        return Response(self.serializer_class(`

`            [DataObject(s) for s in servers],`

`            many=True).data)`

代码调用过程如下图所示：

![](/assets/getServers.png)

关于list get\_server方法，代码中有这样的注释Like``` ``get_server``, but instead of returning information about just one node, return all the nodes in an array```

retrieve和list方法中都用到了DataObject对象，它的作用是 `A convenience for converting dicts from the backend into`

`    objects, because django_rest_framework expects objects`

