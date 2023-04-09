

<!--

**Here are some ideas to get you started:**

🙋‍♀️ A short introduction - what is your organization all about?
🌈 Contribution guidelines - how can the community get involved?
👩‍💻 Useful resources - where can the community find your docs? Is there anything else the community should know?
🍿 Fun facts - what does your team eat for breakfast?
🧙 Remember, you can do mighty things with the power of [Markdown](https://guides.github.com/features/mastering-markdown/)
-->

Hi there 👋
> 国内安装K8S基本镜像站---> lank8s.cn  
> 最新内容请查看 [lank8s.cn服务文章](https://liangyuanpeng.com/post/cncf-kubernetes/service-lank8s.cn/)

欢迎使用，有问题/建议都可以到[lank8s.cn服务文章](https://liangyuanpeng.com/post/cncf-kubernetes/service-lank8s.cn/)或[这个issue](https://github.com/liangyuanpeng/liangyuanpeng.github.io/issues/84)留下你的评论

`lank8s.cn`的使命是希望国内能够更低门槛的学习Kubernetes技术!

在微软的镜像代理节点还可用的时候,`azk8s.cn`一直是一个很好的选择,但是2020年上半年微软不再对外提供azk8s服务,只对微软云的国内服务器提供服务,非常的遗憾。

在这样一个背景下我创立了`lank8s.cn`,这是对上游`k8s.gcr.io`搭建的代理,`k8s.gcr.io`有的镜像那么`lank8s.cn`就可以拉取,希望国内技术人在学习K8S之初能够很好的进行一个Kubernetes的Hello World!

使用的方式也非常简单,如果使用了kubeadm来进行搭建K8S集群,只需要一行命令就可以快速开始：

```shell
kubeadm init --image-repository=lank8s.cn --kubernetes-version=v1.17.4 --pod-network-cidr=10.244.0.0/16 --service-cidr=10.96.0.0/12 --ignore-preflight-errors=Swap 
```  

其中使用image-repository参数指定镜像的仓库为`lank8s.cn`即可.

上述例子是部署一个1.17.4版本的K8S,如需其他版本可自行修改.   

# lank8s.cn和registry.aliyuncs.com/google_containers的区别  

registry.aliyuncs.com/google_containers是定时同步kubernetes的镜像到阿里镜像仓库服务的,但只是K8S组件的镜像,可以看下和lank8s.cn的对比:  

   |         | k8s组件镜像    |  k8s.gcr.io其他镜像  |  及时性  |  容易记  |  
   | --------   | -----:   | :----: |  :----: |  :----: |  
   | registry.aliyuncs.com/google_containers       | 支持      |   不支持    | 定时,存在时间差    |  容易记    |  
   | lank8s.cn        | 支持      |   支持    |  直接从k8s.gcr.io拉取,不存在时间差    |   容易记,短域名   |  
   
# 技术使人懒惰   

我们知道,不管使用哪一种方式,我们都少不了的步骤时再部署一些`k8s.gcr.io`的资源时需要在部署前将`k8s.gcr.io`的镜像修改为国内某个地方(例如`lank8s.cn`),这样的事情做得多了也会显得繁琐.

因此我们即将推出一个k8s mutating webhook, 这个webhook的唯一作用就是在创建或更新资源(例如Deployment,Statefulset)将`k8s.gcr.io`修改为`lank8s.cn`.后续也会支持参数化,例如支持配置将`registry.aliyuncs.com/google_containers`修改为`lank8s.cn`




