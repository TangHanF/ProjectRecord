# 代码：



``` javascript

//中文占用两个字符，英文占用一个字符
String.prototype.gblen = function() {  
	var len = 0;  
	for (var i=0; i<this.length; i++) {  
		if (this.charCodeAt(i)>127 || this.charCodeAt(i)==94) {  
				len += 2;  
			} else {  
				len ++;  
			}  
		}  
	return len;  
};
var str = "软件开发";
var str_1 = "1234";
console.log(str.gblen());   
console.log(str_1.gblen());  
```