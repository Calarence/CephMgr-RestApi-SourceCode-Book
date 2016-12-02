# RequestViewSet

用来追踪和管理一些比较耗时的操作\(如创建Pool\)。这种类型的请求到达时，服务会立即返回202状态码和requestID，然后根据requestID可以了解该操作的进展以及完成情况。可以根据‘complete’、‘submitted’关键字对request进行过滤;也可以根据requestID取消某个操作。

---

代码调用情况如下所示：

![](/assets/userRequest.png)

由图中红框所示，RequestViewSet最终会调用RequestCollection里的代码，所以只需要关心RequestCollection即可。

`_by_request_id = {} ，`是一个map，用于存放submit的request，key为request\_id,值为对应request

`def submit(self, request):`

             ` #将request保存到_by_request_id`

`        """`

`        Submit a request and store it.  Do this in one operation`

`        to hold the lock over both operations, otherwise a response`

`        to a job could arrive before the request was filed here.`

`        """`

`        with self._lock:`

`            log.info("RequestCollection.submit: {0} {1}".format(`

`                request.id, request.headline))`

`            self._by_request_id[request.id] = request`

`            request.submit()`

`def `_**`get_by_id`**_`(self, request_id):`

               `#根据id值从map中取出对应的request`

`        return self._by_request_id[request_id]`

`def get_all(self, state=None):`

              `#根据state过滤，state值可能为completed或submitted，若无state字段，返回全部request`

`        if not state:`

`            return self._by_request_id.values()`

`        else:`

`            return [r for r in self._by_request_id.values() if r.state == state]`



def cancel\(self, request\_id\):现在这个方法被注释掉了，



































