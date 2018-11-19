# 一、使用ssh秘钥对授权

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
