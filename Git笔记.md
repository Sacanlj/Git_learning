

# Git笔记

## 一、Git文件的三种状态与工作模式

ps:

本地仓库：理解成自己的电脑。

| 状态              |                             描述                             |
| ----------------- | :----------------------------------------------------------: |
| 已提交(committed) |         已提交表示数据已经安全的保存在本地数据库中。         |
| 已修改(modified)  |      已修改表示修改了文件，但还没有保存到本地数据库中。      |
| 已暂存(staged)    | 已暂存表示对一个已修改文件的当前版本做了标记，使之包含在下次提交的工作快照中。 |

工作流程：

![](C:\Users\asus\Desktop\屏幕截图 2021-07-07 210916.jpg)

## 二、创建本地库并提交



![image-20210707211752605](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20210707211752605.png)**创建一个工作目录，编写一个文件，并且提交到本地git仓库**

### **·工作目录**

![image-20210707212914012](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20210707212914012.png)



### **·初始化git本地仓库**

通过执行`git init`命令在本地初始化一个仓库。执行该命令后会在**本地**初始化一个没有任何文件的空仓库。



![image-20210707212934325](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20210707212934325.png)

![image-20210707213156134](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20210707213156134.png)

![image-20210707213216397](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20210707213216397.png)



### **·将要提交的文件推送到暂存区**

在.git同级目录下添加文件后，使用`git status`命令可以查看工作目录与暂存区的状态。

再执行`git add <path>`将文件推送到暂存区。

![image-20210707213311746](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20210707213311746.png)

![image-20210707213352749](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20210707213352749.png)

(因为还没有git add所以是未追踪的)

使用git add追踪（推送到暂存区）后：

![image-20210707213605742](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20210707213605742.png)

### **·提交文件到本地仓库**

![image-20210707213708690](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20210707213708690.png)

通过`git commited -m '本次提交注释'`命令可以将暂存区内容提交到本地仓库。

![image-20210707213739451](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20210707213739451.png)

提交后，暂存区没有东西了。

![image-20210707213812858](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20210707213812858.png)

`git log`命令可以查看提交日志信息

## 三、文件修改和提交

### **1.修改刚刚工作目录中的文件**

再查看工作目录和暂存区状态：

![image-20210707214048587](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20210707214048587.png)

**显示文件已修改(modified)，但是还未保存到暂存区。**

### **2.推送到暂存区**

可以用`git add .`命令**提交当前工作目录下的全部文件**

![image-20210707214321315](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20210707214321315.png)

`git add .`中的.可以用绝对路径代替。上图下划线就是当前工作目录的绝对路径。

![image-20210707214426508](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20210707214426508.png)

### **3.提交**

使用`git commit`当不使用 `-m '注释'`的时候，会进入下图的vim编辑界面，编辑注释内容。

![image-20210707214600405](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20210707214600405.png)

![image-20210707214713889](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20210707214713889.png)

保存退出后就提交了。

![image-20210707214753819](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20210707214753819.png)

### 4.修改后未提交或者提交不成功时查看本地库和工作目录下文件的差别

使用 `git diff HEAD -- <path>`  命令可以将工作目录文件与本地库（版本库）进行对比。

![image-20210707234453162](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20210707234453162.png)

--- 表示变动之前的（本地库中的）

+++ 表示变动之后的（当前工作目录下的）

-1,2表示变动之前（本地库中）从1行到2行。

+1,3表示变动之后（目录中的）从1行到3行。

第三行的 ”+第三次提交“ 就是变动之后（工作目录中的新内容）。

### 5.推送到暂存区后的撤回——法1

**有时候会误操作把文件推送到了暂存区，这时可以撤回。所以规范操作时add之后status看看检查一下，在提交。**

先把刚刚的提交了

![image-20210707235125559](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20210707235125559.png)

（可以发现，提交后再查看diff发现没有显示这说明本地库和目录下的文件没有差别）

新建一个文件：

![image-20210707235408901](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20210707235408901.png)

![image-20210707235500689](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20210707235500689.png)

发现git02.txt误推送到暂存区了

使用命令 `git restore --staged <文件名>`将该文件撤销

![image-20210707235811674](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20210707235811674.png)

可见重新变回了未追踪（未add）状态。

### 6.推送到暂存区后的撤回——法2

![image-20210708000135941](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20210708000135941.png)

使用`git reset HEAD`命令。

![image-20210708000208333](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20210708000208333.png)

#### 区别：

​	<1> `git restore --staged <文件名>` 是只能撤销暂存区的文件，且可以追加，即文件名可以写多个，然后用这一个命令撤销多个。

​	<2> `git reset HEAD` 是指撤回上一次操作，即就算git commit了也能撤回。

## 四、时光穿梭机（版本回退）

意义：类似于游戏存档，当多次修改和提交后，可以回退到某个版本，以便于检查BUG等作用。Git提供的这个功能可以使我们在各个版本间任意穿梭，形象的说成时光穿梭机。

### 1.查看全部版本记录

`git log` 命令可以查看版本记录（提交记录）

![image-20210708001104639](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20210708001104639.png)

可见总共提交了三次。

我们再多提交几次：

这里可以用 `git commit --am '注释'`命令来快速提交。

即 -am就是add . 的缩写，可以把目录下所有文件 add了然后再提交。

![image-20210708001523704](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20210708001523704.png)

再查看：

![image-20210708001615876](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20210708001615876.png)

可见这样查看的内容太多了，可以使用命令：`git  log --pretty=oneline`来简化查看：

![image-20210708001901476](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20210708001901476.png)

每一行的开头一大串代码，就是每次提交的唯一ID。

后面白字就是提交的备注，注释内容。

**看第一行的  (HEAD -> master) 是指向最后一次（最近一次）提交**

**所以版本间穿梭，就是用HEAD指针指向不同的版本。**

### 2.版本回退（穿梭）

使用HEAD指针

#### 法1：git reset --hard HEAD^

其中一个^表示回退一个版本。

当前版本：

![image-20210708003751686](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20210708003751686.png)

回退两个：

`git reset --hard HEAD^^`

![image-20210708003920604](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20210708003920604.png)

![image-20210708003938270](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20210708003938270.png)

#### 法2：git reset --hard HEAD~x

其中~X（~是波浪号）表示回退X个版本。

![image-20210708004045520](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20210708004045520.png)

回退两个：git reset --hard HEAD~2

![image-20210708004202923](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20210708004202923.png)

![image-20210708004217394](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20210708004217394.png)

#### 法3：`git --hard <部分提交唯一ID>`

**此法就可以穿梭到任意版本**

![image-20210708004410227](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20210708004410227.png)

穿梭回最后一次提交：

`git reset --hard cc901d00`

![image-20210708004537619](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20210708004537619.png)

![image-20210708004622152](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20210708004622152.png)

PS：有时候退出了Git Bash窗口或再打开会导致提交记录不全以至于找不到唯一ID号

这时可以用 `git reflog` 命令查看所有提交记录。

![image-20210708004851931](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20210708004851931.png)

就可以查看到全部的ID号了。

## 五、文件删除

**其实，Git认为，文件的增加，插入内容，删除都是文件的修改操作。**

### 1.法1：工作目录删除后再提交

先直接在工作目录下删除了：

![image-20210708005633218](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20210708005633218.png)

但此时我们的本地库中还有刚刚被删除的文件：

命令 ： `git ls-files`

![image-20210708005940530](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20210708005940530.png)

仍然还可以从本地库中拉取新版本到当前工作目录下：

命令：git checkout <文件名>

![image-20210708010513223](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20210708010513223.png)

![image-20210708010526329](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20210708010526329.png)

因为此时我们在工作目录的操作仍然算作一次文件的修改操作，我们可一通过git status看到：

![image-20210708010104521](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20210708010104521.png)

本次文件的删除修改操作，未被追踪到。

这时可以通过正常的提交，将本次操作提交，最后真正的在工作目录和本地仓库中同时删除。

先 `git add learning.txt` 

![image-20210708010827600](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20210708010827600.png)

再提交：

![image-20210708010935991](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20210708010935991.png)

成功删除。

### 2.法2：直接在本地仓库删除，此时可以连同工作目录中的一起删除。

先回退到删除之前：

![image-20210708011149640](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20210708011149640.png)

然后命令： `git rm <文件名>`

![image-20210708011329921](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20210708011329921.png)

![image-20210708011409674](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20210708011409674.png)

本地库和工作目录下都删除了。

## 六、远程仓库——Github使用

Git是一个分布式的版本控制系统。同一个Git仓库(本地仓库)，可以分布到不同的机器上(服务器)。即可以把本地版本推送到远程仓库进行存储，也可以从远程仓库下载到本地，极大的方便开发。

Github(https://github.com/访问慢可以使用镜像站(https://github.com.cnpmjs.org/)就是一个比较有名的远程仓库。

国内的比较出名的有码云(https://gitee.com/)

注意，上面两个是开源的代码托管平台。一般公司内是自己搭建，以便保密。

### 6.1 从远程仓库下载代码到本地库

#### 1. 法1：访问Github下载。

![image-20210708142153851](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20210708142153851.png)

![image-20210708142229542](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20210708142229542.png)

#### 2.法2：使用Git通过命令拉取下载。

复制项目的地址：

![image-20210708142532950](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20210708142532950.png)

Git Bash拉取：

命令： `git clone <项目地址>`

![image-20210708142658656](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20210708142658656.png)

![image-20210708142729937](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20210708142729937.png)

![image-20210708142749838](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20210708142749838.png)

OK.

### 6.2 SSH下载项目

为什么使用SSH下载？因为采用SSH下载效率会更高，而且更安全。

#### 1.生成public SSH keys

需要key：

![image-20210708143400251](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20210708143400251.png)

使用本地Git端生成SSH公钥与私钥，

使用命令：`ssh-keygen -t rsa -C "Github账户邮箱"`

![image-20210708143850701](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20210708143850701.png)

![image-20210708143955574](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20210708143955574.png)

一直回车就好，我这里之前已经生成过了，在上面写着的那个文件夹里。找一下：

![image-20210708160904176](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20210708160904176.png)

id_rsa是私钥，id_rsa.pub是公钥。

我们现在要用公钥：

![image-20210708161053056](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20210708161053056.png)

全部拷贝下来，然后会Github添加SSH钥匙：

![image-20210708161208170](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20210708161208170.png)

或者：

![image-20210708161233833](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20210708161233833.png)

![image-20210708161413397](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20210708161413397.png)

![image-20210708161648980](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20210708161648980.png)

主义赋值key时，多了一个换行，删掉。

![image-20210708162107569](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20210708162107569.png)

检查：

![image-20210708162417731](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20210708162417731.png)

命令： `ssh -T git@github.com`

成功，ssh已经绑定了github。

#### 2.通过SSH安全快速的下载。

![image-20210708163024659](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20210708163024659.png)

复制下来ssh地址：

命令 ： `git clone <ssh地址>`

![image-20210708163200648](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20210708163200648.png)

![image-20210708163250412](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20210708163250412.png)

OK。

#### 6.3推送到远程仓库

以原来的仓库为例，即把git_learning仓库推送到远程仓库。

##### 1.本地仓库

![image-20210708164654960](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20210708164654960.png)

![image-20210708164851171](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20210708164851171.png)

##### 2.创建一个远程仓库

![image-20210708165020634](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20210708165020634.png)

![image-20210708165428982](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20210708165428982.png)

README就是一个介绍该仓库项目的文件。

Choose a license是用来选择许可证的，许可证的作用是：比如，区别该项目是开源的，你可以下载去自己玩一玩，改一改，但不可以发布。或者是开源的然后还可以自己改甚至可以二次改造发布。

**推送：**

首先要

`git init`初始化一个本地库（这里最一开始就弄好了，不重复了。）

`git add READM.md`

`git add`

`git commit -m`  	提交

`git branch -M master`     移动到主分支

`git remote add origin git@github.com:Sacanlj/git_learning.git`（使用SSH方式）

![image-20210708203242186](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20210708203242186.png)

已经连接到了远程。

`git push -u origin master` 推送到远程





