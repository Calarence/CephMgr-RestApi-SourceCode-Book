这个类含有两个方法： retrieve：根据id获取指定的monitor;  list：获取monitor列表。

两方法代码如下所示：

`def retrieve(self, request, mon_id):`

             `mons = self._get_mons()
             try:
             mon = [m for m in mons if m['name'] == mon_id][0]
             except IndexError:
             raise Http404("Mon '%s' not found" % mon_id)
             return Response(self.serializer_class(DataObject(mon)).data)

`def list(self, request):`

`mons = self._get_mons()`

`return Response(`

`self.serializer_class([DataObject(m) for m in mons],`

`many=True).data)`

上面两个方法都通过\_get\_mons\(\)方法获取mon，然后将其返回。

\_get\_mons\(\)代码执行流程图如下所示：

