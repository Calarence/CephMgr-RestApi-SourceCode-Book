# RequestViewSet

用来追踪和管理一些比较耗时的操作\(如创建Pool\)。这种类型的请求到达时，服务会立即返回202状态码和requestID，然后根据requestID可以了解该操作的进展以及完成情况。可以根据‘complete’、‘submitted’关键字对request进行过滤;也可以根据requestID取消某个操作。

