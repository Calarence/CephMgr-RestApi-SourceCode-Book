PoolViewSet类图如下所示，重点关注前五个。

![](/assets/poolviewset.png)

---

获取Pool列表，代码如下所示：

`def list(self, request):`

`if 'defaults' in request.GET:`

`return self._defaults()`

`pools = [PoolDataObject(p) for p in self.client.list(POOL, {})]`

`return Response(PoolSerializer(pools, many=True).data)`

**To get the default values which will be used for any fields omitted from a POST, do a GET with the ?defaults argument.  The returned pool object will contain all attributes,but those without static defaults will be set to null. 这段话解释了self.\_defaults的作用。默认值取得过程如下图所示：**

![](/assets/poolrequest._defaults.png)

假设请求中不带有‘defaults’字段,来看一下`pools = [PoolDataObject(p) for p in self.client.list(POOL, {})]这行代码的执行流程。`

![](/assets/poolviewsetlist.png)

从上图可以看出，Pool依然是从OsdMap取得，而OsdMap是经过ceph\_state“中间件”从ceph集群获得。

---

根据Pool\_id获取某个Pool,代码如下所示：

`def retrieve(self, request, pool_id):`

`pool = PoolDataObject(self.client.get(POOL, int(pool_id)))`

`return Response(PoolSerializer(pool).data)`

代码调用流程如下图所示：

![](/assets/poolRetrive.png)

---

Pool 创建流程分析：在接收创建Pool请求后，先对POST过来的数据进行检查，具体包括\_check\_crush\_ruleset、    def \_check\_pg\_num\_inside\_config\_bounds、\_check\_pgp\_less\_than\_pg\_num、\_check\_name\_unique，最后交由mgrclient进行crate操作。具体过程如下图所示：

---------------------

