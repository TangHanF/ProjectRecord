在Mac OSX 系统默认是没有类似windows中的 tree命令，找到一条比较有意思的命令可以实现：

> find . -print | sed -e 's;/*/;|;g;s;|; |;g'

为了方便使用，写一个alias 到~/.profile或者 ~/.bash_profile 里:

> alias tree="find . -print | sed -e 's;/*/;|;g;s;|; |;g'"

写完之后记得`source ~/.profile`