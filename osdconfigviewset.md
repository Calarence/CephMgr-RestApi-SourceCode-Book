# _**OsdConfigViewSet：管理OsdMap中的flags.**_

目前ceph-mgr所支持的flags包括'pause', 'noup', 'nodown', 'noout', 'noin', 'nobackfill', 'norecover', 'noscrub', 'nodeep-scrub'

主要包括两个方法：

> * 获取flags,代码如下：
> 
> `def osd_config(self, request):
>     osd_map = self.client.get_sync_object(OsdMap, ['flags'])
>     return Response(osd_map)`
> 
> * 更新flags,代码如下：
> 
> `def update(self, request):
>     erializer = self.serializer_class(data=request.DATA)
>     if not serializer.is_valid(request.method):
>             return Response(serializer.errors, status=403)     
>       response = self.client.update(OSD_MAP, None, serializer.get_data())
>     return self._return_request(response)`

---

获取flgs代码流程如下：首先通过ceph\_state获取OsdMap，然后通过OsdMap中键值对的方式获取flags。

![](/assets/getOsdMapFlags.png)

---

更新flag的流程图如下所示：![](/assets/updateOsdMapflags1.png)

上图最后一步是进行了request.submit操作，首先看一下submit是如何定义的。

![](/assets/OsdMapModifyingRequest.submit.png)

由上图可以看出，submit调用了\_submit\(\)方法，\_submit\(\)方法在UserRequestBase类中，没有实现，只是定义；具体实现在RadosRequest类中，然后OsdMapModifyingRequest类继承了RadosRequest，完成request.submit\(\)操作。

