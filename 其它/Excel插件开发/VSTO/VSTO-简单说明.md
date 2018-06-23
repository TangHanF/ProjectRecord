Tab
	Group



# 文档结构模型

![](https://ws3.sinaimg.cn/large/006tNc79ly1fshhjx6251j30h907pt8w.jpg)

![](https://ws3.sinaimg.cn/large/006tKfTcly1fsgazzb6dtj30m70elq5n.jpg)

Excel对象模型基本模拟了UI界面：

- 一个Excel应用程序就是一个Application，全局的对象比如菜单，工具条都属于Application对象。
- 一个Application可以包含很多个Workbook（Workbooks）。具体而言就是，我们可以同时打开很多个工作簿（Workbooks），但某一时候只有一个工作簿（Workbook）处于编辑状态，这个工作簿叫做活动工作簿(ActiveWorkbook)；
- 一个Workbook可以包含很多个Worksheet(Worksheets)。具体而言就是，一个工作簿可以包含很多工作表(Worksheets)，某一时刻只有一个工作表(Worksheet)处于编辑状态，这个工作表称之为活动工作表（ActiveWorksheet）。
- 一个Workbook还可以包含很多Shapes对象。工作表中还可以包含一些图表，标记，注释，控件等，这些都是浮在Sheet页上的，这些统称为Shapes，其中我们接触的最多的是图表（Charts）。
- 一个WorkSheet可以包含很多个Range对象。具体而言，一个工作表里面有很多个单元格，单元格范围用Range表示，Range可以使一个单元格，也可以使多个单元格。单元格都是嵌入到Sheet页中的。

更详细地Excel的对象模型图，如下，图中灰色的部分存在于office.dll中所有Office应用程序中都存在的对象：

![](https://ws3.sinaimg.cn/large/006tKfTcly1fskyhdmgggj30tf0mjtcd.jpg)

具体可参考：[《浅谈 Excel 对象模型.md》](https://github.com/TangHanF/ProjectRecord/blob/master/其它/Excel插件开发/VSTO/浅谈%20Excel%20对象模型.md)

--------

由于 Excel 文档中的数据已高度结构化，因此该对象模型是分层模型且非常简单。 Excel 提供数百个你可能需与之进行交互的对象，但你可以通过将重点放在非常小的一部分可用对象上来很好的开始了解对象模型。 这些对象包括以下四种：

- Application

- Workbook

- Worksheet

- Range

  许多使用 Excel 完成的工作都是围绕这四种对象及其成员进行的。

  

  > - Excel Application 对象表示 Excel 应用程序本身。 Application 对象公开了大量有关正在运行的应用程序、应用于该实例的选项以及在该实例内部开启的当前用户对象的信息。
  > - Workbook 对象表示 Excel 应用程序中的单个工作簿。Visual Studio 中的 Office 开发工具通过提供 `Workbook类型`来扩展 Workbook 对象。 此类型使你可以访问 Workbook 对象的所有功能
  > - Worksheet 对象是 Worksheets 集合的成员。 Worksheet 的许多属性、方法和事件与由 Application 或 Workbook 对象提供的成员相同或类似。**Excel 提供一个 Sheets 集合作为 Workbook 对象的属性**。 **Sheets集合的每个成员都是 Worksheet 或 Chart 对象**。Visual Studio 中的 Office 开发工具通过提供 `Worksheet类型`来扩展 Worksheet 对象。 此类型使你可以访问 Worksheet 对象的所有功能以及承载托管控件和处理新事件等新功能

  