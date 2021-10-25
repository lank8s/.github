

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

欢迎使用，有问题/建议都可以到lank8scn的github库提issue!

lank8s.cn的使命是希望国内能够更低门槛的学习Kubernetes技术!

在微软的镜像代理节点还可用的时候,azk8s.cn一直是一个很好的选择,但是2020年上半年微软不再对外提供azk8s服务,只对微软云的国内服务器提供服务,非常的遗憾。

在这样一个背景下我创立了lank8s.cn,目前只提供搭建K8S所需要的最基本的镜像,希望国内技术人在学习K8S之初能够很好的进行一个Kubernetes的Hello World!

使用的方式也非常简单,如果使用了kubeadm来进行搭建K8S集群,只需要一行命令就可以快速开始：

```shell
kubeadm init --image-repository=lank8s.cn --kubernetes-version=v1.17.4 --pod-network-cidr=10.244.0.0/16 --service-cidr=10.96.0.0/12 --ignore-preflight-errors=Swap 
```  

其中使用image-repository参数指定镜像的仓库为lank8s.cn即可.

上述例子是部署一个1.17.4版本的K8S,如需其他版本可自行修改.
