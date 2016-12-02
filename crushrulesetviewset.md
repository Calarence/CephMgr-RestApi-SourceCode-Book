CrushRuleSetViewSet和CrushRuleViewSet代码调用流程是一样的，只是数据处理不同，CrushRuleSet返回的是rule集合，而CrushRule返回的是某条rule

![](/assets/ceph-mgrOO1.png)

` rules = self.client.list(CRUSH_RULE, {})`

` osds_by_rule_id = self.client.get_sync_object(OsdMap, ['osds_by_rule_id'])`

CrushRuleSetViewSet和CrushRuleViewSet都用到了这两行代码，然后对返回结果进行处理，最后返回Response。所以重点关注这两个方法。

---------------------------------------

