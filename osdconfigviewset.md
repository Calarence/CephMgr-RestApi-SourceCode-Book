# _**OsdConfigViewSet：管理OsdMap中的flags.**_

主要包括两个方法：

> * 获取osd\_map,代码如下：
> 
> `def osd_config(self, request):`
>     `osd_map = self.client.get_sync_object(OsdMap, ['flags'])`
>     `return Response(osd_map)`

> * 更新osd\_map,代码如下：
> 
> `def update(self, request):`
>     `erializer = self.serializer_class(data=request.DATA)`
>     `if not serializer.is_valid(request.method):`
>             return Response\(serializer.errors, status=403\)     
>       response = self.client.update\(OSD\_MAP, None, serializer.get\_data\(\)\)
>     `return self._return_request(response)`



