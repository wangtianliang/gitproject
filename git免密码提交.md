使用git push提交时，每次都要输入密码，次数多了，感觉挺麻烦. 如果git以ssh协议通讯，免密码可以用ssh公钥设置免登录。如果git时以https方式访问呢，该怎么办？下面方可以解决这个问题.
 
* 新建文件并保存密码
touch ~/.git-credentials
vim ~/.git-credentials
添加内容
https://{username}:{passwd}@github.com
* 添加git配置
执行下面命令添加配置
git config --global credential.helper store
 
* 查看~/.gitconfig文件变化
 
~/.gitconfig文件多出下面配置项
[credential]
    helper = store
 
再尝试git push不再需要输入密码.
