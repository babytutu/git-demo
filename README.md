# Git软件安装使用教程

> for mac -> see USAGE.md

## 1 安装Git

一切从这里开始 [官方下载地址](https://git-scm.com/downloads)

![img](images/win/1install-git.png)

## 2 配置 ssh-key

> Git使用`ssh/https`两种协议，关联`ssh-key`并使用`ssh协议`可以免去每次都输密码的麻烦
>
> 参考Git官方帮助文档：[生成 SSH 公钥](https://git-scm.com/book/zh/v2/%E6%9C%8D%E5%8A%A1%E5%99%A8%E4%B8%8A%E7%9A%84-Git-%E7%94%9F%E6%88%90-SSH-%E5%85%AC%E9%92%A5)

### 2.1 判断是否已有ssh-key

> 默认情况下，用户的 `ssh-key`存储在其 `~/.ssh` 目录

```bash
cd ~/.ssh
ls
```

如图所示，没有ssh-key

![img](images/win/2.1ssh-key-check.png)


### 2.2 生成新的ssh-key

> 已有`ssh-key`的跳过这一步

```bash
ssh-keygen
```

首先 `ssh-keygen` 会确认密钥的存储位置（默认是 `.ssh/id_rsa`），然后它会要求你输入两次密钥口令。如果你不想在使用密钥时输入口令，将其留空即可。

![img](images/win/2.2ssh-keygen.png)

执行`ssh-add`

```bash
eval $(ssh-agent)

ssh-add ~/.ssh/id_rsa
```

![img](images/win/2.2ssh-add.png)

###  2.3 将ssh-key关联到GitHub/GitLab

复制已有的`ssh-key`

```bash
cat ~/.ssh/id_rsa.pub
```

![img](images/win/2.3ssh-key-copy.png)

添加到gitlab Profile Setting ssh-keys ADD SSH KEY

![img](images/win/2.3add-ssh-keys.png)

### 2.4 验证ssh-key关联状态

>以GitHub为例,图中为设置成功的返回结果

```bash
ssh -T git@github.com
```

![img](images/win/2.4ssh-key-test.png)



## 3 安装Sourcetree

> 免费的Git客户端  [官方下载地址](https://www.sourcetreeapp.com)

- 非常高兴的宣布，sourcetree升级到v3了，然后注册账号的问题已经解决了，尴尬的是还是需要注册，那就注册吧，选择右边那个

![img](images/win/3install-sourcetree-step1.png)

- 在网页中完成注册，过程有点慢

![img](images/win/3install-sourcetree-step2.png)

- 进入一个简单的功能选择界面，如果之前没有安装`Git`，这个界面会自动下载安装
- 不要勾选`Mercurial`，它是Git的兄弟，咱们不用
- 打开高级选项，都勾上，一个是自动格式化换行符，一个是开启全局忽略文件的设置

![img](images/win/3install-sourcetree-step3.png)

- 总算装完了，简单配置下信息，顺便把讨厌的信息收集关闭

![img](images/win/3install-sourcetree-step4.png)

- 点击下一步，会出现个加载SSH密钥的提示框，选择***否***

![img](images/win/3install-sourcetree-step5.png)

- 看到这个界面，说明安装顺利完成

![img](images/win/3install-sourcetree-end.png)

## 4 Sourcetree简明使用指南

### 4.1 基础配置

#### 4.1.1 账户信息

先别急着加仓库，还是要简单设置下的，`工具-设置`

![img](images/win/4.1.1start-setting.png)

主要关注以下几点

- 默认用户信息，安装过程中已经输过了
- SSH客户端配置，选择`OpenSSH`，会自动加载SSH密钥
- Repo Settings，项目目录选好，以后远程仓库克隆下来就到这个文件夹下了，我只能说这个软件翻译做了一半，如果中文看不下去了，可以在这边切换语言，记得重启后才生效

![img](images/win/4.1.1setting.png)


### 4.2 新建/克隆仓库

Sourcetree提供若干添加仓库的方式

![img](images/win/4.2add-git.png)


#### 4.2.1 Clone

> 已配置并成功测试`ssh-key`后，请复制`ssh`开头的远程仓库地址

最常见的方式，从gitlab中拷贝地址，可以通过`高级选项-检出分支`来选择分支，git仓库缺省分支一般是master，而开发使用feature或者develop

![img](images/win/4.2.1clone-git.png)

添加成功后，自动进入仓库

![img](images/win/4.2.1clone-git-ok.png)

打开新标签后，会发现所有仓库列表多了个仓库

![img](images/win/4.2.1clone-git-list.png)


#### 4.2.2 Add

添加已经存在的本地仓库

![img](images/win/4.2.2add-local-git.png)


#### 4.2.3 Create

创建本地仓库，把本地文件夹变成一个本地仓库，可以通过关联远程仓库把本地仓库内容推送到远程仓库

![img](images/win/4.2.3create-local-git.png)



### 4.3 分支管理【Git-flow】

| 分支命名规则 | 功能         | 备注                        |
| ------------ | ------------ |--------------------------- |
| feature      | 功能分支     | 功能开发，每次从develop新建 |
| develop      | 开发分支     | 功能开发完毕后合并到此分支  |
| release      | 发布分支     | 从develop新建，发布tag      |
| hotfix       | 补丁分支     | 修复紧急bug                 |
| master       | 生产环境分支 | 用于记录发布版本            |


#### 4.3.1 初始化

> 新仓库先执行`Git工作流`，为分支设置前缀

![img](images/win/git-flow/4.3.1git-flow-reset.png)

Git flow的几个基本操作

![img](images/win/git-flow/4.3.1git-flow-detail.png)


#### 4.3.2 建立新的功能

![img](images/win/git-flow/4.3.2git-flow-feature.png)

功能开发完毕后，在feature分支点击Git工作流后，出现如下提示

![img](images/win/git-flow/4.3.2git-flow-feature-end.png)

点击完成当前项目，出现提示，默认会在完成功能后删除`feature`分支，会自动进行分支合并

![img](images/win/git-flow/4.3.2git-flow-feature-check.png)

#### 4.3.3 建立新的发布版本

> 默认从develop分支新建

![img](images/win/git-flow/4.3.3git-flow-release.png)

在release分支点击Git工作流后，出现如下提示

![img](images/win/git-flow/4.3.3git-flow-release-end.png)

点击完成当前项目，会出现如下信息，需要给发布的版本打`tag`同时默认删除`release`分支

![img](images/win/git-flow/4.3.3git-flow-release-check.png)

然后Git工作流会在master上打`tag`，并重新回到develop分支


#### 4.3.4 建立新的修复补丁

> 人无完人，bug永无止境，很可能刚发布一个`tag`，就忽然发现一个重大问题需要紧急修复

![img](images/win/git-flow/4.3.4git-flow-hotfix.png)

bug修复完毕后，在hotfix分支点击Git工作流后，出现如下提示

![img](images/win/git-flow/4.3.4git-flow-hotfix-end.png)

点击完成当前项目，会出现如下信息，需要给发布的补丁打`tag`同时默认删除`hotfix`分支

![img](images/win/git-flow/4.3.4git-flow-hotfix-check.png)

最后仓库的状态

![img](images/win/git-flow/4.3.4git-flow-all.png)

标准模式的Git flow会自动进行分支的新建删除，整个过程如下

![img](images/win/git-flow/4.3git-flow-all.png)



### 4.4 代码维护

- 操作建议：多人协作开发项目，每次推送代码前，都执行拉取操作
- 巧用贮藏：拉取失败不要紧张，三步走：1、贮藏本地代码，2、拉取更新，3、应用贮藏
- 解决冲突：当发现有若干文件有冲突时，一定不能盲目合并代码，请和产生冲突的代码推送人一起解决

#### 4.4.1 提交代码

将需要提交的代码加入`已暂存文件`，填写`提交信息`，点击提交即可

![img](images/win/4.4.1commit-code.png)


#### 4.4.2 贮藏代码

> 遇到无法推送的情况，git会提示需要先提交或者贮藏你的本地代码，这时候就用到了贮藏代码功能

可能会多次使用此功能，建议为每次操作都填写信息用于区分，可以勾选保留缓存的变更，那本地代码不会有变动，贮藏区域会把当前的变更保存，此选项默认是不勾选的

![img](images/win/4.4.2stash.png)

点击贮藏后，就恢复到了上一次提交，且`已贮藏`会显示保存的内容

> 特别说明：未加入版本管理的文件不会被贮藏


在`已贮藏`列表中选中需要应用的信息，右键，可以应用贮藏，会出弹窗确认此操作

![img](images/win/4.4.2stash-apply.png)


#### 4.4.3 遴选 cherry-pick

- 把需要的功能选中，然后`遴选`

![img](images/win/4.4.3cherry-pick.png)

- 顺利合上去了

![img](images/win/4.4.3cherry-pick-ok.png)

### 4.5 搜索

> 多维度搜素代码

![img](images/win/4.5search.png)



## 5 自动生成CHANGELOG

### 5.1 安装插件

```bash
npm install -g conventional-changelog-cli
cd my-project
conventional-changelog -p angular -i CHANGELOG.md -s
```

### 5.2 添加脚本

```package.json
"scripts": {
   "changelog": "conventional-changelog -p angular -i CHANGELOG.md -s -r 0"
 },
```

### 5.3 生成文件

```bash
npm run changelog
```


## 参考资料

- [git-book](https://git-scm.com/book/zh/v2)
- [Git Flow工作流程](https://www.jianshu.com/p/9a76e9aa9534)
- [Commit message 和 Change log 编写指南](http://www.ruanyifeng.com/blog/2016/01/commit_message_change_log.html)
- [conventional-changelog](https://github.com/conventional-changelog/conventional-changelog)

