# 一、git基本概念
- 工作区：本地工作目录
- 暂存区：缓存文件区域
- 版本库：文件正式仓库

# 二、使用ssh秘钥对授权

## 1. 检查本地主机上是否存在ssh秘钥对
```shell
list -al ~/.ssh
```
若不存在 *id_rsa.pub* 及 *id_rsa*，使用`ssh-keygen -t rsa -C "youremail@example.com"`生成ssh key，接下来确认路径和输入密码均直接回车；
若存在 *id_rsa.pub* 及 *id_rsa*，可直接使用，也可重新生成。\

## 2. 添加ssh key到github账户
- 复制ssh key到剪贴板
```shell
clip < ~/.ssh/id_rsa.pub
```
- 打开github，选择Settings->SSH and GPG keys->New SSH key，在Title栏添加该ssh key的标签，Key栏填入刚刚复制的key
- 点击Add SSH key

## 3. 测试SSH是否连接
- 打开bash，输入：
```shell
ssh -T git@github.com
```
- 若提示是否continue，则输入yes。若最后显示`Hi username! You've successfully authenticated, but GitHub does not
provide shell access.`，则表示连接成功。

# 三、设置username和email
```shell
git config --global user.name "your name"
git config --global user.email "your_email@youremail.com"
```
查看是否配置成功：
```shell
git config --list
```

# 四、管理本地仓库
1. 创建新目录或者直接进入已存在的目标目录
2. 初始化仓库：`git init`
3. 创建新文件或修改、删除已有文件
4. 使用`git status`查看文件状态
5. 使用`git add filename`将文件更新到暂存区
6. 使用`git commit -m "版本信息"`将更新保存到版本库


# 五、管理远程仓库
1. 添加远程仓库：`git remote add`
```
git remote add origin git@github.com:username/repository.git
```
2. 修改远程仓库的URL：`git remote set-url`
```
git remote set-url origin git@github.com:username/repository.git
```
3. 重命名远程仓库：`git remote rename`
```
git remote rename origin new
```
4. 删除远程仓库：`git remote rm`
```
git remote rm origin
```
5. 详细显示远程仓库信息
```
git remote -v
```
6. 克隆远程仓库：`git clone`
```
git clone git@github.com:username/repository.git
```
7. 推送本地更新到远程仓库：`git push`
```
git push origin master  --将本地仓库的master分支推送到远程仓库origin
```
8. 提取远程或本地分支，并合并到指定分支：`git pull 远程仓库名 远程分支名:本地分支名`
```
git pull origin master:master  --将origin的master分支提取并合并到本地master分支
```
9. 提取分支：`git fetch`
```
git fetch origin master  --提取origin的master分支到本地origin/master分支
git fetch origin master:temp  --提取origin的master分支到本地新建的temp分支
```
10. 合并分支：`git merge`
```
git merge origin/master  --将本地origin/master分支与当前分支合并
git merge temp  --将本地temp分支与当前分支合并
```
# 五、添加、删除文件

# 六、提交

# 七、分支管理
1. 创建分支：`git branch 新分支名`
```
git branch dev  --创建dev分支
```

2. 列出分支：`git branch`
```
git branch  --列出本地分支
git branch -r  --列出远程分支
git branch -a  --列出所有分支
```
3. 查看分支详细信息：`git show-branch`

4. 检出分支：`git checkout 分支名`
```
git checkout dev  --切换到dev分支
```

5. 创建并检出分支：`git checkout -b 新分支名`
```
git checkout -b dev  --创建并检出分支dev
```

6. 删除分支：`git branch -d 分支名`
```
git branch -d dev  --删除dev分支
```
