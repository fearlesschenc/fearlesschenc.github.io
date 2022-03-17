## 产品部署步骤

### 依赖

* 部署在管控集群

### 手动部署和配置

* 创建 namespace： `kubectl create namespace paas-template`

* 需要在 coredns 里加一行配置 `{{ .Values.module_domains.paas_template }}` 对应的域名的解析

### 自动化部署和配置

* `helm -n paas-template install paas-template ./paas-template`

#### 组件自有配置特别说明

```
image_pull_policy: IfNotPresent
```

* image_pull_policy 表示 Pod 拉镜像的策略
* 无特殊情况无需配置其他参数

### 测试验证

在计算集群执行

```
kubectl -n paas-template get po && kubectl -n paas-template logs -f {podName}
```

如果 Pod 日志不报错，说明部署成功

### 卸载

```
helm uninstall -n paas-template paas-template
```

