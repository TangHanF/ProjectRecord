**一、引言**

　　也许很多朋友都没有听说过VSTO这个东西的，本人之前也同样也不知道的，但是由于工作的原因接触了这方面，由于VSTO方面国内的资料比较少，本人刚开始学习的时候都是参考MSDN的，但是上面很多资料都是英文的，可能学习起来会比较慢点，所以本人把最近一段时间学习的内容记录下来，一来是作为一个巩固的学习笔记，二来希望这些博客可以帮助一些刚接触VSTO的朋友可以有所借鉴。

　　讲了这么多废话(指的上面一些过渡的话)，到底VSTO到底是什么呢?这里我简单的概括下的——**VSTO是微软推出一种对Office产品进行操作的技术，其中提供了一些类库来让开发人员可以更方便地开发出Office的解决方案,即对Word/Excel/Outlook实现一些扩展功能**。  在这个专题将为大家介绍下，如何创建Excel的解决方案?

**二、创建VSTO项目**

对于刚接触VSTO的朋友来说，可能根本就不知道如何去创建一个VSTO的项目的，相信通过这个部分大家就会觉得是如此的简单。

**环境的搭建**

进行VSTO开发的环境搭建是相当简单的，只需要安装Visual Studio 2010(当然安装VS2010的时候在安装组件中必须勾选VSTO选择，这个选项是默认勾上的。大家可以在安装VS的时候留意下)和Office 2010就可以，当然VS2008 和Office 2007的安装也可以完成环境的搭建。

**创建第一个Excel工程来开始我们的VSTO之旅**

第一步， 选择新建项目->Visual C#->Office->2010，然后选择Excel 2010外接程序(如何是英文版即Excel 2010 Add-in)，如下图：

![img](https://images0.cnblogs.com/blog/383187/201302/23220759-c42604d2422e4eb683cc57fc6054ef3d.png)

　　从图中可以看到，除了外接程序外，还有Excel模板和Excel文档这两种项目类型，他们的区别是 外接程序是应用程序级别的，即如果你创建了Excel 2010外接程序，该程序对所有Excel应用都是有效的，因为每次Excel的启动过程都会加载该插件(即该程序)，大家肯定留意到当我们启动Excel或Word的时候都会加载一些加载项，其实这些加载项就是属于外接程序，即插件，启动过程见下面图：

![img](https://images0.cnblogs.com/blog/383187/201302/23222129-46cf7b26e6c2471d8cc858b73558f68b.jpg)

　　而 文档和模板项目，都是属于文档级别的程序，该程序只对当前文档和模板有效，创建这两种类型的项目，会在项目的工程目录下会生成一个word文件(文档项目会生成一个 Document1.docx文件，模板项目会生成一个Document1.dotx文件)。

创建成功之后，外接程序的项目文件结构见下图：

![img](https://images0.cnblogs.com/blog/383187/201302/23222855-fcced69ff5544c3587d6ed13df18acdc.jpg)

　　从图中可以看出，刚创建的VSTO外接程序都只有一个ThisAddIn.cs文件，该文件即是一个宿主项(更多关于宿主项和宿主控件的内容可以查看该系列的[第一篇博文](http://www.cnblogs.com/zhili/archive/2012/09/03/VSTO.html))，我们可以通过这个文件来对Excel对象进行访问。同时该类中有ThisAddIn_Startup和ThisAddIn_Shutdown两个方法，从两个方法中命名中可以知道，如果你的代码想在加载外接程序时运行的话，就放把代码放在ThisAddIn_Startup方法内容，如果你想在外接程序卸载的时候运行你的代码，就把这些代码放在ThisAddIn_Shutdown方法内。

**三、Excel对象模型**

 要开发Excel的项目，就自然少不了对Excel对象模型的了解了，只有了解Excel对象模型，这样才能更好地对Excel进行处理。下面先给出一张Excel对象模型的图：

![img](https://images0.cnblogs.com/blog/383187/201302/23233257-d77c9b0060cf436f89f5d2e6da23142a.jpg)

 下面就具体对上图中的各个对象做一个简单的介绍：

Application对象——Excel中的[Application](http://msdn.microsoft.com/zh-cn/library/microsoft.office.interop.excel.application.aspx)对象表示Excel应用程序，该对象是所有Excel对象的根，你可以通过Application对象，获取到其他对象，在外接程序中，我们可以通过下面的方式来获得Application对象：Globals.ThisAddIn.Application

Workbooks对象代表Workbook对象的集合，而Workbook对象表示Excel中的单个工作簿，我们可以通过下面的方式来获得工作簿对象：Globals.ThisAddIn.Application.ThisWorkbook

Worksheets对象代表Worksheet对象的集合，而Worksheet代表的就是Excel中的表，下面的代码可以获得Worksheet对象：Globals.ThisAddIn.Application.ThisWorkbook.ActiveSheet (激活的表，每次打开一个Excel文件，都是表一即sheet1被激活，所以通过该代码就说获得表一对象)

Range对象代表一个范围，是操作Excel文档最常用的对象，它可以表示为一个单元格、一行、一列或多个单元格块（可以连续，也可以不连续）的单元格选定范围，甚至多个工作表中的一组单元格。可能上面的解释过于枯燥，相信大家通过下图可以更好地理解Excel中的各个对象：

![img](https://images0.cnblogs.com/blog/383187/201302/24000424-25c88a984c234ab3a75ccc598ed56a41.jpg)

**四、创建Excel外接程序**

介绍完了Excel对象模型之后，我们就可以利用这些对象来对Excel文档进行操作了，下面就创建一个简单的Excel外接程序的。

首先我们模拟一个需求，大多说软件在使用时都会弹出一个欢迎界面，这样我们就创建一个外接程序，每次打开Excel文件时弹出一个欢迎界面,退出时弹出“谢谢使用”界面。

 我们只需要在上面的创建工程中介入下面的代码即可：

![复制代码](https://common.cnblogs.com/images/copycode.gif)

```
using System.Windows.Forms;

namespace MyExcelAddIn1
{
    public partial class ThisAddIn
    {
        private void ThisAddIn_Startup(object sender, System.EventArgs e)
        {
            // 因为欢迎使用窗口要在打开Excel的时候弹出，所以把下面代码放在Startup方法内
            MessageBox.Show("欢迎使用Microsoft Excel");
        }

        private void ThisAddIn_Shutdown(object sender, System.EventArgs e)
        {
            // 在退出Excel的时候弹出谢谢使用窗口，所以把下面的代码放在Shutdown方法内
            MessageBox.Show("谢谢使用！");
        }

        #region VSTO generated code

        /// <summary>
        /// Required method for Designer support - do not modify
        /// the contents of this method with the code editor.
        /// </summary>
        private void InternalStartup()
        {
            this.Startup += new System.EventHandler(ThisAddIn_Startup);
            this.Shutdown += new System.EventHandler(ThisAddIn_Shutdown);
        }
        
        #endregion
    }
}
```

![复制代码](https://common.cnblogs.com/images/copycode.gif)

这样，我们就完成了上面简单的一个模拟需求了，下面让我们按F5来测试下效果吧！
按F5运行该程序时，首先打开一个Excel之后，一个欢迎界面就会弹出：

![img](https://images0.cnblogs.com/blog/383187/201302/24135640-66f8e92b83ce4ed284431c5435037528.jpg)

点击Excel窗口上的"X"按钮时，就会弹出一个 “谢谢使用！”的窗口，效果如下：

![img](https://images0.cnblogs.com/blog/383187/201302/24135843-a4c40298f67346de9508429d0c3b36cd.jpg)

点击 Ok 按钮之后才会正常退出Excel。这样就完成了一个简单的Excel外接程序了，上面提到过外接程序是应用程序级别的，所以当你每次打开Excel的时候都会有这样的一个欢迎界面和关闭Excel时都有一个"谢谢使用"窗口,有些朋友想问了，如果我想卸载这个插件怎么办呢？方法很简单，只需要右键你的解决方案——>清理，这样可以了，另外你也可以从开发工具选项卡——>COM 插件，在弹出的窗口中选择你自定义的插件 再按下移除按钮。具体步骤见下图：

![img](https://images0.cnblogs.com/blog/383187/201302/24141111-2fe7600cfd1342fba726ca18ccef9ece.jpg)

**五、创建Excel文档级自定义项**

介绍完了创建Excel外接程序之后，下面看看如何创建一个文档级的项目：

\1. 新建一个Excel 2010 Workbook(即Excel工作簿)项目：

![img](https://images0.cnblogs.com/blog/383187/201302/24141620-8612502a1db14639a4acb94f3dec2bb3.jpg)

\2. 单击 OK按钮，在下面的窗口中单击 ”OK“按钮：

![img](https://images0.cnblogs.com/blog/383187/201302/24141820-0b3f9c94a10b4d299b743703e8657b4e.jpg)

\3. 在第一创建Excel工作簿项目是会弹出下面的一个窗口（窗口意思为：是否允许创建的项目访问VBA项目系统），此时我们只需要点击“Ok”就完成了Excel工作簿项目的创建。

![img](https://images0.cnblogs.com/blog/383187/201302/24141950-507baf60981b49efaac0480373159074.jpg)

 现在我们来模拟一个需求，比如现在有一个成绩单工作表，我们希望获得各科目不及格同学的名字。此时我们只需要在上面创建的工作簿项目中添加一个ComboBox，一个Button，一个textbox。在button的Click事件中添加下面的代码：

![复制代码](https://common.cnblogs.com/images/copycode.gif)

```
 // 找出各科目不及格同学的名字
        private void btnSearch_Click(object sender, EventArgs e)
        {
            // 清除textbox中的内容
            txtResult.Clear();

            // 从复选框中获得选择的科目索引
            int subjectIndex = cbxsubjects.SelectedIndex;      
            if (subjectIndex == -1)
            {
                MessageBox.Show("请先选择一个科目");
                return;
            }

            // 获得选择的科目名称
            string subjectName = cbxsubjects.SelectedItem.ToString();
            // 获得工作表对象
            Excel.Worksheet worksheet =(Excel.Worksheet)Globals.ThisWorkbook.ActiveSheet;
           
            for (int row = 2; row < worksheet.UsedRange.Rows.Count+1; row++)
            {         
                Excel.Range rng =(Excel.Range)worksheet.Cells[row,subjectIndex + 2];
                Excel.Range rng1 = (Excel.Range)worksheet.Cells[row, 1];
                if (rng.Value< 60)
                {
                    txtResult.Text += rng1.Value + "; ";
                }
            }
            if (txtResult.Text.Length == 0)
            {
                txtResult.Text = subjectName + "没有不及格的同学";
            }
        }
```

![复制代码](https://common.cnblogs.com/images/copycode.gif)

运行该项目结果为：
![img](https://images0.cnblogs.com/blog/383187/201302/24171722-52dc9a452c9143179a7895c852b6d854.png)

**六、小结**

　　到这里本专题的介绍就结束了， 本专题首先主要介绍了Excel的对象模型和如何创建Excel的两种项目类型，希望通过本专题大家可以开发出一些简单的Excel的解决方案，后面一个专题将为大家介绍如何为Excel自定义一个选项卡和上下文菜单。

 专题源码：<http://files.cnblogs.com/zhili/ExcelWorkbook2.zip> 