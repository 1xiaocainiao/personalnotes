##将默认bash改为zsh
chsh -s /usr/local/bin/zsh
因为有的配置在~/.bash_profile， 使用zsh是不会加载的,解决办法是vim ~/.zshrc创建，并将source ~/.bash_profile添加到~/.zshrc, 在终端执行一次source ~/.zshrc即可

##配置Zsh终端语法高亮显示

[原文链接](https://ywnz.com/linuxjc/4211.html)

一旦安装并设置zsh作为默认shell，从Github克隆zsh-syntax-highlighting并在~/.zshrc上获取它：

mkdir ~/.scripts

cd ~/.scripts

git clone https://github.com/zsh-users/zsh-syntax-highlighting.git

你需要在~.zshrc上获取的文件是~/.scripts/zsh-syntax-highlighting/zsh-syntax-highlighting.zsh。

编辑.zshrc文件：

vim ~/.zshrc

在文件末尾添加以下行：

source ~/.scripts/zsh-syntax-highlighting/zsh-syntax-highlighting.plugin.zsh

esc :wq 保存并退出

手动执行一次

source ~/.zshrc

要确认Zsh语法突出显示是否有效，请尝试在当前shell上编写for循环：

for i in a b c; do

echo "Printing value "

echo $i

done

![如图](https://upload-images.jianshu.io/upload_images/167849-52e86783553155cf.JPG?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
