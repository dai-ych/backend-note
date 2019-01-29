
### 一、新建本地仓库及初始化
- $ git config --global user.name `[UserName]`            ---设置用户名  
- $ git config --global user.email `[Emailaddress]`       ---设置邮箱信息  
- $ ssh-keygen -t rsa -C "55270072@qq.com"                 ---生成SSH加密密钥，提示信息直接回车，使用默认值。  
- $ pwd                                                    ---查看当前路径
- $ git init                                               ---在当前路径建立版本仓库  
- $ git init XXXXProject-name                              ---新建一个目录，将其初始化为Git代码库  
- $ git clone XXXXUrl                                      ---下载项目和它的整个代码历史   


### 二、配置
- $ git config --list                                      ---查看配置信息  
- $ git config -e [--global]                              ---编辑Git配置文件  
- $ git config [--global] user.name "[UserName]"  
  $ git config [--global] user.email "[EmailAddress]"   ---设置提交代码时的用户信息  
  


### 三、增加/删除文件
- $ git add [file1] [file2] ...                           ---添加指定文件到暂存区  
- $ git add [dir]                                         ---添加指定目录到暂存区，包括子目录  
- $ git add .                                              ---添加当前目录的所有文件到暂存区  
- $ git add -p                                             ---对于同一个文件的多处变化，可以实现分次提交  
- $ git rm [file1] [file2] ...                            ---删除工作区文件，并且将这次删除放入暂存区  
- $ git rm --cached [file]                                ---停止追踪指定文件，但该文件会保留在工作区  
- $ git mv [file-original] [file-renamed]                ---改名文件，并且将这个改名放入暂存区  


### 四、代码提交
- $ git commit -m "[message]"                            ---提交暂存区到仓库区。 message:本次提交说明  
- $ git commit [file1] [file2] ... -m "[message]"       ---提交暂存区的指定文件到仓库区   
- $ git commit -a                                         ---提交工作区自上次commit之后的变化，直接到仓库区  
- $ git commit -v                                         ---提交时显示所有diff信息  
- $ git commit --amend -m "[message]"                    ---使用一次新的commit，替代上一次提交；如果代码没有任何新变化，则用来改写上一次commit的提交信息  
- $ git commit --amend [file1] [file2] ...               ---重做上一次commit，并包括指定文件的新变化  
- $ git commit --help                                     ---帮助  

### 五、分支
