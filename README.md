# Zheng-Pages-docker.io
该项目是一个基于Cloudflare的Pages实现的Docker镜像代理工具。可以有效的中转对Docker官方镜像的请求，解决当下访问限制问题



@[TOC](目录)
# 前言

近期docker官方镜像拉取经常容易出现网络超时，下面为一些常用的处理解决部分

> **实现docker镜像拉取加速解决方案**
> 1. 直接使用一些大佬搭建好的镜像加速服务
> 2. 通过使用Cloudflare免费自建一个自己的镜像加速服务实现可以有效的解决无法拉取镜像的问题


# 一、直接配置镜像加速地址
下面是一些第三方的镜像加速地址或者镜像代理
1.镜像代理地址：
| 提供商 | 	地址 |
| --- | --- |
| DaoCloud | https://docker.m.daocloud.io/ |
| 阿里云 | https://<your_code>.mirror.aliyuncs.com |
| Docker镜像代理 | https://dockerproxy.com/ |
| 百度云 | https://mirror.baidubce.com/ |
| 南京大学 | https://docker.nju.edu.cn/ |
| 中科院 | https://mirror.iscas.ac.cn/ |


2. 第三方镜像地址
```powershell

https://docker.registry.cyou
https://docker.jsdelivr.fyi
https://dockerpull.com
https://dockerhub.icu
https://docker.ckyl.me
https://hub.uuuadc.top
```


把镜像加速地址添加到`/etc/docker/daemon.json`文件中

```powershell
	{
	    "registry-mirrors": [
	        "https://zhengfp.cn" # 请替换为您自己的自定义域名
	    ]
	}
```

# 二、自己搭建中转服务进行镜像加速
## 1、Fork副本
Fork副本到自己的github仓库


## 2、创建cloudflare
1. 创建/登陆cloudflare账号

	官网：[https://dash.cloudflare.com](https://dash.cloudflare.com)
	登陆进去是这样，可以切换为中文
![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/29f1e7d164cd46c9a70b5717c6098dcb.png)

2. 拉取项目
![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/46a00be0091d4060a3ed6b18a9a149ff.png)
- 选择Pages，连接到Git
![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/6e6396657ac14f5cb6ca4cde126e34e8.png)
- 跳转账号后选择刚刚Fork的项目，添加配置访问权限

	![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/3deb859fe7cf4439a5530b47c1ec6508.png)
- 选择存储库，点击`开始设置`
![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/21ef4ac679b84bf1a14179493c797cb6.png)

- 滑到最下面，点击开始部署，不用修改本页的配置
![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/1c172485aef54b18a992bfed19e3fb66.png)
- 部署成功
![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/6ee644204fa0411f8d3764270fd666aa.png)





## 3、注册域名


**华为云域名注册**：[https://www.huaweicloud.com/product/domain.html](https://www.huaweicloud.com/product/domain.html)

1. 选择注册一个自己的域名，新用户价格比较便宜，一块钱就解决了！
![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/7dd20f0d8ec74bd3b212777ddda60051.png)
2. 设置自定义域
- 注册好之后，在回到cloudflare，点击设置自定义域![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/0c6af764f0d947acbc27c3b5f3161cfd.png)
输入刚刚注册的域名
![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/7aa026004f374ec3acd359f945b3bac0.png)

![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/a1a37a483d854af8b63b2cf88439f18d.png)

- 把域名注册到cloudflare来，再点击`继续`
![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/22f32f9662f448e7a202f767a5be274e.png)



选择免费的社区版就行，在点击`继续`
![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/50bf4af0b14244d3ac675e94a90d5e66.png)
- 点击继续
![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/e18006354ca54042bfb588af4a74d67a.png)
- 会得到两个名称服务器
![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/9bfc6790b9de4428b33e41d3e7789031.png)



![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/a99f01732f1c487b918abf60de3c0f45.png)


- 进入[域名注册控制台](https://console.huaweicloud.com/domain/?region=cn-north-4#/domain/list)
进入“域名列表”页面。

在域名列表中，单击“域名”列的待修改DNS服务器的域名。
![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/6a9aafeab6124f0d8b2e0a89ebad36e3.png)
- 进入域名信息页面
点击修改，把上面的两个名称DNS服务器，填入，然后就是等待，**注册机构最多需要 24 小时处理名称服务器更改**
![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/ef902c19b3ca4d098d83ff6f6876613a.png)

- 一般需要等待一两个小时，具体看注册机构
![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/2ede8df777d94633b4b35805c95ee835.png)

- 等待域名变绿，显示`有效`就代表成功了，

![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/f1c53b9a55dd4147af63680bc222b411.png)

- 分配的临时域名，也可以使用
![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/ed250752ac2448878b8c83ab0e0457e8.png)
- 查看测试是否成功
直接访问域名，就可以进入官网了
![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/141b241369774a08965a9dd10092be7d.png)

## 4、测试使用
1. 使用中转服务直接拉取
- 在没使用中转镜像之前，直接拉取就压根拉取不下来
![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/c7f6eaf377a848f5b7b26606ccedb96b.png)


- 使用镜像中转站拉取镜像，就成功拉取到，就是在要拉取的官方镜像前面加上你的`域名`
![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/0333f764bdf04da296b486f06ac42ebb.png)


2. 直接配置镜像加速
修改文件 `/etc/docker/daemon.json`（如果不存在则创建）

	```powershell
	{
	    "registry-mirrors": [
	        "https://zhengfp.cn" # 请替换为您自己的自定义域名
	    ]
	}
	```

## 5、配置变量
这里需要把我们的域名主页屏蔽掉，避免可能会被DNS污染，把我们的地址屏蔽掉。

回到**cloudflare**点击你的Pages项目，点击设置，添加环境变量，也可以设置一个，或者可以不设置，不是必须的，主要是安全起见，还是建议任选一种设置
|  变量名|示例  |备注|
|--|--|-|
| URL302| [https://blog.csdn.net/weixin_52315708](https://blog.csdn.net/weixin_52315708) | 重定向，表示进入主页会重定向到哪，比如我这重定向到了我的博客地址|
|URL  | nginx |主页伪装，设置nginx，表示伪装成nginx的页面，也可以设置www.baidu.com，或者其他的地址|

![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/8a0829db5c8c4bf38306f2bdeffedeb6.png)

部署好之后，重新部署一下，在点击时，就会被重定向到我们设置的地址
![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/531bc39c74d94f40b472eb7e10dee9b9.png)
