# 一、水平居中

## 适用场景说明

> - 块级元素
>
> - 非float的元素
>
> - 宽度确定与否都行

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>07-应用场景-垂直水平居布局</title>
    <style>
        body{
    		background-color: #a1a1a1;
		}
        
        #wrap{
            margin:0 auto;
            background-color: #fda428;
        }
    </style>
</head>
<body>
    <div id="wrap">我是div</div>
</body>
</html>
```

> 关键点在于：`margin:0 auto;`，即上下边距为0，左右自动。

![image-20181108141900784](https://ws2.sinaimg.cn/large/006tNbRwly1fx0mrfqpipj30wu0bct8w.jpg)

从以上效果图观察，很多人可能疑问：“我是div”几个字没有居中啊？注意，我们此处说的居中是指div元素居中，而非内部文字居中。怎么实现div居中且内部文字居中呢？只需要`text-align: center;`

```css
#wrap{
	margin:0 auto;
    text-align: center;
	background-color: #fda428;
}
```

![image-20181108142141736](https://ws1.sinaimg.cn/large/006tNbRwly1fx0mu4l0qnj30wu09yq33.jpg)

# 二、垂直居中

## 1、单行、高度确定

> - 行内元素或者行内块级元素
>
> - **单行**
>
> - **高度确定**

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <style>
       div{
           width: 200px;
           height: 200px;
           line-height: 200px;
           text-align: center;
           background: red;
       }
    </style>
</head>
<body>
    <div>我是单行居中</div>
</body>
</html>
```

![image-20181108142935657](https://ws4.sinaimg.cn/large/006tNbRwly1fx0n2cm9p1j30ma0e8q34.jpg)

> - 注意是**高度确定且单行**的情况下，使用`line-height`才生效
>
> - line-height=height才能垂直居中

## 2、多行、高度不确定(无关)

**适用场景**

> - 块级元素与否都行
>
> - 多行文本
>
> - 高度确定与否都行

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>多行文字居中</title>
    <style>
        body{
            background-color: #a1a1a1;
        }
        #wrap{
            width: 400px;
            height: 400px;
            text-align: center;
            background: red;
            display: table;
        }
        #wrap p{
            display: table-cell;
            vertical-align: middle;
        }
    </style>
</head>
<body>
<div id="wrap">
    <p>小伙找大师算命，大师说:“你从小辍学，十几岁外出打工，后认识了老板女儿，结婚后老板去世，所有家产已经过户到你名下，经过自己努力，现在资产过亿。”小伙说:“大师，你算的不对，我一直是好学生，大学毕业出国留学，有一大堆文凭，现在回来还没找到工作，至今单身，还没谈过恋爱。”大师沉默片刻:“唉，知识改变命运啊，你早辍学的话，早就混好了！”</p>
</div>
</body>
</html>
```
> 具体操作就是在父元素中`display:table`，自身进行：`display: table-cell;vertical-align: middle;`

![image-20181108143938176](https://ws4.sinaimg.cn/large/006tNbRwly1fx0ncskve6j30uy0ocn08.jpg)

## 3、div的垂直居中(高度确定)

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>多行文字居中</title>
    <style>
        body{
            background-color: #a1a1a1;
        }
        #wrap{
            position: relative;
            width: 450px;
            height: 450px;
            background: #ffa500;
        }
        #div1{
            position: absolute;
            width: 200px;
            height: 200px;
            top: 50%;
            margin-top: -100px;
            background: #55d4eb;
        }
    </style>
</head>
<body>
<div id="wrap">
    <div id="div1"></div>
</div>
</body>
</html>
```

> 以上要将div1进行垂直居中显示。
>
> div1的高度是确定的，即200px。我们需要将其父元素的position置为relative，同时自身进行绝对定位，进而设置top以及margin-top值。top:50%是固定的，但是margin-top的值是不固定的，需要根据实际情况计算得出。即`margin-top=-(height/2)`

![image-20181108144753340](https://ws2.sinaimg.cn/large/006tNbRwly1fx0nldzab2j30uy0smaaj.jpg)

## 4、div的垂直居中(高度不确定)

与“二-2”章节原理一样。

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>未知高度居中</title>
    <style>
        #wrap {
            text-align: center;
            width: 200px;
            height: 200px;
            background: #ffa500;
            display: table;
            padding: 50px;
        }

        #wrap div {
            display: table-cell;
            vertical-align: middle;
            background: #55d4eb;
        }
    </style>
</head>

<body>
    <div id="wrap">
        <div>以前听一个笑话让用ABCDEFG怎么造句：A呀，这B孩，C家的，光脚站在D上，EF也不穿，GG还露在外边。其实ABCDEFG是什么意思：A boy can do everything for girl.</div>
    </div>
</body>
</html>
```

![image-20181108154800371](../../../../../Library/Application Support/typora-user-images/image-20181108154800371.png)

# 三、水平垂直居中

## 1、宽度、高度确定

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>多行文字居中</title>
    <style>
        #wrap{
            position: relative;
            width: 450px;
            height: 450px;
            background: #ffa500;
        }
        #div1{
            position: absolute;
            width: 200px;
            height: 200px;
            top: 50%;
            left:50%;
            margin-top: -100px;
            margin-left:-100px;
            background: #55d4eb;
        }
    </style>
</head>
<body>
<div id="wrap">
    <div id="div1"></div>
</div>
</body>
</html>
```

> 以上要将div1进行垂直居中显示。
>
> div1的高度是确定的，即200px，宽度也是确定的，即200px。我们需要将其父元素的position置为relative，同时自身进行绝对定位，进而设置top以及margin-top值。top:50%;left:50%是固定的，但是margin-top的值是不固定的，需要根据实际情况计算得出。即`margin-top=-(height/2)`、`margin-left=-(left/2)`

![image-20181108154945725](../../../../../Library/Application Support/typora-user-images/image-20181108154945725.png)

## 2、未知宽度、高度元素的水平垂直居中

### 方式一:display:table

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>未知高度和宽度元素的水平垂直居中 </title>
    <style>
        #wrap {
            text-align: center;
            width: 200px;
            height: 200px;
            background: #ffa500;
            display: table;
            padding: 50px;
        }

        #wrap div {
            display: table-cell;
            vertical-align: middle;
            background: #55d4eb;
        }
    </style>
</head>

<body>
    <div id="wrap">
        <div>以前听一个笑话让用ABCDEFG怎么造句：A呀，这B孩，C家的，光脚站在D上，EF也不穿，GG还露在外边。其实ABCDEFG是什么意思：A boy can do everything for girl.</div>
    </div>
</body>
</html>
```

### 方式二:position定位+transform

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>未知高度和宽度元素的水平垂直居中 </title>
    <style>
        #wrap {
            position: relative;
            background: #ffa500;
            padding: 50px;
        }

        #wrap div {
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            background: #55d4eb;
        }
    </style>
</head>
<body>
    <div id="wrap">
        <div>以前听一个笑话让用ABCDEFG怎么造句：A呀，这B孩，C家的，光脚站在D上，EF也不穿，GG还露在外边。其实ABCDEFG是什么意思：A boy can do everything for girl.</div>
    </div>
</body>
</html>
```

### 方式三：flex布局

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>未知高度和宽度元素的水平垂直居中-flex实现 </title>
    <style>
        #wrap {
            display: flex;
            /* 水平居中 */
            justify-content: center;
            /* 垂直居中 */
            align-items: center;
            background: #ffa500;

        }

        #wrap div {
          background: #55d4eb;
            margin: 10px;
        }
    </style>
</head>

<body>
    <div id="wrap">
        <div>我是div</div>
        <div>这么巧，我也是div</div>
        <div>我的天啊！居然有两个div在啊，这么巧，我也是div,哈哈</div>
    </div>
</body>
</html>
```

![image-20181108160304177](https://ws2.sinaimg.cn/large/006tNbRwly1fx0prmo5vej30v2054aap.jpg)

### 方式四：gird布局

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>未知高度和宽度元素的水平垂直居中-grid实现 </title>
    <style>
        *{
            margin: 0;
        }
        body,
        html {
            height: 100%;
            display: grid;
            text-align: center;
            background: #ffa500;
        }

        div {
            margin: auto;
            background: #55d4eb;
        }
    </style>
</head>
<body>
    <div id="wrap">
        <div>我是div</div>
        <div>这么巧，我也是div</div>
        <div>我的天啊！居然有两个div在啊，这么巧，我也是div,哈哈</div>
    </div>
</body>
</html>
```

> 第四、五方法属于比较前沿的用法，目前兼容性不是很好，可以在自己的项目中测试后使用。但是这两种方法最终将成为今后的主流方法。