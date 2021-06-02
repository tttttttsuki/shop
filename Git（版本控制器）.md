## Git（版本控制器）

**注：可用于管理多人协同开发项目的技术。**

### 一、Git与SVN的区别

**Git**：分布式版本控制系统，没有中央服务器，每个人的电脑就是一个完整的版本库，方便多人协同开发项目。

**git是目前世界上最先进的分布式版本控制系统**

**SVN**：集中式版本控制系统，版本库是集中放在中央服务器的，而工作的时候，用的都是自己的电脑，所以首先要从中央服务器得到最新的版本，然后工作，完成工作后，需要把自己做完的活推送到中央服务器。

### 二、Git的历史

Linux 内核开源项目有着为数众广的参与者，绝大多数的 Linux 内核维护工作都花在了提交补丁和保存归档的繁琐事务上。到 2002 年，整个项目组开始启用一个专有的分布式版本控制系统 BitKeeper 来管理和维护代码。

到了 2005 年，开发 BitKeeper 的商业公司同 Linux 内核开源社区的合作关系结束，他们收回了 Linux 内核社区免费使用 BitKeeper 的权力。这就迫使 Linux 开源社区(特别是 Linux 的缔造者 Linus Torvalds)基于使用 BitKeeper 时的经验教训，开发出自己的版本系统 Git！

### 三、Git环境配置

#### 1.启动Git

Git Bash：Unix与Linux风格的命令行

Git CMD：Windows风格的命令行

#### 2.常用的Linux命令

1）cd：改变目录

2）cd..：回退到上一级目录

3）pwd：显示当前所在的目录路径

4）ls(ll)：列出当前目录中的所有文件

5）touch：新建文件

6）rm：删除文件

rm-r：删除一个文件夹 ，rm-r src：删除src目录

7）mkdir：新建目录

8）mv：移动文件

9）reset：重新初始化终端/清屏

10）clear：清屏

11）history：查看命令历史

12）help：帮助

13）exit：退出

#### 3.Git配置

1）查看配置 git config-l

2）查看系统config

git config --system --list

3）查看当前用户配置

git config --global --list

### 四、Git的使用

#### 1.三个区域

Git本地有三个工作区域：工作区（Working Directory）、暂存区(Stage/Index)、仓库(Repository或Git Directory)。如果在加上远程的git仓库(Remote Directory)就可以分为四个工作区域。如下图所示：

![1](https://gitee.com/ttttsuki/bloglmage/raw/master/img/20210601215429.png)

#### 2.本地仓库操作

##### 1）设置用户名与邮箱

git config --global user.name "名称"

git config --global user.email "邮箱"

##### 2）创建仓库

- 创建目录![2](https://gitee.com/ttttsuki/bloglmage/raw/master/img/20210601215430.png)

- 在命令行中进入目录

![3](https://gitee.com/ttttsuki/bloglmage/raw/master/img/20210601215431.png)

- Git仓库初始化

  ![4](https://gitee.com/ttttsuki/bloglmage/raw/master/img/20210601215432.png)
  
  **执行之后会在项目目录下创建“.git”的隐藏目录**
  
  ![5](https://gitee.com/ttttsuki/bloglmage/raw/master/img/20210601215433.png)

##### 3）Git常用指令操作

- 查看当前状态：git status 
- 添加到缓存区：git add 文件名
- 提交至版本库：git commit -m “注释内容”

#### 3.远程仓库操作

![6](https://gitee.com/ttttsuki/bloglmage/raw/master/img/20210601215434.png)

#### 4.两种常规使用方式

##### 1）基于http/https协议

-  创建空目录
-  使用clone指令克隆线上仓库到本地
  **git clone 线上仓库地址**

![7](https://gitee.com/ttttsuki/bloglmage/raw/master/img/20210601215435.png)

-  在仓库上做对应的操作（git add、git commit、git push等）

**提交到线上仓库的指令：git push**

**拉取线上仓库：git pull**

在首次往线上仓库shop提交内容的时候（git push）时可能会出错，这是因为不是任何人都可以往线上仓库提交内容，必须需鉴权。

**需要修改“.git/config”文件内容：**

[remote "origin"]

​	url=https://github.com/用户名/仓库.git

修改为：

[remote "origin"]

​	url=https://*用户名:密码@*github.com/用户名/仓库.git

##### 2）基于ssh协议

**注：需要生成公私钥对指令**

- 生成公钥

  ssh-keygen -t rsa -C "注册邮箱"
  
  ![10](https://gitee.com/ttttsuki/bloglmage/raw/master/img/20210601215436.jpg)


- 上传公钥文件内容

![8](https://gitee.com/ttttsuki/bloglmage/raw/master/img/20210601215437.png)


- 在仓库上做对应的操作（git add、git commit、git push等）

#### 5.版本回退操作

版本回退分为两步：

1）查看版本，确定需要回到的时刻点

指令：

git log

git log --pretty=oneline

2）回退操作

指令：

git reset --hard 版本号

注：回退之后，又想回到之前最新版本的时候怎么办？

- 先使用指令：git reflog 查询之前的编号
- 再执行指令：git reset --hard 版本号

#### 6.分支操作

##### 1.分支是什么？

分支就是从主线上分离出来进行另外的操作，而又不影响主线，主线又可以继续干它的事，最后分支做完事后合并到主线上而分支的任务完成可以删掉了。（在开发的时候往往是团队协作，多人进行开发，因此光有一个分支是无法满足多人同时开发的需求的，并且在分支上工作并不影响其他分支的正常使用，会更加安全）

##### 2.分支相关指令

查看分支：git branch
创建分支：git branch 分支名
切换分支：git checkout 分支名 
删除分支：git branch -d 分支名
合并分支：git merge 被合并的分支名

#### 7.冲突问题

**案例：模拟冲突**
我下班之后，同事对线上项目内容进行了修改，此时本地仓库的内容与线上仓库内容不一致，第二天我忘记做git pull操作，而是直接对本地文件进行修改。当进行提交时，会报错。

**如何解决冲突？**

- 先git pull将线上与本地仓库的冲突合并到了对应的文件中
- 需要和同事（谁先提交的）进行商量，看代码如何保留，将改好的文件再次提交即可





