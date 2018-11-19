# 一、git基本概念
- 工作区：本地工作目录
- 暂存区：缓存文件区域
- 版本库：文件正式仓库

# 二、使用ssh秘钥对授权

## 1. 检查本地主机上是否存在ssh秘钥对
```shell
list -al ~/.ssh
```
若不存在 *id_rsa.pub* 及 *id_rsa*，使用```ssh-keygen -t rsa -C "youremail@example.com"```生成ssh key，接下来确认路径和输入密码均直接回车；
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
- 若提示是否continue，则输入yes。若最后显示```Hi username! You've successfully authenticated, but GitHub does not
provide shell access.```，则表示连接成功。

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
2. 初始化仓库：```git init```
3. 创建新文件或修改、删除已有文件
4. 使用```git status```查看文件状态
5. 使用```git add filename```将文件更新到暂存区
6. 使用```git commit -m "版本信息"```将更新保存到版本库


# 五、管理远程仓库
1. 添加远程仓库：```git remote add```
```
git remote add origin git@github.com:username/repository.git
```
2. 修改远程仓库的URL：```git remote set-url```
```
git remote set-url origin git@github.com:username/repository.git
```
3. 重命名远程仓库：```git remote rename```
```
git remote rename origin new
```
4. 删除远程仓库：```git remote rm```
```
git remote rm origin
```
