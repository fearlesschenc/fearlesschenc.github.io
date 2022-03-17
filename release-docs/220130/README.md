## 功能新增和修改

* 多 AZ 调度：尽量均匀的调度 Pod 到多个 AZ
* 动态扩容 PVC：支持资源规格的修改
* 备份恢复
  * 支持可配置的对象存储地址
  * 支持集群备份
  * 支持基于 Crontab 格式的定时备份功能，可配置保留成功备份的份数，失败备份的份数
  * 支持集群备份恢复
* 支持多个 CR 同时 Reconcile
* 支持可配置当集群删除时是否删除 PVC 
* CR 中增加节点是否可读

## 修复的BUG

* 修复当 spec.labels 修改时集群不滚动更新
* 修复没有更新但是日志里显示更新 StatefulSet 的问题

## 其余部署相关更改

* helm中新增日志采集配置文件 `clusterlogconfig.yaml` 和 `verify-clgc.yaml` ，用于适配日志采集和去除 clusterlogconfig上多余的label，clusterrole中新增对`clusterlogconfig`的权限；