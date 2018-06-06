> 作者：TangHanF（GuoFu）
>
> 日期：
>
> 说明：转载请注明出处，谢谢！🤝
>
> 联系方式：guofu_gh@163.com

# Mac键盘符号映射

![](https://ws1.sinaimg.cn/large/006tNc79ly1fr4c4kxmrij30iq0plwgn.jpg)

# Finder

- `⌘+⬆` 返回上一级目录

- `⌘+⇧+.` 可以显示隐藏文件、文件夹，再按一次，恢复隐藏，或者命令：

  > - 显示：defaults write com.apple.finder AppleShowAllFiles -bool true
  > - 隐藏：defaults write com.apple.finder AppleShowAllFiles -bool false
  >
  > 注意执行：`KillAll Finder` 以便生效

  或者利用Automator制作一个小程序：

  ```bash
  display dialog "隐藏/显示隐藏文件" buttons {"可见", "隐藏"} with icon 2 with title "Switch to presentation mode" default button 1
  
  set switch to button returned of result
  
  if switch is "隐藏" then
  	do shell script "defaults write com.apple.finder AppleShowAllFiles -bool false;
  KillAll Finder"
  	
  else
  	do shell script "defaults write com.apple.finder AppleShowAllFiles -bool true;
  KillAll Finder"
  	
  end if
  ```

  

- `⌘+⇧+G` 可以前往任何文件夹，包括隐藏文件夹。

- `⌘+N` 新建文件夹

# 全局

- `⌃+↑` 打开任务，等同于F3
- `⌃+↓`
- `⌘+↑` 回到顶部
- `⌘+↓` 回到底部
- `⌘+M` 最小化
- 按住 ⌘ 键，可以拖动非焦点窗口同时不激活它
- `⌃+⌘+空格` 快速打开表情符号
- 激活Spotlight搜索的时候，使用⌘+上下方向键还可以在搜索分组之间切换
- `⌘+⌫` 删除文件，移动到废纸篓，如果是在废纸篓里面按该组合键，则是将删除的内容还原😳
- `Fn+⌫` 可以实现向后删除，类似于windos的Delete键，正常的⌫相当于Windows的BackSpace键
- `⌘+⇧+S` 另存为
- `⌘+⌥+H` 隐藏所有闲置的窗口