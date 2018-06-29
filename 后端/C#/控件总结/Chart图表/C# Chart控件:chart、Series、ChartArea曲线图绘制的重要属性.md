![](https://ws4.sinaimg.cn/large/006tKfTcly1fsruxh6ugij30j60cdq52.jpg)



先简单说一下，从图中可以看到一个chart可以绘制多个ChartArea，每个ChartArea都可以绘制多条Series。ChartArea就是就是绘图区域，可以有多个ChartArea叠加在一起，series是画在ChartAarea上的，Series英文意思是“序列、连续”，其实就是数据线，它可以是曲线、点、柱形、条形、饼图...可以注意该chart当数据非常多的时候可以通过鼠标选择查看区域，进一步拖拽横纵向滚动条来缩小曲线图查看。
代码中的Chart控件的命名是chartData，数据源是dt，由于chart属性太多，不好一一解释，所以请仔细看截图，尤其重视本例用到的属性

 

# 一、数据源

​    数据返回方式是DataSet.Tables[0],即DataTable，也是最基本的数据源方式。这里只介绍DataTable绑定数据源，很简单：

​                chartData.DataSource = dt;
                chartData.DataBind();

# 二、Series

​    Series是画在ChartArea上的线、点、柱形、条形、饼图，简单点儿说就是画在上面的数据，直接说属性，

## 1、标记

> 就是数据点，某个数据值的点。如下图所示：

​    [![C# Chart控件，chart、Series、ChartArea曲线图绘制的重要属性](http://s12.sinaimg.cn/mw690/621e24e2tx6CIBXVbGXdb&690) ](http://photo.blog.sina.com.cn/showpic.html#blogid=621e24e20101cp64&url=http://album.sina.com.cn/pic/621e24e2tx6CIBXVbGXdb)[![C# Chart控件，chart、Series、ChartArea曲线图绘制的重要属性](http://s6.sinaimg.cn/mw690/621e24e2tx6CIBYIqzPd5&690) ](http://photo.blog.sina.com.cn/showpic.html#blogid=621e24e20101cp64&url=http://album.sina.com.cn/pic/621e24e2tx6CIBYIqzPd5)

- `MarkerBorderColor`：数据点边框的颜色

- `MarkerBorderWidth`：数据点边框的宽度

- `MarkColor`：数据点的颜色

- `MakerSize`：数据点的大小，默认值为0数据点不存在，建议代码控制

- `MarkerStep`：数据点显示的频率

- `MarkerStyle`：数据点的样式，可以是方块、圆圈、三角、叉子....

​               

## 2、标签

> 就是现在是在数据点旁边数据值        

​      [![C# Chart控件，chart、Series、ChartArea曲线图绘制的重要属性](http://s8.sinaimg.cn/mw690/621e24e2tx6CIC0WK9h67&690) ](http://photo.blog.sina.com.cn/showpic.html#blogid=621e24e20101cp64&url=http://album.sina.com.cn/pic/621e24e2tx6CIC0WK9h67)

- `IsValueShownAsLabel`：数据值是否显示，建议代码控制

- `SmartLabelStyle`：数据值样式

- `SmartLabelStyle`.Enabled：直接控制可用不可用，建议不可用

- `SmartLabelStyle.AllowOutsidePloArea`：数据值显示是否允许在外面

- 其他属性....



**注意：**

​	如果要使用SmartLabelStyle的话，所有的数据点的值都会自动找位置显示出来，如果某一个区域数据点较多，就会直线指示；如果不用的话，数据点的值会在数据点旁边显示，不会有直线。如下图所示也可以看到AllowOutsidePlotArea的区别：

[![C# Chart控件，chart、Series、ChartArea曲线图绘制的重要属性](http://s7.sinaimg.cn/mw690/621e24e2tx6CIC3IKpM06&690)](http://photo.blog.sina.com.cn/showpic.html#blogid=621e24e20101cp64&url=http://album.sina.com.cn/pic/621e24e2tx6CIC3IKpM06)
[![C# Chart控件，chart、Series、ChartArea曲线图绘制的重要属性](http://s10.sinaimg.cn/mw690/621e24e2tx6CIC6bKVHf9&690)](http://photo.blog.sina.com.cn/showpic.html#blogid=621e24e20101cp64&url=http://album.sina.com.cn/pic/621e24e2tx6CIC6bKVHf9)

## 3、Font

> 数据标签上的字体和样式

​               [![C# Chart控件，chart、Series、ChartArea曲线图绘制的重要属性](http://s15.sinaimg.cn/mw690/621e24e2tx6CICan6x03e&690) ](http://photo.blog.sina.com.cn/showpic.html#blogid=621e24e20101cp64&url=http://album.sina.com.cn/pic/621e24e2tx6CICan6x03e)      

- `Font`：标签字体设置

- `Font.Unit`：个人设置此值为Document，自己体会

- `LabelAngle`：标签角度，斜多少度，建议就正着

- `LabelBackColor`：标签背景颜色

- `LabelBorderColor`：标签边框颜色

- `LabelBorderDahStyle` ：标签边框样式

- `LabelBorderWidth`：标签边框宽度

- `LabelForeColor`：标签字体颜色

- 其他属性....



​                 [![C# Chart控件，chart、Series、ChartArea曲线图绘制的重要属性](http://s14.sinaimg.cn/mw690/621e24e2tx6CICc8zOB8d&690) ](http://photo.blog.sina.com.cn/showpic.html#blogid=621e24e20101cp64&url=http://album.sina.com.cn/pic/621e24e2tx6CICc8zOB8d)[![C# Chart控件，chart、Series、ChartArea曲线图绘制的重要属性](http://s2.sinaimg.cn/mw690/621e24e2tx6CICcMzQJd1&690) ](http://photo.blog.sina.com.cn/showpic.html#blogid=621e24e20101cp64&url=http://album.sina.com.cn/pic/621e24e2tx6CICcMzQJd1)     
        

真好看![C# <wbr>Chart控件，chart、Series、ChartArea曲线图绘制的重要属性](http://www.sinaimg.cn/uc/myshow/blog/misc/gif/E___6725EN00SIGG.gif)数据多的时候本来显示就乱拉，这样更是画蛇添足，建议透明，正常点的颜色就好

## 4、空白点

就是连续的数据，譬如X轴对应Y轴没数据，或Y轴对应X轴没数据，这样的数据点可以对其设置相应的属性，属性大多都是上面说过的，自己试一下即可

​               [![C# Chart控件，chart、Series、ChartArea曲线图绘制的重要属性](http://s7.sinaimg.cn/mw690/621e24e2tx6CHwzZsN056&690) ](http://photo.blog.sina.com.cn/showpic.html#blogid=621e24e20101cp64&url=http://album.sina.com.cn/pic/621e24e2tx6CHwzZsN056)

 

## 5、数据

其实就是就是serie的名字和值类型

​               [![C# Chart控件，chart、Series、ChartArea曲线图绘制的重要属性](http://s15.sinaimg.cn/mw690/621e24e2tx6CICfkaHI4e&690)](http://photo.blog.sina.com.cn/showpic.html#blogid=621e24e20101cp64&url=http://album.sina.com.cn/pic/621e24e2tx6CICfkaHI4e)  

- `Name`：就是唯一的名字
- `XvalueType`： X轴值类型
- `YValuesPerPoint`： 数据点的Y值数目
- `YValueType`：Y轴值类型

- 其他属性...

​    默认不用设置就好，主要是X轴和Y轴值类型设置的是Auto，也就是根据X轴上的值和Y轴上的值的类型自动匹配，当然手动设置的话不设错就行了。

## 6、数据源

注意这里是Series的数据源

​            [![C# Chart控件，chart、Series、ChartArea曲线图绘制的重要属性](http://s13.sinaimg.cn/mw690/621e24e2tx6CICkkb1i5c&690) ](http://photo.blog.sina.com.cn/showpic.html#blogid=621e24e20101cp64&url=http://album.sina.com.cn/pic/621e24e2tx6CICkkb1i5c)

​    注意：
    第一，这两个属性对应的是DataTable的两个列，也就是一般的X轴对应时间，Y轴对应数据值，但是也要注意对DataTable的每个数据单元的值做判断，尤其是DBNull或空。我这里的数据库的NewDateTime列数据类型是DateTime类型，NewFyj是Double类型。

​    第二，Series的数据源和Chart控件的数据源有区别，只有DataTable先绑定了Chart，Series才对应到列，否则无法对应。

​    第三，假如用户需要先查看所有数据，然后取消某几条进行数据对比，但是不需要重新查询数据，推荐赋值string.Empty实现，如下图:

​                     [![C# Chart控件，chart、Series、ChartArea曲线图绘制的重要属性](http://s16.sinaimg.cn/mw690/621e24e2tx6CHyOFosv9f&690) ](http://photo.blog.sina.com.cn/showpic.html#blogid=621e24e20101cp64&url=http://album.sina.com.cn/pic/621e24e2tx6CHyOFosv9f)

## 7、图表

​	也就是Serie画在哪个ChartArea上，ChartType是Serie的图表类型，也就是画何种图，曲线图、直线图、点、柱状图、饼图等...

​                  [![C# Chart控件，chart、Series、ChartArea曲线图绘制的重要属性](http://s15.sinaimg.cn/mw690/621e24e2tx6CIChYOvQee&690)](http://photo.blog.sina.com.cn/showpic.html#blogid=621e24e20101cp64&url=http://album.sina.com.cn/pic/621e24e2tx6CIChYOvQee)

## 8、图例

​	也就是每个Serie的名字和样式，只要创建Serie就会自动产生加载在Legend里，里面的属性可以试一下，如果想调整Legend的位置，可以去Legend集合里设置，比较简单，这里不多说

​                     [![C# Chart控件，chart、Series、ChartArea曲线图绘制的重要属性](http://s14.sinaimg.cn/mw690/621e24e2tx6CICmgvmt0d&690) ](http://photo.blog.sina.com.cn/showpic.html#blogid=621e24e20101cp64&url=http://album.sina.com.cn/pic/621e24e2tx6CICmgvmt0d)

## 9、图表

​                   [![C# Chart控件，chart、Series、ChartArea曲线图绘制的重要属性](http://s16.sinaimg.cn/mw690/621e24e2tx6CICnOrvx2f&690) ](http://photo.blog.sina.com.cn/showpic.html#blogid=621e24e20101cp64&url=http://album.sina.com.cn/pic/621e24e2tx6CICnOrvx2f)

## 10、映射区

鼠标放在数据点上出现的小提示，建议用代码控制

​                      [![C# Chart控件，chart、Series、ChartArea曲线图绘制的重要属性](http://s16.sinaimg.cn/mw690/621e24e2tx6CHzKJRV57f&690)](http://photo.blog.sina.com.cn/showpic.html#blogid=621e24e20101cp64&url=http://album.sina.com.cn/pic/621e24e2tx6CHzKJRV57f)

​             [![C# Chart控件，chart、Series、ChartArea曲线图绘制的重要属性](http://s12.sinaimg.cn/mw690/621e24e2tx6CICw6SLN7b&690) ](http://photo.blog.sina.com.cn/showpic.html#blogid=621e24e20101cp64&url=http://album.sina.com.cn/pic/621e24e2tx6CICw6SLN7b)

## 11、杂项

​               [![C# Chart控件，chart、Series、ChartArea曲线图绘制的重要属性](http://s11.sinaimg.cn/mw690/621e24e2tx6CHzLroDM7a&690) ](http://photo.blog.sina.com.cn/showpic.html#blogid=621e24e20101cp64&url=http://album.sina.com.cn/pic/621e24e2tx6CHzLroDM7a)
                          EmptyPointValue          空数据点的值做平均还是做零处理

​                          LabelStyle               对标签硬性的规定显示在数据点旁的哪个位置

## 12、轴

​	也就是X轴和Y轴，X轴有主轴和副轴，Y轴也有主轴和副轴，主轴为Primary，副轴为Secondary。X主轴在下方，Y主轴在右方，X副轴在上方，Y副轴在右方。

​                         [![C# Chart控件，chart、Series、ChartArea曲线图绘制的重要属性](http://s13.sinaimg.cn/mw690/621e24e2tx6CHzMlHoE5c&690)  ](http://photo.blog.sina.com.cn/showpic.html#blogid=621e24e20101cp64&url=http://album.sina.com.cn/pic/621e24e2tx6CHzMlHoE5c)

# 三、ChartAreas

​    Chart控件里最重要的，每个Serie都画在ChartArea上，Chart控件可以有多个ChartArea叠加在一起显示。比如第一个ChartArea绘制的是曲线，第二个画的柱状图或者是什么什么，这也是上面说过的Serie的ChartType，我们也可以把多个Serie画在一个ChartArea上，但是如果有一个列数据单位范围在 500~10000 之间的数据浮动最大，有一列数据单位范围在 0.1~2.0 之间，有一列数据单位范围在 50~100 之间，那画在同一个ChartArea上显示的话，0.1到2.0的数据会变成一条直线。当只有1、2条这样的数据时，可以在Serie中设置主轴和副轴，但当出现多条数据，多种类型的显示，就需要多个ChartArea来解决了。由于属性太多了，捡重点属性介绍，其他的属性自己试一下

## 1、对齐：

ChartArea对齐方式

​                   [![C# Chart控件，chart、Series、ChartArea曲线图绘制的重要属性](http://s16.sinaimg.cn/mw690/621e24e2tx6CHClkWMT6f&690) ](http://photo.blog.sina.com.cn/showpic.html#blogid=621e24e20101cp64&url=http://album.sina.com.cn/pic/621e24e2tx6CHClkWMT6f)

- `AlignmentOrientation`            水平对齐、垂直对齐、全部对齐

- `AlignmentStyle`                  根据哪种方式对齐

- `AlignmentWithChartArea`          和哪个对齐

​     老实说，没啥用，可以设置Position，一会儿在外观里会说到

## 2、 三维

自己试试，效果很沉重，不是很好

​                            [![C# Chart控件，chart、Series、ChartArea曲线图绘制的重要属性](http://s16.sinaimg.cn/mw690/621e24e2tx6CHCDyoOjef&690)](http://photo.blog.sina.com.cn/showpic.html#blogid=621e24e20101cp64&url=http://album.sina.com.cn/pic/621e24e2tx6CHCDyoOjef)

 

## 3、 外观

可以对ChartArea颜色、边框、位置的设置

​                 [![C# Chart控件，chart、Series、ChartArea曲线图绘制的重要属性](http://s1.sinaimg.cn/mw690/621e24e2tx6CICzIuOsc0&690)](http://photo.blog.sina.com.cn/showpic.html#blogid=621e24e20101cp64&url=http://album.sina.com.cn/pic/621e24e2tx6CICzIuOsc0)

- `BackColor`                       ChartArea的背景颜色
- `BackGradientStyle`               背景颜色的渐变方式
- `BackHatchStyle`                  背景阴影
- `BackImage`                       背景图片
- `BackImageAlignment`              图片显示位置
- `BackImageTransparentColor`       绘制图像时显示的颜色
- `BackImageWrapMode`               包装模式  
- `BackSecondaryColor`              ChartArea的第二背景颜色，搭配渐变用的
- `BorderColor`                     边框颜色
- `BorderDashStyle`                 边框线的样式
- `BorderWidth`                     边框宽度
- `ShadowColor`                     整个图标的背影颜色
- `ShadowOffset`                    背影偏移量

**注意：**

- 第一，InnerPlotPosition和Position一个是大的，一个是内部绘制的，试一下就明白了，这里最重要的是多个ChartArea重叠在一起的时候，两个Position一定要设置相同，否则就重叠不上了。
- 第二，多个ChartArea重叠在一起的时候，颜色或图片只能在叠在最底下的ChartArea来设置，上面的ChartArea都设置为透明即可，最底下的ChartArea是ChartAreas[0]，所以不要设置错。

 

## 4、游标

CursorX和CursorY，就是横向和纵向滚动条

​             [![C# Chart控件，chart、Series、ChartArea曲线图绘制的重要属性](http://s5.sinaimg.cn/mw690/621e24e2tx6CICCyuTq74&690)](http://photo.blog.sina.com.cn/showpic.html#blogid=621e24e20101cp64&url=http://album.sina.com.cn/pic/621e24e2tx6CICCyuTq74)
                       CursorX.AutoScroll                  滚动条自动滚动

- CursorX.AxisType                    游标作用在主轴还是副轴
- CursorX.Interval                    游标偏移的间隔
- CursorX.IntervalOffset              游标间隔偏移量
- CursorX.IntervalOffsetType          游标间隔的单位，建议Auto
- CursorX.Type                        游标间隔偏移量的单位，建议Auto
- CursorX.IsUserEnabled               启用游标
- CursorX.IsUserSelectedEnabled       启用游标选择区域
- CursorX.LineColor                   游标线颜色
- CursorX.LineDashStyle               游标线样式
- CursorX.LineWidth                   游标线的宽度
- CursorX.SelectionColor              游标选择区域的颜色
- CursorY相同，其他属性自己试

​    首先强调一下，只要想选择区域细看曲线图，就一定要启用游标，游标的设置只能在叠加在最上面的ChartArea进行设置，也就是ChartArea[ChartArea.Count-1]，。列了这么多属性看一下图更直观：

[![C# Chart控件，chart、Series、ChartArea曲线图绘制的重要属性](http://s4.sinaimg.cn/mw690/621e24e2tx6CICEsu4z73&690)](http://photo.blog.sina.com.cn/showpic.html#blogid=621e24e20101cp64&url=http://album.sina.com.cn/pic/621e24e2tx6CICEsu4z73)
X轴和Y轴上有游标，可以拖动，可以注意看有个按钮上面有个圆圈，就是向后退，图中的蓝色矩形方块就是用户选择的区域，松开鼠标就会变成该区域的图形。

## 5、杂项

Name，没啥好说的

​                       [![C# Chart控件，chart、Series、ChartArea曲线图绘制的重要属性](http://s8.sinaimg.cn/mw690/621e24e2tx6CHHDWEMD67&690) ](http://photo.blog.sina.com.cn/showpic.html#blogid=621e24e20101cp64&url=http://album.sina.com.cn/pic/621e24e2tx6CHHDWEMD67)

## 6.、轴Axes！！

非常重要，一个ChartArea有4个轴：

1. 主轴X axis

2. 主轴Y（Value）axis、

3. 副轴X axis、

4. 副轴Y（Value）axis


每个轴属性均相同，只说一个一个轴

​                 [![C# Chart控件，chart、Series、ChartArea曲线图绘制的重要属性](http://s12.sinaimg.cn/mw690/621e24e2tx6CICG6CRZ5b&690) ](http://photo.blog.sina.com.cn/showpic.html#blogid=621e24e20101cp64&url=http://album.sina.com.cn/pic/621e24e2tx6CICG6CRZ5b)
                        IsLabelAutoFit                  轴上的标签自动调整

- LabelAutoFitMaxFontSize         轴上标签自适应字体大号
- LabelAutoFitMaxFontSize         轴上标签自适应字体小号
- LabelStyle.Angle                标签显示角度
- LabelStyle.IsEndLabelVisible    最后一个标签是否显示     
- 其他属性自己试

​    我的Interval这里设置都是NotSet，没有设置Auto，为什么，自己试就明白了。

​                  [![C# Chart控件，chart、Series、ChartArea曲线图绘制的重要属性](http://s2.sinaimg.cn/mw690/621e24e2tx6CICHYGYN71&690) ](http://photo.blog.sina.com.cn/showpic.html#blogid=621e24e20101cp64&url=http://album.sina.com.cn/pic/621e24e2tx6CICHYGYN71)
                        TextOrientation             轴的标题方向

- Title                       轴的名字，X轴是时间轴，Title就是时间

其他属性自己试，简单

​                  [![C# Chart控件，chart、Series、ChartArea曲线图绘制的重要属性](http://s8.sinaimg.cn/mw690/621e24e2tx6CIweiudF17&690) ](http://photo.blog.sina.com.cn/showpic.html#blogid=621e24e20101cp64&url=http://album.sina.com.cn/pic/621e24e2tx6CIweiudF17)
                       IntervalAutoMode             间隔是固定值还是随着轴变化，自己试

​                     [![C# Chart控件，chart、Series、ChartArea曲线图绘制的重要属性](http://s16.sinaimg.cn/mw690/621e24e2tx6CICL2qJx8f&690) ](http://photo.blog.sina.com.cn/showpic.html#blogid=621e24e20101cp64&url=http://album.sina.com.cn/pic/621e24e2tx6CICL2qJx8f)
                      ScaleView                      数据视图，就是当前绘制展开的图！重要！
                      MinSizeType                    游标滚动类型

ScrollBar                      滚动条

​    ScaleView是数据视图，也就是当前绘制出图表的一个区域，如果用鼠标选择某个区域展开显示，新展开的就又是一个ScaleView，只把它想成当前显示的视图就好理解了。

​    ScrollBar就是游标，之前我们说的ChartArea.CursorX或Y是也是游标，这里的ScrollBar是滚动条，仔细看两者的属性不难发现，一个是选择区域，一个是拖拽滚动条查看所有数据。

[![C# Chart控件，chart、Series、ChartArea曲线图绘制的重要属性](http://s15.sinaimg.cn/mw690/621e24e2tx6CIDiMIGOce&690)](http://photo.blog.sina.com.cn/showpic.html#blogid=621e24e20101cp64&url=http://album.sina.com.cn/pic/621e24e2tx6CIDiMIGOce)

 

![C# <wbr>Chart控件，chart、Series、ChartArea曲线图绘制的重要属性](http://s4.sinaimg.cn/mw690/621e24e2tx6CICMWluH33&690) 

​                       这些属性都不是重点，自己试试吧，就是外观设计

​           [![C# Chart控件，chart、Series、ChartArea曲线图绘制的重要属性](http://s13.sinaimg.cn/mw690/621e24e2tx6CICOAWTOac&690)](http://photo.blog.sina.com.cn/showpic.html#blogid=621e24e20101cp64&url=http://album.sina.com.cn/pic/621e24e2tx6CICOAWTOac)

​       不多说了，需要网格的在这里设置就行，感觉设置完了很丑，不过各花入个眼，如下图，还不错哈

[![C# Chart控件，chart、Series、ChartArea曲线图绘制的重要属性](http://s13.sinaimg.cn/mw690/621e24e2tx6CICRSrYEfc&690)](http://photo.blog.sina.com.cn/showpic.html#blogid=621e24e20101cp64&url=http://album.sina.com.cn/pic/621e24e2tx6CICRSrYEfc)
             [![C# Chart控件，chart、Series、ChartArea曲线图绘制的重要属性](http://s11.sinaimg.cn/mw690/621e24e2tx6CIyULOwW8a&690)](http://photo.blog.sina.com.cn/showpic.html#blogid=621e24e20101cp64&url=http://album.sina.com.cn/pic/621e24e2tx6CIyULOwW8a)

​                                          简单不说
       别忘了，咱们还停留在ChartArea.Axis里呢，这仅是一个轴，有需要的别忘了设置其他的轴哦![C# <wbr>Chart控件，chart、Series、ChartArea曲线图绘制的重要属性](http://www.sinaimg.cn/uc/myshow/blog/misc/gif/E___6722EN00SIGG.gif)
[![C# Chart控件，chart、Series、ChartArea曲线图绘制的重要属性](http://s2.sinaimg.cn/mw690/621e24e2tx6CIDebH8J71&690)](http://photo.blog.sina.com.cn/showpic.html#blogid=621e24e20101cp64&url=http://album.sina.com.cn/pic/621e24e2tx6CIDebH8J71)

 

 