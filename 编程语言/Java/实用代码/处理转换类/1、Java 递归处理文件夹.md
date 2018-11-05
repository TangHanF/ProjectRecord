> 作者：TangHanF（GuoFu）
>
> 日期：Jul 26, 2018
>
> 说明：转载请注明出处，谢谢！🤝
>
> 联系方式：guofu_gh@163.com

# 简单版

```java
public static void showAllFiles(File dir) throws Exception {
        File[] fs = dir.listFiles();
        if(fs!=null) {
            for (int i = 0; i < fs.length; i++) {
                System.out.println(fs[i].getAbsolutePath());
                if (fs[i].isDirectory()) {
                    try {
                        showAllFiles(fs[i]);
                    } catch (Exception e) {
                    }
                }
            }
        }else{
            System.out.println("无文件夹");
        }
    }
```

# 改进版

```java
public static void showAllFiles(File dir) throws Exception {
        File[] fs = dir.listFiles();
        if(fs!=null) {
            for (int i = 0; i < fs.length; i++) {
                if (fs[i].isDirectory()) {
                    //此处只显示文件夹，不显示文件
                 System.out.println(fs[i].getAbsolutePath());//C:\psht\psht\js
                    showAllFiles(fs[i]);
                }else{
                    //此处只获取文件，无文件夹
//                    System.out.println(fs[i].getAbsolutePath()); 
                }
            }
        }else{
            System.out.println("无文件夹");
        }

    }
```
