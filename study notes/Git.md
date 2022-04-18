# Git

## Version control

**Version control** is an important function in git.  They have    Local version control, Integrated version control and Distributed Version Control.





## Git config

1. ```
   git config -l
   ```

2. ```
   git config --system --list
   ```

3. ```
   git config --global --list
   ```



## Git system config

directory:  **Git\etc\gitconfig**

## Git user config

directory: **C:\Users\\"user_name"\\.gitconfig**

**apply to the current user's config**   –global 



- configure user information 

``` 
git config --global user.name <user name>
git config --global user.email <email>
```

## Git principle



1. **WORKING DIRECTORY** ——>**STAGE(INDEX)**

```
git add <files>  // move the files into the stage 
```

2. **STAGE(INDEX)**——>**WORKING DIRECTORY**

```
git checkout  
```

3. **STAGE(INDEX)**——>**HISTORY(LOCAL REPOSITORY)**

```
git commit
```

argument:    **-m** :  add  comment

​					**-a** :   skip    `git add`  

4. **HISTORY(LOCAL REPOSITORY)**——>**STAGE(INDEX)**

```
git reset
```

5. **HISTORY(LOCAL REPOSITORY)**——>**REMOTE DIRECTORY**

```
git push
```

6. **REMOTE DIRECTORY**——>**HISTORY(LOCAL REPOSITORY)**

```
git pull
```

##    Git Local Repo initialization

1. Step 1:

- initialize the git local repository

```
git init
```

- clone a project form the remote repository

```
git clone "ssh key or URL "
```

2. Step 2:   display  file status

```  //
git status "file_name" // check specify file status
```

```
git status  // check all the files status in this directory
```

3. Step 3: create an `ssh key` (public key) 

```
ssh-keygen -t rsa -C "email" // "-t rsa"  is an encryption algorithm
```



## Git remote repository

- Add named  `origin` （This name could be called what you want.） remote repository.   添加远程版本库

```
git remote add origin git@github.com:Joynrui/project.git
```

```
git remote add [shortname] [url]    // shortname is the repository name.
```

- delete remote one of the repositories:

```
git remote rm name  # 删除远程仓库
```

- rename remote one of the repositories:

```
git remote rename old_name new_name  # 修改仓库名
```

## Download the remote host file

**git pull** 命令用于从远程获取代码并合并本地的版本。

**git pull** 其实就是 **git fetch** 和 **git merge FETCH_HEAD** 的简写。 命令格式如下：

```
git pull <远程主机名> <远程分支名>:<本地分支名>
```

example:

更新操作：

```
$ git pull
$ git pull origin
```

将远程主机 origin 的 master 分支拉取过来，与本地的 brantest 分支合并。

```
git pull origin master:brantest
```

如果远程分支是与当前分支合并，则冒号后面的部分可以省略。

```
git pull origin master
```

上面命令表示，取回 origin/master 分支，再与本地的 brantest 分支合并。



## Example of push process

```
$ mkdir runoob-git-test                     # 创建测试目录
$ cd runoob-git-test/                       # 进入测试目录
$ echo "# 菜鸟教程 Git 测试" >> README.md     # 创建 README.md 文件并写入内容
$ ls                                        # 查看目录下的文件
README
$ git init                                  # 初始化
$ git add README.md                         # 添加文件
$ git commit -m "添加 README.md 文件"        # 提交并备注信息
[master (root-commit) 0205aab] 添加 README.md 文件
 1 file changed, 1 insertion(+)
 create mode 100644 README.md

# 提交到 Github
$ git remote add origin git@github.com:tianqixin/runoob-git-test.git  //每次上传文件时，都需要重新配置远端主机地址,即库地址
$ git push -u origin main
```

关于 git push origin main  与 git push -u origin main 的区别 ：[link](https://www.jianshu.com/p/dd864fcee643)



## 强制本地与远端同步

```
      git fetch --all
      git reset  --hard origin/main 
      git pullx
```





## 提示Your branch is up-to-date with 'origin/master的解决方法

1、新建一个分支

git branch newBranch

2、检查分支是否创建成功

git branch

3、然后切换到新建的分支

git checkout newBranch

4、将改动提交到新分支

git add .
git commit -m "the new branch"


5、然后git status检查是否提交新分支成功


6、切回到主分支

git checkout master

7、新分支提交的改动合并到主分支

git merge newBranch



8、然后就可以push代码到远端仓库

git push -u origin master

如果不放心，在这里可以再git status检查下

9、删除新分支

git branch -D newBranch

Done，完美解决问题。

原文链接：https://blog.csdn.net/qq_33912215/article/details/89000254

## 关于因ssh 问题引发的无法提交文件的解决方法

Sometimes, firewalls refuse to allow SSH connections entirely. If using [HTTPS cloning with credential caching](https://docs.github.com/en/github/getting-started-with-github/caching-your-github-credentials-in-git) is not an option, you can attempt to clone using an SSH connection made over the HTTPS port. Most firewall rules should allow this, but proxy servers may interfere.

发现此问题的前提：ssh key 正常， 远端库密钥正常，本地公钥正常。 解决方法来源：[link](https://docs.github.com/en/authentication/troubleshooting-ssh/using-ssh-over-the-https-port)

报错信息：

```
git-ssh: connect to host github.com port 22: Connection timed out
```

解决方法：

1. 测试 443 端口链接是否可用：

```
ssh -T -p 443 git@ssh.github.com
```



2. 在本地.ssh 目录添加 config 文件  （文件名称为 `config`）

文件内容：

```
Host github.com
Hostname ssh.github.com
Port 443
```

3. 再次测试：

```
ssh -T git@github.com
```

测试通过后再尝试  push 即可成功上传。
