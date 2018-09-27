和谐版的Alfred 3 在每次开机后，都会提示“是否允许访问通讯录”的弹窗，让人不胜其烦。
这是因为和谐片的App丢失了签名导致不会自动加入系统

### 处理方法

打开终端（或iTerm2）

```bash
sudo codesign -f -d -s - /Applications/Alfred\ 3.app/Contents/Frameworks/Alfred\ Framework.framework/Versions/A/Alfred\ Framework
```

