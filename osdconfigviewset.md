# _**OsdConfigViewSet：管理OsdMap中的flags.**_

常用的flags包括pause\(unpause\)、noIn\(noOut\)、noUp\(noDown\)

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

------------------

