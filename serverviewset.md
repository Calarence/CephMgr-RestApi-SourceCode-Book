ServerViewSet包括两个方法：retrieve\(request,fqdn\)：根据fqdn获取指定的server；list\(request\):获取server列表。

代码如下：

`def retrieve(self, request, fqdn):`

`        return Response(`

`            self.serializer_class(`

`                DataObject(self.client.server_get(fqdn))).data`

`        )`

代码调用流程图如下：

![](/assets/getServer.png)

通过上图可以发现，这个过程比较简单，依然是从ceph\_state取数据。

------------

