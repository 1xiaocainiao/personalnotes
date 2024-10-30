更新 ruby
brew upgrade ruby 

执行 brew link ruby 
根据报错添加，实际添加下面的到环境变量设置即可，需要更换版本号

export PATH="/opt/homebrew/opt/ruby/bin:$PATH"
export LDFLAGS="-L/usr/local/opt/ruby@3.3.5/lib"
export CPPFLAGS="-I/usr/local/opt/ruby@3.3.5/include"

生效配置
source ~/.zshrc   # 如果你是使用 zsh
# 或者
source ~/.bash_profile  # 如果你是使用 bash
