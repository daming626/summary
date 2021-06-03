

```
克隆仓库：git clone http://github.com/username/仓库名.git 

添加文件：git add ./*

添加文件：git add 具体名称

提交文件：git commit -m "注释"

上传文件：git push

下拉文件：git pull

查看详情：git status

查看日志：git log

回溯：
回退命令：

$ git reset --hard HEAD^         回退到上个版本
$ git reset --hard HEAD~3        回退到前3次提交之前，以此类推，回退到n次提交之前
$ git reset --hard commit_id     退到/进到 指定commit的sha码
 
强推到远程：
$ git push origin HEAD --force

```

将工程文件上传GitHub (cmd)

```
type nul>README.md
编辑README.md加入/out/
git init 
git add .
git commit -m "注释"
git remote add <name> <url>  //事先注册的仓库url?
git push <name>
```

create a new repository on the command lind

```
echo "# 仓库名" >> README.md
git init
git add README.md
git commit -m "注释"
git branch -m main
git renote add origin url
git push -u origin main
```

