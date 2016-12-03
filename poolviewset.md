PoolViewSet类图如下所示，重点关注前五个。

![](/assets/poolviewset.png)

---

`def list(self, request):`

`if 'defaults' in request.GET:`

`return self._defaults()`

`pools = [PoolDataObject(p) for p in self.client.list(POOL, {})]`

`return Response(PoolSerializer(pools, many=True).data)`

**To get the default values which will be used for any fields omitted from a POST, do a GET with the ?defaults argument.  The returned pool object will contain all attributes,but those without static defaults will be set to null. 这段话解释了self.\_defaults的作用。**



假设请求中不带有‘defaults’字段,来看一下`pools = [PoolDataObject(p) for p in self.client.list(POOL, {})]这行代码的执行流程。`

![](/assets/poolviewsetlist.png)

从上图可以看出，Pool依然是从OsdMap取得，而OsdMap是经过ceph\_state“中间件”从ceph集群获得。

