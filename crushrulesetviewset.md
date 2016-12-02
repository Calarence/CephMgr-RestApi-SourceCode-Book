CrushRuleSetViewSet和CrushRuleViewSet代码调用流程是一样的，只是数据处理不同，CrushRuleSet返回的是rule集合，而CrushRule返回的是某条rule

![](/assets/ceph-mgrOO1.png)

`rules = self.client.list(CRUSH_RULE, {})`

`osds_by_rule_id = self.client.get_sync_object(OsdMap, ['osds_by_rule_id'])`

CrushRuleSetViewSet和CrushRuleViewSet都用到了这两行代码，然后对返回结果进行处理，最后返回Response。所以重点关注这两个方法。

---

_**rules获取过程**_

![](/assets/getRules.png)

上图大体表示出了获取rules流程,代码调用到最好，用到了ceph\_state,它是一个c++封装的插件，负责从ceph-mgr daemon获取集群状态，由于我不懂c++，并没有继续深究下去，但ceph\_state是很重要的部分，可以说是连接ceph-mgr daemon与api的桥梁，以后让同事帮忙看一下这部分。

---

_**osds\_by\_rule\_id获取流程**_

![](/assets/osds_by_rule_id.png)

对比上图发现，代码调用到最好都是通过ceph\_state去获取ceph 集群状态。

