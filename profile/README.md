
# Auto generate from https://liangyuanpeng.com/post/service-lank8s.cn/

Hi there 👋  

> 国内安装K8S基本镜像站---> lank8s.cn


欢迎使用，有问题/建议都可以加我微信交流，在博客底部可以找到我的微信联系方式 :)

`lank8s.cn`的使命是希望国内能够更低门槛的学习 Kubernetes 技术!

在微软的镜像代理节点还可用的时候,`azk8s.cn`一直是一个很好的选择,但是2020年上半年微软不再对外提供azk8s服务,只对微软云的国内服务器提供服务,非常的遗憾。

在这样一个背景下我创立了 `lank8s.cn`,目前只提供搭建K8S所需要的最基本的镜像,希望国内技术人在学习K8S之初能够很好的进行一个 Kubernetes 的 Hello World!

使用的方式也非常简单,如果使用了 kubeadm 来进行搭建K8S集群,只需要一行命令就可以快速开始：

```shell
kubeadm init --image-repository=lank8s.cn --kubernetes-version=v1.17.4 --pod-network-cidr=10.244.0.0/16 --service-cidr=10.96.0.0/12 --ignore-preflight-errors=Swap 
```  

其中使用 image-repository 参数指定镜像的仓库为`lank8s.cn`即可.

上述例子是部署一个 1.17.4 版本的 K8S ,如需其他版本可自行修改.   

# lank8s.cn和registry.aliyuncs.com/google_containers的区别  

registry.aliyuncs.com/google_containers 是定时同步kubernetes的镜像到阿里镜像仓库服务的,但只是K8S组件的镜像,可以看下和 lank8s.cn 的对比:  


 | k8s组件镜像    |  k8s.gcr.io其他镜像  |  及时性  |  容易记 
--------   | :--------:   | :----: |  :--------: |  :--------:
registry.aliyuncs.com/google_containers       | 支持      |   不支持    | 定时,存在时间差    |  容易记 
lank8s.cn        | 支持      |   支持    |  直接从 registry.k8s.io 拉取,不存在时间差    |   容易记,短域名
   
# 技术使人懒惰   

我们知道,不管使用哪一种方式,我们都少不了的步骤时再部署一些 `registry.k8s.io` 的资源时需要在部署前将 `registry.k8s.io` 的镜像修改为国内某个地方(例如 `lank8s.cn`),这样的事情做得多了也会显得繁琐.  

~~因此我们即将推出一个k8s mutating webhook, 这个webhook的唯一作用就是在创建或更新资源(例如Deployment,Statefulset)将`k8s.gcr.io`修改为`lank8s.cn`.后续也会支持参数化,例如支持配置将`registry.aliyuncs.com/google_containers`修改为`lank8s.cn`~~  

你可以为 containerd 配置仓库镜像,这样当你拉取 registry.k8s.io 的镜像时，不再需要去手动为每个镜像修改地址,可以直接使用到 lank8scn 服务. 参考[文章:为containerd配置仓库镜像](https://liangyuanpeng.com/post/cncf-containerd/registry-mirrors-for-containerd/)

# 服务说明  

## 仓库镜像对应

原始仓库    |  lank8s服务 
 --------   | :--------:   
  registry.k8s.io      |   registry.lank8s.cn   
  registry.k8s.io      |   lank8s.cn  
 gcr.io     |   gcr.lank8s.cn   


## 使用

由于维护 `lank8s.cn` 存在一定的经济压力(服务器费用,域名费用,带宽费用等),因此 `lank8s.cn` 保证可用性,但不保证绝佳的镜像下载速度.   

这样的原因是越来越多人使用 `lank8s.cn`,镜像下载速度会变慢,而提升服务器配置/带宽是解决这类问题的方法.如果有对 `lank8s.cn` 的赞助将把所有赞助都使用在 `lank8s.cn` 服务的优化上.

# 安全性

由于 lank8s.cn 是一个镜像服务,那么必然会存在一个安全性的问题,如何保证拉取到的容器镜像与上游(gcr.io 等地址)的容器镜像是相同的呢? 

可以看看官方文章:[验证已签名容器镜像](https://kubernetes.io/zh-cn/docs/tasks/administer-cluster/verify-signed-artifacts/)  

从文章中了解到,kubernetes 1.24以及之后版本的内容都可以使用 cosign 来校验 kubernetes 组件的数据完整性.

这里给出一个简单的校验容器镜像的示例:

```shell
COSIGN_EXPERIMENTAL=1 cosign verify registry.lank8s.cn/kube-apiserver-amd64:v1.24.0
```

校验 kube-apiserver 1.24 版本的镜像.

注意:你从哪里下载的镜像就从哪里校验镜像,例如如果你的镜像地址是 `abc.com/kube-apiserver-amd64:v1.24.0`,那么你的校验命令应该是:

```shell
COSIGN_EXPERIMENTAL=1 cosign verify abc.com/kube-apiserver-amd64:v1.24.0
```

# k8s.lank8s.cn 将被淘汰

官方镜像 `k8s.gcr.io` 使用 `registry.k8s.io` 替代,而 lank8s 服务也会跟随上游,将 `k8s.lank8s.cn` 淘汰,请使用 `registry.k8s.io` 的镜像服务 `registry.lank8s.cn`.

# 应用场景

除了拉取 K8S 官方组件镜像之外,典型的应用场景有以下几个:  

- tekton 镜像,使用 gcr.lank8s.cn/tekton-releases 来拉取 gcr.io/tekton-releases 下的镜像
- knative 镜像, 使用 gcr.lank8s.cn/knative-releases 来拉取 gcr.io/knative-releases 下的镜像
- ml-pipeline 镜像,使用 gcr.lank8s.cn/ml-pipeline 来拉取 gcr.io/ml-pipeline 下的镜像
- kubernetes 的 CI 镜像,使用gcr.lank8s.cn/k8s-staging-ci-images 来拉取 gcr.io/k8s-staging-ci-images 下的镜像
- 使用 gcr.lank8s.cn/google_samples 来拉取 gcr.io/google_samples 下的镜像
- 使用 gcr.lank8s.cn/distroless 来拉取 gcr.io/distroless 下的镜像
- 使用 gcr.lank8s.cn/etcd-development 来拉取 gcr.io/etcd-development 下的镜像
- 使用 gcr.lank8s.cn/k8s-staging-sig-auth 来拉取 gcr.io/k8s-staging-sig-auth 下的镜像  

# 可能的付费服务  

为什么是可能呢?  

因为在服务器压力承受范围内的话`gcr.lank8s.cn`、`lank8s.cn`、`registry.lank8s.cn`、`k8s.lank8s.cn` 都会免费提供服务,但使用的人越来越多之后服务器承受不了太多人共同使用时`gcr.lank8s.cn`(`lank8s.cn`/`registry.lank8s.cn`依然是免费服务)将会作为付费服务推出.经过多次决策,最终定价为15一年.有意者请加我微信,谢谢!  

由于本意不是为了赚钱,因此即使是收费也会采取比较宽容的策略,比如付费用户在登录了 `lank8s.cn` (拉取镜像时带有正确的认证信息)后其所在 IP 都可以免费(无需登录)拉取镜像.

也就是一个局域网内,只要有一个节点登录了 `lank8s.cn`,那么其他节点都可以直接使用服务.

在服务免费期间成为了付费用户的人员将会额外赠送一年使用时间.

![weixin](https://res.cloudinary.com/lyp/image/upload/v1614786289/weixin.jpg)

# 额外的免费服务

- proxy.lank8s.cn/googleapis/oauth2/v3/certs 代理 https://www.googleapis.com/oauth2/v3/certs
- proxy.lank8s.cn/gh/avatars/  代理  https://avatars.githubusercontent.com/
- proxy.lank8s.cn/gh/api 代理 https://api.github.com   本意是加速 giscus 评论

例如 原地址为 https://avatars.githubusercontent.com/u/19399934?v=4 替换为 https://proxy.lank8s.cn/gh/avatars/u/19399934?v=4

注意 目前这些服务都始于我个人的需要,随时会关闭,如何对你有帮助欢迎评论在此博客留下你的评论,某个服务达到足够热度会考虑长期维护.

# 额外付费服务

## 为 us-central1-docker.pkg.dev 提供镜像服务,8元3个月. 

映射关系:  

us-central1-docker.pkg.dev ---> us-central1-docker.pkgdev.lank8s.cn

镜像案例:

- https://docs.robusta.dev  kubernetes的可观测性监控方案

## 代理 api.github.com

加我微信与我联系:)


# 接受赞助

为了提供更好的服务,`lank8s.cn`服务接受赞助,我承诺所有赞助都只会用于优化`lank8s.cn`服务.点击本文下方的赞助按钮开始赞助:)



