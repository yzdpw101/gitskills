### 一、安装及初始化Git

#### 1.在Git官网下载适合操作系统的安装包并安装Git

Git官方下载链接：[Git - Downloads](https://git-scm.com/downloads)

Git安装教程：[[2024]Windows系统Git详细图文安装教程](https://blog.csdn.net/2301_76884890/article/details/141158307)

#### 2.安装完成后打开Git Bash，初始化Git

输入以下两行代码，其中Your Name和Email Address分别为你的姓名和邮箱地址：

```shell
git config --global user.name "Your Name"

git config --global user.email "Email Address"
```



### 二、初始化仓库仓库（Repository）

#### 1.改变当前工作目录

```shell
cd E:/Project/MyProjects
```

#### 2.在当前工作目录下创建文件目录：

```shell
mkdir LearnGit
```

#### 2.移动至工作目录

```shell
cd LearnGit
```

#### 3.查看当前工作目录

```shell
pwd
```

#### 4.显示当前目录下的所有文件

```shell
ls
```

#### 5.初始化仓库（Repository）

```shell
git init
```

这是创建了一个空的仓库，目录下多了一个隐藏的.git目录，这个目录是用来给Git跟踪管理代码版本库的，最好不要手动修改。`ls -ah`可以显示这个隐藏的目录。



### 三、添加、提交文件给Git仓库

#### 1.创建一个文件

```shell
touch readme.txt
```

#### 2.使用vi文本编辑器编辑文本

```shell
vi readme.txt
```

打开`vi`后，进入文本编辑前的命令模式。

![使用vi文本编辑器打开文本](C:\Users\Tel13\AppData\Roaming\Typora\typora-user-images\image-20240928160122529.png)

按`i`键进入编辑模式。输入要编辑的内容，编辑完成后按`ESC`键退出编辑模式到命令模式。

![编辑模式，下方底线显示INSERT](C:\Users\Tel13\AppData\Roaming\Typora\typora-user-images\image-20240928160807904.png)

输入`:wq`后按回车可以保存并关闭`vi`文本编辑器

![在底线下方输入:wq](C:\Users\Tel13\AppData\Roaming\Typora\typora-user-images\image-20240928160824330.png)

#### 3.把文件添加到仓库（提交前的打包，可以在提交前添加好几个文件）

```shell
git add readme.txt
```

#### 4.将添加的一个或多个文件提交给仓库，并输入此次提交的说明（版本说明）

```shell
git commit -m "write a readme file"
```

提交命令成功后的的返回信息：

![提交命令成功后的的返回信息：](C:\Users\Tel13\AppData\Roaming\Typora\typora-user-images\image-20240928162159082.png)

#### 5.查看仓库当前状态

```shell
git status
```

#### 6.查看文件变化

```shell
git diff readme.txt
```



### 四、版本回退

#### 1.查看命令历史记录

```shell
git log
```

如果嫌输出信息太多可以添加`--pretty=oneline`参数让他每条改动以一行输出。

```shell
git log --pretty=oneline
```

注意：`HEAD`表示当前版本，`commit`后面一长串表示版本号。

#### 2.回退版本

```shell
git reset --hard HEAD^
```

`HEAD^`表示上一个版本，`HEAD^^`表示上上个版本，依次类推。上n个版本写成`HEAD~n`，也可以使用指定版本号回退或者恢复。

`--hard`：工作区和暂存区均回到指定版本的已提交状态，HEAD指向指定版本号；

`--soft`：暂存区和工作区均保持不变，HEAD指向指定版本号；

`--mixed`：暂存区回到指定版本的已提交状态，工作区保持不变，回到已添加但未提交状态。

实际上版本的修改主要针对的就是工作区的文件。

注意：如果回退到了上一个版本，那么在使用`git log`查看命令记录就会发现后面的记录丢失了，这时候想回去就要使用版本号恢复。

#### 3.查看内容文本内容

```shell
cat readme.txt
```

#### 4.查寻所有改动下的命令

```shell
git reflog
```

使用这条命令看到回退后`git log`命令查询不到的命令了，这时可以使用版本号回退了。



### 五、工作区和暂存区

#### 1.工作区（Working Directory）

电脑里能看到的目录，比如`LearnGit`文件夹就是一个工作区。

#### 2.版本库

工作区内隐藏的`.git`目录就是版本库，版本库内有暂存区（`stage`或者叫`index`）、第一个分支`main`以及指向`main`的指针`HEAD`（一般主分支`main`不修改的情况下默认叫`master`）。

所以我们使用`git add`命令是把文件修改添加到暂存区，`git commit`是提交修改，把暂存区的内容提交到当前分支下，这时工作区与暂存区的内容都会被记录下来。

#### 3.把文件在工作区的修改全部撤销，恢复到上一次提交后的状态

```shell
git checkout -- readme.txt
```

#### 4.把文件从暂存区移动到工作区，但不撤销对文件的修改

```shell
git reset HEAD readme.txt
```



### 六、删除文件

#### 1.删除工作区或者任意目录下的文件或者目录（不在git目录下也可以用）

```shell
rm to_be_deleted_file_catalogue
```

工作区内的文件如果删错了，还可以通过`git`语句恢复。

#### 2.从版本库中删除文件或者目录

```shell
git rm to_be_deleted_file_or_catalogue
```



### 七、远程仓库

#### 1.创建SSH Key

打开`Git Bash`，创建`SSH Key`：

```shell
ssh-keygen -t rsa -C "yzdpw@njust.edu.cn"
```

之后一路回车使用默认配置就好

#### 2.登陆注册GitHub

[GitHub](https://github.com/)

#### 3.在GitHub中添加SSH Key

登录`GitHub`，点击`Account seetings` -> `SSH and GPG Keys` -> `New SSH Key`

![image-20240930201256115](C:\Users\Tel13\AppData\Roaming\Typora\typora-user-images\image-20240930201256115.png)

之后在`Add new SSH Key`项下填写密钥信息，标题随便填写，在用户主目录下寻找到`.ssh`文件夹下的i`d_rsa.pub`并用记事本打开后复制全部内容到`Key`栏中，然后点击`Add SSH key`。

![image-20240930201845361](C:\Users\Tel13\AppData\Roaming\Typora\typora-user-images\image-20240930201845361.png)

重新打开一个`Git Bash`窗口，输入`pwd`命令后回车即可看到`Git`主目录了。

![image-20240930202101970](C:\Users\Tel13\AppData\Roaming\Typora\typora-user-images\image-20240930202101970.png)

#### 4.在GitHub创建仓库

在主界面点击`Create repository`。

![image-20240930202424890](C:\Users\Tel13\AppData\Roaming\Typora\typora-user-images\image-20240930202424890.png)

在`Create repository`界面，仅需要输入`Repository name`，其他使用默认设置就好，在最下方点击`Create repository`。

![image-20240930202817270](C:\Users\Tel13\AppData\Roaming\Typora\typora-user-images\image-20240930202817270.png)

![image-20240930202839221](C:\Users\Tel13\AppData\Roaming\Typora\typora-user-images\image-20240930202839221.png)

#### 5.将本地仓库与远程仓库关联

执行这个命令后，本地仓库就会和 `GitHub` 上的 `RepositoryName` 仓库关联起来，其中`YourName`是你远程仓库的用户名，`origin`是远程库的别名可以修改，`git@github.com:YourName/RepositoryName.git`其实是地址，可以使用其他的协议写。在上传之前需要使用`cd`命令移动到你的仓库目录下。

```shell
git remote add origin git@github.com:YourName/RepositoryName.git
```

#### 6.推送导入本地库的所有内容到远程库上

```shell
git push -u origin main
```

实际上`git push`是把当前分支`main`推送到远程。

关于`-u`参数，`Git`不但会把本地的`main`分支内容推送到远程的新的`main`分支，还会把这两个分支关联起来，在以后的推送或者拉取时就可以简化命令。

推送成功后就可以在`GitHub`页面中看到远程库的内容已经和本地的一模一样了。

![image-20240930214434636](C:\Users\Tel13\AppData\Roaming\Typora\typora-user-images\image-20240930214434636.png)

#### 7.推送

```shell
git push origin main
```

#### 8.查看远程库信息

```shell
git remote -v
```

#### 9.删除远程库（解除本地库和远程库的绑定）

```shell
git remote rm origin
```

其实这里的删除只是解除了本地和远程的绑定关系，并不是物理上的删除。删除远程库需要在GitHub里操作。

#### 10.克隆库

```shell
git clone git@github.com:YourName/RepositoryName.git
```



### 八、分支管理

#### 1.创建分支

```shell
git checkout -b dev
```

其中`dev`是指要创建的分支名，`-b`参数是指创建`dev`分支并转到该分支下。

#### 2.查看当前分支

```shell
git branch
```

#### 3.安全删除分支（分支若有未合并的部分则会拒绝删除）

```shell
git branch -d dev
```

#### 4.强制删除分支（分支即使有未合并的部分也会删除）

```shell
git branch -D dev
```

#### 5.切换分支（同时创建）

```shell
git switch -c dev
```

其中`dev`是要创建的分支名，`-c`参数是`--create`的缩写，是指创建分支并切换到该分支上。

若要切换分支，去掉`-c`参数就好了。这条这令比`git checkout`更好理解，推荐用这个。

#### 6.修改上一次的提交

```shell
git commit --amend
```

该命令会直接进入编辑器内以修改上一次的提交。

#### 7.合并分支

```shell
git merge dev
```

如果顺利合并，默认使用的是`Fast forward`（`ff`）模式合并的，这样合并的坏处是在删除分支后分支的信息会完全丢失。如果合成出现冲突，需要自己手动修改冲突的部分。分支路线如图所示：

![image-20241008135557843](C:\Users\Tel13\AppData\Roaming\Typora\typora-user-images\image-20241008135557843.png)

main

```shell
git merge --no-ff -m 'merge with no-ff' dev
```

上面是强制禁用ff模式的合并命令。其中`--no-ff`参数是指禁用`Fast forward`合并模式，由于要创建新的`commit`，所以就要用上`-m`参数，引号里的`merge with no-ff`是此次合并的提交信息，可以修改为实际的内容。

![image-20241008134909985](C:\Users\Tel13\AppData\Roaming\Typora\typora-user-images\image-20241008134909985.png)

#### 8.分支策略

**首先，main分支应该非常稳定，仅用来发布新版本，平时不能再上面干活；**

平时都在`dev`分支上面干活，到版本发布的时候把`dev`分支合并到`main`分支啥分支上，在`main`分支上发布新版本；

你和小伙伴平时都在`dev`分支上干活，每个人都有自己的分支，往`dev`分支上合并就好了；

所以团队合作的分支看起来就像这样：

![image-20241008134502461](C:\Users\Tel13\AppData\Roaming\Typora\typora-user-images\image-20241008134502461.png)

#### 9.暂时保存当前工作进度

```shell
git stash
```

查看已保存的`stash`：

```shell
git stash list
```

恢复`stash`但不删除之：

```shell
git stash apply
```

删除`stash`：

```shell
git stash drop
```

恢复`stash`并删除之：

```shell
git stash pop
```

#### 10.多人协作

**其中main是主分支，需要时刻与远程同步；**

**dev分支是开发分支，团队所有成员都在上面工作，也需要远程同步；**

`bug`分支只用于在本地修复`bug`，没必要推送到远程；

`feature`分支是否要推到远程，取决于你是否和小伙伴在上面合作开发。

#### 11.从远程仓库拉取更新并合并到当前分支

```shell
git pull
```

如果报错以下信息则说明未设置与远程分支的追踪关系：

```
There is no tracking information for the current branch.
Please specify which branch you want to merge with.
```

使用以下命令可以设置当前分支与远程分支的追踪关系：

```shell
git branch --set-upstream-to=origin/dev dev
```

若要从临时指定远程分支进行`git pull`：

```shell
git pull origin main
```

如果合并有冲突，则解决冲突，手动修改冲突部分。

#### 12.变基（并合并）

```shell
git rebase origin main
```

该指令会将提交历史线性化，即仅显示从dev分支下出来的分支路线，如果main分支有改动那么会将其合并，之后处理冲突即可。

`git rebase` 是 Git 中用来合并分支历史的一个命令，通常用来清理历史记录、保持线性历史或者把一个分支的提交应用到另一个分支上。

**rebase 只在本地开发时使用**。不要对已经推送到共享仓库的公共分支使用 rebase，除非所有人都同意。



### 九、标签

#### 1.创建标签

```shell
git tag v1.0
```

在使用上述命令之前需要先切换到分支下

#### 2.查看所有标签

```shell
git tag
```

#### 3.指定提交号打标签

```shell
git tag v0.9 xxxxxxx
```

提交号可以使用`git log --pretty=oneline --abbrev-commit`（这是简洁模式，直接输入`git log`也可以）命令查看

#### 4.查看标签信息

```shell
git show <tagname>
```

#### 5.创建带有说明的标签

```shell
git tag -a v0.1 -m 'version 0.1 released' xxxxxxx
```

其中用参数`-a`指定标签名，用`-m`参数指定说明文字。

#### 6.删除标签

```shell
git tag -d v0.1
```

#### 7.推送标签到远程仓库

```shell
git push origin v1.0
```

或者一次性推送所有尚未推送到远程的本地标签

```shell
git push origin --tags
```

#### 8.删除远程标签

先要删除本地标签：

```shell
git tag -d v0.9
```

然后从远程删除，删除命令也是`push`：

```shell
git push origin :refs/tags/v0.9
```



### 十、使用GitHub和Gitee

#### 1.克隆开源项目

先要访问项目主页，然后点击Fork克隆该项目到自己账号下，接着从自己的账号下克隆：

```shell
git clone git@github.com:YourName/RepositoryName.git
```

#### 2.pull request

如果你希望开源方的官方库能接受你的修改，你就可以在GitHub上发起一个pull request。当然，对方是否接受你的pull request就不一定了。

#### 3.让仓库同时和关联GitHub和Gitee

先删除原来和GitHub关联的仓库：

```shell
git remote rm origin
```

然后重新分别关联GitHub和Gitee并取不一样的仓库别名：

```shell
git remote add github git@github.com:YourName/RepositoryName.git
```

```shell
git remote add gitee git@gitee.com:YourName/RepositoryName.git
```

查看远程库信息我们可以用这条语句：

```shell
git remote -v
```

如果要推送更新（在推送之前，Gitee需要先添加本地的SSH公钥，远程仓库的3有讲过类似的操作）：

```shell
git push github main
```

```shell
git push gitee main
```



### 十一、自定义Git

#### 1.让Git Bash显示颜色，让命令输出输出起来更显目：

```shell
git config --global color.ui true
```

#### 2.忽略特殊文件

在仓库目录下新建一个`.gitignore`文件（子目录下也可以）：

![image-20241009105757009](C:\Users\Tel13\AppData\Roaming\Typora\typora-user-images\image-20241009105757009.png)

关于语法，#是注释，在`.gitignore`文件内编写需要忽略的文件或者同后缀名文件或者文件夹，比如：

```
# Windows:
Thumbs.db
ehthumbs.db
Desktop.ini

# Python:
*.py[cod]
*.so
*.egg
*.egg-info
dist
build

# My configurations:
db.ini
deploy_key_rsa
```

如果想强制添加被`.gitignore`文件忽略的文件或者目录，可以使用：

```shell
git add -f App.class
```

检查要添加的文件与`.gitignore`冲突的部分：

```shell
git check-ignore -v App.class
```

但是我们发现`.gitignore`内的.*规则把`.gitignore`本身也忽略了，这时候就可以在`.gitignore`文件内添加新的规则：

```
# 不排除.gitignore和App.class:
!.gitignore
!App.class
```

#### 3.给命令配置别名

```shell
git config --global alias.st status
```

上面的语句就是给`status`取别名为`st`，而且是全局适用，如果不想全局设置那么可以添加  `--global`参数

还有几条语句常用于以下简写：

```shell
git config --global alias.co checkout
git config --global alias.ci commit
git config --global alias.br branch
git config --global alias.unstage 'reset HEAD'
git config --global alias.last 'log -1'
```

查看/编辑的配置文件：

```shell
cat .git/config
```

上面的命令是查看该仓库的配置信息

而要查看用户的Git配置信息，就需要在用户主目录下找到隐藏文件.`gitconfig`文件，比如我的`.gitconfig`文件在这里：

![image-20241009112507729](C:\Users\Tel13\AppData\Roaming\Typora\typora-user-images\image-20241009112507729.png)

#### 4.搭建Git服务器

搭建`Git`服务器需要准备一台运行`Linux`的机器，强烈推荐用`Ubuntu`或`Debian`，这样，通过几条简单的`apt`命令就可以完成安装。

假设你已经有`sudo`权限的用户账号，下面，正式开始安装。

**第一步**，安装`git`：

```shell
sudo apt install git
```

**第二步**，创建一个`git`用户，用来运行`git`服务：

```shell
sudo adduser git
```

**第三步**，创建证书登录：

收集所有需要登录的用户的公钥，就是他们自己的`id_rsa.pub`文件，把所有公钥导入到`/home/git/.ssh/authorized_keys`文件里，一行一个。

**第四步**，初始化`Git`仓库：

先选定一个目录作为`Git`仓库，假定是`/srv/sample.git`，在`/srv`目录下输入命令：

```shell
sudo git init --bare sample.git
```

`Git`就会创建一个裸仓库，裸仓库没有工作区，因为服务器上的`Git`仓库纯粹是为了共享，所以不让用户直接登录到服务器上去改工作区，并且服务器上的`Git`仓库通常都以`.git`结尾。然后，把`owner`改为`git`：

```shell
sudo chown -R git:git sample.git
```

**第五步**，禁用shell登录：

出于安全考虑，第二步创建的git用户不允许登录shell，这可以通过编辑`/etc/passwd`文件完成。找到类似下面的一行：

```shell
git:x:1001:1001:,,,:/home/git:/bin/bash
```

改为：

```shell
git:x:1001:1001:,,,:/home/git:/usr/bin/git-shell
```

这样，`git`用户可以正常通过`ssh`使用`git`，但无法登录`shell`，因为我们为`git`用户指定的`git-shell`每次一登录就自动退出。

**第六步**，克隆远程仓库：

现在，可以通过`git clone`命令克隆远程仓库了，在各自的电脑上运行：

```shell
git clone git@server:/srv/sample.git
```

**管理公钥**

如果团队很小，把每个人的公钥收集起来放到服务器的`/home/git/.ssh/authorized_keys`文件里就是可行的。如果团队有几百号人，就没法这么玩了，这时，可以用[Gitosis](https://github.com/res0nat0r/gitosis)来管理公钥。

**管理权限**

`Git`支持钩子（`hook`），可以在服务器端编写一系列脚本来控制提交等操作，达到权限控制的目的。[Gitolite](https://github.com/sitaramc/gitolite)就是这个工具。



### 十二、SourceTree

#### 1.从官网下载安装SourceTree

[SourceTree官网](https://www.sourcetreeapp.com/)

[SourceTree安装教程](https://blog.csdn.net/zqd_java/article/details/123681302)

#### 2.在SourceTree中打开Git库目录（也可以直接把目录拖进应用里）

![image-20241009144923876](C:\Users\Tel13\AppData\Roaming\Typora\typora-user-images\image-20241009144923876.png)

打开后的状态：

![image-20241009145042930](C:\Users\Tel13\AppData\Roaming\Typora\typora-user-images\image-20241009145042930.png)

#### 3.提交

在左侧面板点击`WORKSPACE`->`File status`，右侧就会列出当前已修改的文件；

当选中某个文件，并点击右边的`+`就可以将该文件添加到暂存区（实际上是执行了              `git add README.md`命令）：

![image-20241009151303424](C:\Users\Tel13\AppData\Roaming\Typora\typora-user-images\image-20241009151303424.png)

![image-20241009151318265](C:\Users\Tel13\AppData\Roaming\Typora\typora-user-images\image-20241009151318265.png)

然后我们在下方输入`Commit`描述，点击提交就可以完成一次本地提交了（实际上是执行了`git commit -m Use SourceTree to commit`命令）：

![image-20241009151722821](C:\Users\Tel13\AppData\Roaming\Typora\typora-user-images\image-20241009151722821.png)

#### 4.分支

点击左侧面板的`BRANCHES`，可以查看任意分支提交记录。

如果要合并分支可以选择其他分支右键点击`Merge dev into master`，实际上是执行了   `git merge dev`。

#### 5.推送

在`SourceTree`的工具栏上还有`Pull`和`Push`，分别对应命令`git pull`和`git push`，只需要注意本地和远程分支的名称要对应起来，使用很方便。

#### 6.注意

SourceTree本身是通过Git命令来完成的，如果操作失败我们可以通过Git返回的错误信息知道出错的原因。
