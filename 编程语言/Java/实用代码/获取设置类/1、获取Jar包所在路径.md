> 作者：TangHanF（GuoFu）
>
> 日期：Jul 26, 2018
>
> 说明：转载请注明出处，谢谢！🤝
>
> 联系方式：guofu_gh@163.com

```java
/**
	 * 获取Jar所在目录
	 *
	 * @return
	 */
	public static String getPath() {
		String path = "";
		try {
			URL url = UtilProperties.class.getProtectionDomain().getCodeSource().getLocation();
			String filePath = null;
			try {
				filePath = URLDecoder.decode(url.getPath(), "utf-8");// 转化为utf-8编码
			} catch (Exception e) {
				e.printStackTrace();
			}
			if (filePath.endsWith(".jar")) {// 可执行jar包运行的结果里包含".jar"
				// 截取路径中的jar包名
				filePath = filePath.substring(0, filePath.lastIndexOf("/") + 1);
			} else {
				String[] splits = filePath.split("/");
				filePath = filePath.substring(0, filePath.lastIndexOf(splits[splits.length - 1]));
			}
			File file = new File(filePath);
			filePath = file.getAbsolutePath();//得到windows下的正确路径
			path = filePath;

//		String path = monitorClientMain.class.getClassLoader().toString();
//		LogHelper.i(path);
//		path = monitorClientMain.class.getClassLoader().getResource("").toString();
//		LogHelper.i(path);
//		path = monitorClientMain.class.getClassLoader().getResource("").getPath().toString();
//		LogHelper.i(path);
		} catch (Exception ex) {
			LogHelper.e(ex);
			ex.printStackTrace();
		} finally {
			return path;
		}
	}
```

