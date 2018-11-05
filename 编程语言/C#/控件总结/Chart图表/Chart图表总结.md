![](https://ws2.sinaimg.cn/large/006tKfTcly1fsru7ucpf1j30xt0h1jut.jpg)

1. 一个chart可以包含多个chartArea。 chartArea是具体的坐标区域。
2. 每一个chartArea主要包含X轴，Y轴，副X轴(上方)，副Y轴(右方)，绑定的线条，绑定的图例。 
3. 线条可以有许多，只要将线条绑定到chartArea就可以在对应的chartArea显示。

其树形实体结构如下所示： 对于每个实体里面的许多样式属性可以自行尝试研究。

![](https://ws2.sinaimg.cn/large/006tKfTcly1fsru8tnm2dj30jv0auwfa.jpg)

综上可以对chart的结构有一个基本了解。接下来结合代码进行说明

# 线条的创建

此处用于创建4条线段。

```c#
public Series maxTemp;  
public Series avgTemp;  
public Series minTemp;  
public Series vibration;

maxTemp = new Series("maxTemp");  
avgTemp = new Series("avgTemp");  
minTemp = new Series("minTemp");  
vibration = new Series("vibration");
```

# 设置线条的样式

```c#
//曲线的颜色  
maxTemp.BorderColor = Color.Black;  
maxTemp.Color = Color.Red;  
avgTemp.BorderColor = Color.Black;  
avgTemp.Color = Color.Green;  
minTemp.BorderColor = Color.Black;  
minTemp.Color = Color.Blue;  
vibration.BorderColor = Color.Black;  
vibration.Color = Color.Blue;  

//曲线的宽度  
maxTemp.BorderWidth = 2;  
avgTemp.BorderWidth = 2;  
avgTemp.BorderWidth = 2;  
vibration.BorderWidth = 2;  

//曲线的样式  有圆形曲线，阶梯形曲线，折线等等。  
maxTemp.ChartType = SeriesChartType.Spline;      
avgTemp.ChartType = SeriesChartType.Spline;  
minTemp.ChartType = SeriesChartType.Spline;  
vibration.ChartType =SeriesChartType.Spline; 

//曲线的阴影样式  可以让曲线更加突出有立体感。  
maxTemp.ShadowOffset = 1;  
avgTemp.ShadowOffset = 1;  
minTemp.ShadowOffset = 1;  
vibration.ShadowOffset = 1;  

//标记的样式  设置曲线中每个数据点标记的样式。可以在标记中显示数据点的值，但是太多数据点的话将没有可视性
maxTemp.MarkerColor = Color.White;  
maxTemp.MarkerStyle = MarkerStyle.Square;  
avgTemp.MarkerColor = Color.White;  
avgTemp.MarkerStyle = MarkerStyle.Square;  
minTemp.MarkerColor = Color.White;  
minTemp.MarkerStyle = MarkerStyle.Square;  
vibration.MarkerColor = Color.White;  
vibration.MarkerStyle = MarkerStyle.Square;

//设置线条的轴类型   主要设置以下方做X轴还是上方做X轴，左方做Y轴还是右方做Y轴  
maxTemp.XAxisType = AxisType.Primary;  
maxTemp.YAxisType = AxisType.Primary;  
avgTemp.XAxisType = AxisType.Primary;  
avgTemp.YAxisType = AxisType.Primary;  
minTemp.XAxisType = AxisType.Primary;  
minTemp.YAxisType = AxisType.Primary;  
vibration.XAxisType = AxisType.Primary;  
vibration.YAxisType = AxisType.Primary; 

vibration.IsValueShownAsLabel = true;    //此属性将数据点的值作为标签。


```

# ChartArea的创建和属性设置

```c#
public ChartArea mainArea1 = new ChartArea("areaDTS");
public ChartArea mainArea2 = new ChartArea("areaDOVS"); 

//设置图表区域 用户可以拖动游标   此处设置后用户可以通过拖动游标放大查看区域 
//设置图表区域 用户可以拖动游标  
mainArea1.CursorX.IsUserEnabled = true;  
mainArea1.CursorY.IsUserEnabled = true;  
mainArea2.CursorX.IsUserEnabled = true;  
mainArea2.CursorY.IsUserEnabled = true;

//设置X Y 轴坐标的标题。  
mainArea1.AxisX.Title = "光纤分区号/(标量)";  
mainArea1.AxisY.Title = "温度值/(摄氏度)";  
mainArea2.AxisX.Title = "光纤震动位置/(m)";  
mainArea2.AxisY.Title = "震动值/(a.u.)";

//设置网格。主网格 与主刻度对应 副网格与副刻度对应，从刻度向另一端画一条线。如果线条中数据过多,产生较多的网格线会 使得整个区域过于密集，甚至为全黑色。所以在数据点较多的情况小关闭副网格，甚至主网格
mainArea1.AxisX.MajorGrid.Enabled = false;  
mainArea1.AxisY.MajorGrid.Enabled = false;  
mainArea1.AxisX.MinorTickMark.Enabled = false;  
  
mainArea2.AxisX.MajorGrid.Enabled = false;  
mainArea2.AxisY.MajorGrid.Enabled = false;  
mainArea2.AxisX.MinorTickMark.Enabled = false; 

//设置曲线横坐标值类型为时间类型
vibration.XValueType = ChartValueType.DateTime; 
//将此线条绑定到的AxisX的标签设置时间格式。  
mainArea1.AxisX.LabelStyle.Format = "MM-dd HH:mm";
//设置主刻度线和副刻度线 一般只有主刻度线才有对应标签值。  
mainArea1.AxisX.MinorTickMark.Enabled = true ;  
mainArea1.AxisX.MajorTickMark.Enabled = true;
```

# 创建图例、标题

 ```c#
//图例
Legend legend = new Legend(); 
ElementPosition p = new ElementPosition(0, 0, 12, 10); 
chart.Legends[0].Position = p;   //每创建一个对象都会存放在chart的集合属性中可以通过数组的形式随机访问

//标题
Title title = new Title("chart使用方法");  
chart.Titles.Add(title);  

 ```

# 将前面创建的对象加入到自己所属的父实体中

```c#
chart2.ChartAreas.Add(mainArea1);  //将线条加入到chart的chartAreas集合属性中  
chart2.ChartAreas.Add(mainArea2); 

series4.ChartArea = "areaDOVS";   //将线条绑定到对应ChartArea 通过chartArea的名字就可以绑定  
series3.ChartArea = "areaDTS";  

chart2.Series.Add(series3);       //将线条加入到chart的series集合属性中。  
chart2.Series.Add(series4);
```

# 示例效果

注意示例效果与前述代码无关，前述代码只为了说明

![](https://ws1.sinaimg.cn/large/006tKfTcly1fsrughdoy4j30wf0c00u7.jpg)



![](https://ws4.sinaimg.cn/large/006tKfTcly1fsruh5tcpwj318o0eljwe.jpg)

![](https://ws4.sinaimg.cn/large/006tKfTcly1fsruhdr9dyj31520ijgpv.jpg)





参考博客：[](https://blog.csdn.net/andrewniu/article/details/78770186)