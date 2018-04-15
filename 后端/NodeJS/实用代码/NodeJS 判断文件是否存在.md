引入

```javascript
var fs= require("fs")
```

判断的方法

```javascript
fs.exists(path, callback)
```

path：判断的文件夹、文件的路径

callback：回调函数

```javascript
fs.exists("dirName", function(exists) {
	console.log(exists ? "创建成功" : "创建失败");
});
```