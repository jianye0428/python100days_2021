- [1. 了解Github](#1-了解github)
- [2. 注册Github](#2-注册github)
- [3. 访问不了Github怎么办](#3-访问不了github怎么办)
- [4. 了解一些项目页面](#4-了解一些项目页面)
- [5. 在码云平台创建项目](#5-在码云平台创建项目)
- [6. Git创建项目](#6-git创建项目)
- [7. 推送到远程仓库](#7-推送到远程仓库)
- [8. 更新到本地仓库](#8-更新到本地仓库)
- [10. 部署公钥管理](#10-部署公钥管理)
- [11. 如何白嫖别人的资料](#11-如何白嫖别人的资料)
- [12. 文章推荐](#12-文章推荐)
# 1. 了解Github
Git是一个跟踪代码更改的版本控制系统，而GitHub是一个基于Web的Git版本控制存储库托管服务。它提供了Git的所有分布式版本控制和源代码管理（SCM）功能，并提供了一些自己的特性。对于开发人员而言，这是他们可以在其中存储项目并与志趣相投的人建立联系的地方。您可以将其视为“代码云”。（百度百科）

其实，Github就是放代码的地方，通过Git来上传提交代码。

# 2. 注册Github
# 3. 访问不了Github怎么办
访问Github突然上不去了，出现了网页无法正常运行？

![](https://camo.githubusercontent.com/22e5df7d61e2d217da59d3cc8cabe0f1810a33f495941d86079f212b7103c99b/68747470733a2f2f696d672d626c6f672e6373646e696d672e636e2f32303230303531313136303132363637372e706e67)

你应该知道Github在外国，当然访问慢了。只要修改hosts，80%可以解决。

打开Dns检测|Dns查询 ，这里推荐站长工具

http://tool.chinaz.com/dns?type=1&host=github.com&ip=

![](https://camo.githubusercontent.com/f16a4b7a6f27d2ce76afbeb491c82f749ff214211b3246d9e01f8fab43c09ce6/68747470733a2f2f696d672d626c6f672e6373646e696d672e636e2f32303230303531313136303731343433392e706e67)

把检测列表里的TTL值最小的IP输入到hosts里，并对应写上github官网域名

下面是不同系统的hosts
```
Windows 系统位于 C:\Windows\System32\drivers\etc\
Android（安卓）系统hosts位于 /etc/
Mac（苹果电脑）系统hosts位于 /etc/
iPhone（iOS）系统hosts位于 /etc/
Linux系统hosts位于 /etc/
```

我这里使用Notepad++打开的，填写的是以前的hosts
![](https://camo.githubusercontent.com/309c4ce03412cc4bafa8053992b114ad42ff26125fe968ad6946a5dd6b3ce914/68747470733a2f2f696d672d626c6f672e6373646e696d672e636e2f32303230303531313136303430353138382e706e67)

如果你的Github真的访问不了，那用码云吧，码云是我国开发者为了打破Github垄断，仿照Github诞生的，网址：https://gitee.com/

# 4. 了解一些项目页面
现在我找到一个Java项目，找到一个很多人点赞的Java项目，写的应该是教程，
![](https://camo.githubusercontent.com/d844e01b6d1f8cd3afc5972734f1482bac0614d900d79fc6ac1a603bdcaafdd8/68747470733a2f2f696d672d626c6f672e6373646e696d672e636e2f32303230303531313136323335333639322e706e67)

如果你能够修复bug或自己添加功能 ，请发一个pull request吧！如果你提交了一个pull request，维护者就会将你的分支与已有的分支作比较来决定是否要合并。

不要想得不可能，我记得的有一个6岁的孩子pull request通过了，就是因为在注释中写了一个*号，可以显得更加严谨好看。

# 5. 在码云平台创建项目
![](https://camo.githubusercontent.com/5812b54784cc5a030df15f96eca899533345758d4e7a089e2b99b0a27b3b1189/68747470733a2f2f696d672d626c6f672e6373646e696d672e636e2f323032303035313131363434313736302e706e67)
创建成功后，之后会出现以下界面的信息。
![](https://camo.githubusercontent.com/655a25597780d57010c8fd33750532e212b890f716b034ee6490a900b280efde/68747470733a2f2f696d672d626c6f672e6373646e696d672e636e2f32303230303531313136353133343538322e706e67)

创建好仓库后，你的仓库会有两个地址，一个是https，一个是ssh。因为使用https需要输入用户名和密码，推荐使用ssh的方式。要使用ssh你需要设置你账户的ssh公钥。

下一步点击下载SSH，复制下来，也就是git@gitee.com:MaoliRUNsen/python_from_novice_to_master.git

远程仓库里已经存在项目文件，你买了台新电脑，需要将项目从远程仓库clone到本地进行工作。

在新电脑新建一个文件夹，再使用git clone git@gitee.com:MaoliRUNsen/python_from_novice_to_master.git克隆下来。
![](https://camo.githubusercontent.com/0ee27d13ae37c3c3b2c83f526d7f35872c33cf688471993811054046fbce94e4/68747470733a2f2f696d672d626c6f672e6373646e696d672e636e2f32303230303531313136353332363633302e706e67)

只要你克隆远程仓库，这样你就可以同步到码云。

# 6. Git创建项目
要把本地仓库和远程仓库联系起来有两种方式， 上面是第一种，另一种是通过Git创建项目

和第一种方式的区别在于先创建仓库，
```
git init	# 创建仓库
git remote add origin git@gitee.com:MaoliRUNsen/python_from_novice_to_master.git
```

# 7. 推送到远程仓库
当本地工作完成，需要将代码推送到远程仓库，使用git push命令
```
git push origin master
```
push前需要add和commit

# 8. 更新到本地仓库
你的同事和你协同开发，他工作的那部分内容完成了，并且已经推送到远程仓库，你接下来的工作需要依赖他的那部分代码，那么你需要将远程仓库代码拉取到本地仓库，使用git pull命令
```
git pull origin master
```

#9. 仓库成员管理
终于到了重点的时候，我们在新建项目的时候，只是写了基本设置
![](https://camo.githubusercontent.com/e3543a705283bfa551fe8b207c4eab4fb78db851335fd3582187c25e62f8d5b8/68747470733a2f2f696d672d626c6f672e6373646e696d672e636e2f3230323030353131313731393136312e706e67)

| 成员角色 | 权限 |
| :-----:| :----:|
| 访客（登录用户） | 对于公有仓库：创建 Issue、评论、Clone 和 Pull 仓库、打包下载代码、Fork 仓库、 Fork 仓库提交 Pull Request、下载附件 |
| 报告者 | 继承访客的权限。 私有仓库：不能查看代码、不能下载代码、不能 Push 、不能 Fork 、 不能提交 Pull Request、可下载附件，不能上传附件，不能删除附件 | 
|观察者|继承报告者权限 私有仓库：创建 Wiki、可以 Clone 下载代码、可以 Pull、不能 Fork
|开发者|创建 Issue、评论、Clone 和 Pull 仓库、Fork 仓库、打包下载代码、创建 Pull Request、 创建分支、推送分支、删除分支、创建标签（里程碑）、 创建 Wiki、可上传附件，可删除自己上传的附件，不能删除他人上传的附件|
|管理员|创建 Issue、评论、Clone 和 Pull 仓库、打包下载代码、创建 Pull Request、 创建分支、推送分支、删除分支、创建标签（里程碑）、创建 Wiki、 添加仓库成员、强制推送分支、编辑仓库属性、可上传附件，可删除自己或他人上传的附件、 不能转移/清空/删除仓库|

这里你直接可以邀请用户，注意这个和Fork是不一样的，Fork就是提交修改的请求，需要成员的同意。新建成员就可以同意提交修改的请求。

![](https://camo.githubusercontent.com/2f913792cc3791d5c999dcb56e2cebd14958e7e7d4a4484299ce2f9706aae9df/68747470733a2f2f696d672d626c6f672e6373646e696d672e636e2f32303230303531313137323333343835302e706e67)

# 10. 部署公钥管理
公钥是什么，就是管理这个项目的钥匙，一般都是项目成员有的。

SSH协议的Git服务，在使用SSH协议访问仓库仓库之前，需要先配置好账户/仓库的SSH公钥。

你需要用Git的SSH 创建Key，然后把这个key放在这个仓库中，一般针对是仓库不是你托管的，在别人平台，你也是项目的成员。
```
YIUYE@DESKTOP-5EEO47M MINGW64 ~
$ ssh-keygen -t rsa -C "2953510364@qq.com"
Generating public/private rsa key pair.
Enter file in which to save the key (/c/Users/YIUYE/.ssh/id_rsa):
/c/Users/YIUYE/.ssh/id_rsa already exists.
Overwrite (y/n)?

YIUYE@DESKTOP-5EEO47M MINGW64 ~
$ pwd
/c/Users/YIUYE

YIUYE@DESKTOP-5EEO47M MINGW64 ~
$ cd .ssh

YIUYE@DESKTOP-5EEO47M MINGW64 ~/.ssh
$ ls
id_rsa  id_rsa.pub  known_hosts

YIUYE@DESKTOP-5EEO47M MINGW64 ~/.ssh
$ cat id_rsa.pub
ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQC/bZaaJ9lO2a9AAuMWVpdsZfIVr4wqBA2vNAsButaNIMAx0OkYrfTloLl138+khQqteZ5b9lZdmiYEuAIS8UlBEdHmNo4LiJrLi4DdqOajpsbbdTmjCc4rlEraKOH2qVOTNEj6E+0oeYnnbQlGcA/nKdVbN8bfcsMWiN82Bjn19dP3LXC4oubRP2jWR/X3KyYcX58z1oltCbaIHtgRs1kFp6srFcU067CSmMulxmFXTalWkRSPq1d/gNWUYpii14YBIFUvwLmJlrUtXBcGZGqZhqu50FjpRcCY0TRV3DqZAR2/KnsRN7VeyuYCDmeXKc+UyNeS3zPFgKS7oyFi60CB 2953510364@qq.com

```

![](https://camo.githubusercontent.com/3d1c06d3bd4fd21cfcd41991611c5992edd02b1d343263b2a3b30df1d8a611fe/68747470733a2f2f696d672d626c6f672e6373646e696d672e636e2f32303230303531313137333534313936372e706e67)

复制生成后的 ssh key，通过仓库主页 「管理」->「部署公钥管理」->「添加部署公钥」 ，添加生成的 public key 添加到仓库中。

![](https://camo.githubusercontent.com/0e9763b070fee873306d644f74b6f86252aaa9aa55d9fbee0bd32a3a5bcfc6c3/68747470733a2f2f696d672d626c6f672e6373646e696d672e636e2f32303230303531313137333833303339372e706e67)

添加后，在终端（Terminal）中输入
```
ssh -T git@gitee.com
```
首次使用需要确认并添加主机到本机SSH可信列表。若返回 Hi XXX! You've successfully authenticated, but Gitee.com does not provide shell access. 内容，则证明添加成功

部署公钥管理是针对不是你的项目而已，由于项目是我，做这个是没有任何意义的。

# 11. 如何白嫖别人的资料
Github上有很多开源免费的资料，很多人为了Star就开源了很多学习资料，在我国都是分享学习资料比较多，比如我搜索Python
![](https://camo.githubusercontent.com/dcd40a5281f509d21f9dd41b7e02bb0bd9ee32dae06965b626b82c261838355f/68747470733a2f2f696d672d626c6f672e6373646e696d672e636e2f32303230303531313137343234353734322e706e67)

下面就有几千个学习资料，所以学东西最好在Github，然后你就下载下来，学习别人是怎么写代码。
![](https://camo.githubusercontent.com/e94248516f781cef33750fd9cf1b1f255b1e7e87311b3910f2ab5fd3b65e2a6c/68747470733a2f2f696d672d626c6f672e6373646e696d672e636e2f32303230303531313137343430383232342e706e67)
还有很多人是为了找项目，在原始项目进行二次开发。白嫖的时候，请你注意版权。

# 12. 文章推荐
我主要推荐的Github的help官方文档

https://help.github.com/en

![](https://camo.githubusercontent.com/aa80391819681ada2eac68c533bfeea4bb2d8b843beb2eb1d56c1a45aec0f33e/68747470733a2f2f696d672d626c6f672e6373646e696d672e636e2f32303230303531313137343830333435372e706e67)

Github就主要看企业的文档和Github的桌面版

![](https://camo.githubusercontent.com/1c36ba34efc1c7855001cd062c7b256664807242cb2ebe1500df922ad2814547/68747470733a2f2f696d672d626c6f672e6373646e696d672e636e2f32303230303531313137343935313631372e706e67)

Github的桌面版以后接着写，还有码云的help官方文档：https://gitee.com/help/

![](https://camo.githubusercontent.com/307fb55fd09744ce9ab9a08db30427774d4d0155f749f6aa9019f0ccf4590ed4/68747470733a2f2f696d672d626c6f672e6373646e696d672e636e2f32303230303531313137353035383938332e706e67)