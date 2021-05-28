Git 学习记录

设置Git的user name和email：
git config --global user.name "xuhaiyan"
git config --global user.email "haiyan.xu.vip@gmail.com"


Git SSH Key 生成步骤
Git分布式代码管理，基于SSH，所以要使用远程Git需要配置SSH

1.打开终端查看是否存在ssh密钥: cd ~/.ssh, 如果有没密钥则不会有此文件夹，有则备份删除
2.生成密钥:
Ssh-keygen -t rsa -C xxx@qq.com
按三个回车，密码为空
Your identification has been saved in /home/tekkub/.ssh/id_rsa.
Your public key has been saved in /home/tekkub/.ssh/id_rsa.pub.
The key fingerprint is:
最后得到两个文件: id_rsa 和 id_rsa.pub
3. 添加密钥到ssh: ssh-add 文件名，需要之前输入的密码 (注意好多教程没有这一步，我这里添加后才能正确)
4. 在github 上添加ssh密钥，打开上面获取的 id_rsa_pub，将里面的公钥复制添加到github ssh
5. 测试: ssh git@github.com
Hi tekkub! You’ve successfully authenticated, but GitHub does not provide shell access
Connection to github.com closed

原文链接 Git SSH Key生成: https://blog.csdn.net/hustpzb/article/details/8230454
Github 创建分支链接 : https://blog.csdn.net/top_code/article/details/51931916
Git 常用命令: https://gist.github.com/akkias/6355816

cd到工程,修改远程仓库地址
git remote set-url origin http://git.sudyapp.com/client/Sudy.git

