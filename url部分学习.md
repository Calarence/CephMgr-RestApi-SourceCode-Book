ceph-mgr rest api 和calamari rest api是相同的作者，他们直接把calamri的api移植到ceph-mgr中\(关于两者的区别，[点这里](https://github.com/Tendrl/documentation/pull/57/files)\)，现有API 24个。所涵盖的对象包括User Requestrian、Osd、Pool、Config、Health、Mon以及Server。具体对象上现有操作见下表。

| 对象 | 对象上的操作 |
| :---: | :--- |
| request | 取消某个请求/查看某个 请求/查看请求列表/查看某个集群上的某个请求/查看某个集群上的请求列表 |
| crush\_rule\_set | crush\_rule\_set查看 |
| crush\_rule | crush\_rule查看 |
| pool | 集群pool的列表查看、增加；集群某个Pool的查看 、更改以及删除 |
| osd | 集群osd列表查看，集群某个osd查看、修改， |
| osd\_command | OSD上可执行的命令、OSD上已经实现的命令 |
| osd\_config | 集群osd\_config查看、更新 |
| mon | 集群mon列表查看；获取集群上的某个mon |
| server | server列表获取；获取某个server |
| config | 集群config列表获取；获取某个config |

