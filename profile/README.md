

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

`lank8s.cn`的使命是希望国内能够更低门槛的学习Kubernetes技术!

在微软的镜像代理节点还可用的时候,`azk8s.cn`一直是一个很好的选择,但是2020年上半年微软不再对外提供azk8s服务,只对微软云的国内服务器提供服务,非常的遗憾。

在这样一个背景下我创立了`lank8s.cn`,目前只提供搭建K8S所需要的最基本的镜像,希望国内技术人在学习K8S之初能够很好的进行一个Kubernetes的Hello World!

使用的方式也非常简单,如果使用了kubeadm来进行搭建K8S集群,只需要一行命令就可以快速开始：

```shell
kubeadm init --image-repository=lank8s.cn --kubernetes-version=v1.17.4 --pod-network-cidr=10.244.0.0/16 --service-cidr=10.96.0.0/12 --ignore-preflight-errors=Swap 
```  

其中使用image-repository参数指定镜像的仓库为`lank8s.cn`即可.

上述例子是部署一个1.17.4版本的K8S,如需其他版本可自行修改.   

# 付费服务  

即将会推出`quay.io`和`gcr.io`的短域名镜像代理服务,并且采取收费策略,30半年,50一年.有意者请加我微信,谢谢!  

![weixin](https://res.cloudinary.com/lyp/image/upload/v1614786289/weixin.jpg)

# 接受赞助

为了提供更好的服务,我在下面贴出两个二维码接受赞助,我承诺所有赞助都只会用于优化`lank8s.cn`服务.  

![zhifubao](https://res.cloudinary.com/lyp/image/upload/v1616142335/pay/zhifubao.png)  

![weixin](https://res.cloudinary.com/lyp/image/upload/v1616142330/pay/weixin.png)




