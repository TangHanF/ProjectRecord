在 ~/.bash_profile 中配置环境变量, 可是每次重启终端后配置的不生效.需要重新执行 : `$source ~/.bash_profile`

发现zsh加载的是 ~/.zshrc文件，而 ‘.zshrc’ 文件中并没有定义任务环境变量。

**解决办法**

在~/.zshrc文件最后，增加一行： 

> source ~/.bash_profile

然后再：

> source ~/.zshrc

