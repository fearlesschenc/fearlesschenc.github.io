## 产品部署步骤

### 依赖

* 部署在计算集群

* storageclass 必须提供才能创建出集群

* 必须在 values 里提供对象存储的 AK/SK 以及访问地址

* labels
  * 给 zookeeper-operator 可以调度的节点打上 skiff/paas: true
  * 给所有 zookeeper 可以调度的节点打上 skiff/paas-zookeeper: true
  * 给所有 zookeeper 可以调度的节点打上 failure-domain.beta.kubernetes.io/zone: {az}

### 手动部署和配置

* 创建 namespace： `kubectl create namespace paas-operator`

### 自动化部署和配置

* `helm -n paas-operator install paas-zk ./paas-zk`

#### 组件自有配置特别说明

```
image_pull_policy: IfNotPresent
nos:
  url: nos-jd.163yun.com
  bucket: ncr-jd-beta
  ak: 595da7952d29400680b2437a1c9fc26f
  sk: 11b22a95ee304f168b3f3d426296ca85
```

* nos 表示对象存储的配置
  * url 表示对象存储的地址
  * bucket 表示使用的对象存储的 bucket
  * ak/sk 表示对象存储的 access_key 和 secret_key
* image_pull_policy 表示 Pod 拉镜像的策略，无特殊情况无需配置

### 测试验证

在计算集群执行

```
kubectl -n paas-operator get csv
```

找到 zookeeper-operator，如果安装状态显示 Succeed 表示部署成功

### 卸载

```
helm uninstall -n paas-operator paas-zk
```

