# Git 命令别名和常用技巧

```
http://www.git-scm.com/download/
http://www.git-scm.com/download/win
http://www.git-scm.com/download/mac

Git via Git
If you already have Git installed, you can get the latest development version via Git itself:
git clone https://github.com/git/git

echo 'alias l="ls -al" ..="cd .." ...="cd ../.."' >> ~/.bash_profile
echo 'alias open=\"$WINDIR/explorer.exe\"' >> ~/.bash_profile
echo 'alias glg="git log --pretty=format:\"%Cred%h%Creset %an %ad - %C(yellow)%d%Creset%s%Cgreen(%cr)%Creset\" --graph --date=format:%c"' >> ~/.bash_profile
echo 'alias g="git" ga="git add" gaa="git add --all" gs="git status -sb" gst="git status" gd="git diff"' >> ~/.bash_profile
echo 'alias gb="git branch" gbr="git branch -r" gba="git branch -a"' >> ~/.bash_profile
echo 'alias gco="git checkout" gcb="git checkout -b" gcm="git checkout master"' >> ~/.bash_profile
echo 'alias gc="git commit -v" gca="git commit -v -a" gcam="git commit -a -m" gcmsg="git commit -m"' >> ~/.bash_profile
echo 'alias gps="git push" gl="git pull"' >> ~/.bash_profile
source ~/.bash_profile


创建分支
git checkout -b newbranch
git push -u origin newbranch
git branch -a
合并newbranch到master分支
git branch master
git branch
git merge newbranch
git push
删除分支
git branch -a
git branch -d delbranch
git branch -r -d origin/delbranch
git push origin :delbarnch
创建tag
git tag newtag
git push origin newtag
git tag -l
删除tag
git tag -d deltag
git push origin :refs/tags/deltag
修改远程仓库地址
$ git remote -v
origin  git@172.24.10.155:Bob/WorkflowDesigner2.git (fetch)
origin  git@172.24.10.155:Bob/WorkflowDesigner2.git (push)
$ git remote set-url origin git@192.168.0.101:Bob/WorkflowDesigner2.git
$ git remote -v
origin  git@192.168.0.101:Bob/WorkflowDesigner2.git (fetch)
origin  git@192.168.0.101:Bob/WorkflowDesigner2.git (push)


配置全局信息（详细：https://git-scm.com/docs/git-config）
$ git config --global user.name "m2nlight"
$ git config --global user.email "wingingbob@gmail.com"
$ git config --global push.default "simple"
$ cat ~/.gitconfig
[user]
        name = m2nlight
        email = wingingbob@gmail.com
[push]
        default = simple
$ git config --global core.excludesfile "$HOME/.gitignore_global"
$ cat ~/.gitignore_global
*~
.DS_Store
.idea
# some comment.




配置SSH
$ ssh-keygen -t -b 4096 rsa -C "weirb@geodo.cn"
$ $ eval "$(ssh-agent -s)"
Agent pid 28728
$ ssh-add -K ~/.ssh/id_rsa   // ssh-add -k ~/.ssh/id_rsa
$ clip < ~/.ssh/id_rsa.pub   // pbcopy < ~/.ssh/id_rsa.pub
如果粘贴github上失败，去掉最后的一个换行。



更改git连接方式https为ssh
复制好ssh地址，然后打开.git/config文件修改[remote "origin"]下的url


Git push/pull fatal: protocol error: bad line length character: This
原因是服务器端没为git用户配置bash，解决方法是：
# sudo usermod -s /bin/bash git

```