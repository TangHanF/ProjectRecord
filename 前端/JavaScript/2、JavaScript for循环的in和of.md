```javascript
var obj = {name:"zhangsan",age:22};

for(var item in obj){
	console.log(item);
}
// 输出：name  age


for(var item of obj){
	console.log(item);
}
// 输出：zhangsan  22
```

