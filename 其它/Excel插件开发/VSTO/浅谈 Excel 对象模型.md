​	不论您采用何种方式来开发Excel应用程序，了解Excel对象模型尤其重要，这些对象是您与Excel进行交互的基石。据不完全统计，Excel的对象模型中有270多个对象及超过5000多个属性和方法。通过这些对象及方法，您可以充分利用Excel来定制化您的插件。

​	Excel的所有对象，事件，方法和属性在这里不可能全部介绍完。本文简要介绍一下Excel的整体文档对象模型，以及一些比较重要的，平常开发中需要频繁接触到的对象，属性，事件及方法，如Application，Range对象等，使您对Excel的整个结构有一个简单的了解。后面在编程中遇到问题了，您可以快速定位知道需要设置或者调用哪个对象及其方法，然后根据关键字到Google或者MSDN上方便查找。本文大部分内容参照MSDN上的这篇文章[Understanding the Excel Object Model from a .NET Developer's Perspective](http://msdn.microsoft.com/en-us/library/office/aa168292(v=office.11).aspx) 如果您对英文没有问题，建议您直接去MSDN看原文。

# 一 Excel 对象模型简介

​	在与Excel进行交互之前，了解Excel对象模型的整体结构非常重要，这使得我们对Excel有一种更整体全面的了解。下图是Excel的对象模型的整个层级结构。

[![Basic Excel Object Model ](http://images.cnitblog.com/blog/94031/201308/09010004-e972fdbf517d49f5a88b3b510a9f64e8.png)](http://images.cnitblog.com/blog/94031/201308/09010003-69c16358c88c470594d5098d13bf7bc3.png)

根据这个图，我们打开一个Excel，可以有一种非常直观形象的了解。

[![Excel Object Model Demo](http://images.cnitblog.com/blog/94031/201308/09010005-aef447d0b2a245229aacebc66efc7a20.png)](http://images.cnitblog.com/blog/94031/201308/09010004-cd91fffd93d748548fde7415aa812419.png)

图中可以看到，Excel对象模型基本模拟了UI界面：

- 一个Excel应用程序就是一个Application，全局的对象比如菜单，工具条都属于Application对象。
- 一个Application可以包含很多个Workbook（Workbooks）。具体而言就是，我们可以同时打开很多个工作簿（Workbooks），但某一时候只有一个工作簿（Workbook）处于编辑状态，这个工作簿叫做活动工作簿(ActiveWorkbook)；
- 一个Workbook可以包含很多个Worksheet(Worksheets)。具体而言就是，一个工作簿可以包含很多工作表(Worksheets)，某一时刻只有一个工作表(Worksheet)处于编辑状态，这个工作表称之为活动工作表（ActiveWorksheet）。
- 一个Workbook还可以包含很多Shapes对象。工作表中还可以包含一些图表，标记，注释，控件等，这些都是浮在Sheet页上的，这些统称为Shapes，其中我们接触的最多的是图表（Charts）。
- 一个WorkSheet可以包含很多个Range对象。具体而言，一个工作表里面有很多个单元格，单元格范围用Range表示，Range可以使一个单元格，也可以使多个单元格。单元格都是嵌入到Sheet页中的。

更详细地Excel的对象模型图，如下，图中灰色的部分存在于office.dll中所有Office应用程序中都存在的对象。

[![Excel Object Model](http://images.cnitblog.com/blog/94031/201308/09010006-db5d232cc85b4817baabecd0b07306f7.png)](http://images.cnitblog.com/blog/94031/201308/09010005-a6ce4064b932471daa39aeff54db472d.png)

 

​	以上是Excel文档对象模型的大概全部的对象模型。其中最重要的几个对象为Application，Workbook，Worksheet 和Range对象。下面就简单介绍下这些对象中的一些属性，方法及事件。

# 二 Application对象

​	Application是根对象，代表着Excel应用程序本身，一切Excel中的其他对象都有它直接或者间接创建。 您可以回想到前面我们在Shared Add-in项目中创建Excel菜单和工具条时接触到的对象。我们首先是在Connect方法中保存了 application对象，然后在该对象上创建了MenuBar和Toolbar。Application对象有一些熟悉，事件和方法，在我们编程中经常会用到，现在就稍微讲一下：

## 2.1 Application中控制Excel状态和显示的方法和属性

​	Application中控制Excel状态和显示的方法和属性有很多，表一中列出了常用的几个属性。有一个属性是需要重新启用后才可以生效的。

| 属性                      | 类型                | 说明                                                         |
| ------------------------- | ------------------- | ------------------------------------------------------------ |
| Cursor                    | XlMousePointer 枚举 | 获取或者设置鼠标手势的形状                                   |
| EditDirectlyInCell        | Boolean             | 获取或者设置是否可以直接在单元格里面对数据进行编辑，如果为false，则只能在公示栏中对数据进行编辑 |
| Interactive               | Boolean             | 获取或者设置用户是否可以通过鼠标或者键盘与Excel进行交互      |
| MoveAfterReturnDirection  | xlDirection枚举     | 设置当用户敲回车时，在 MoveAfterReturn属性设置为true的情况下，下一个单元格移动的位置，默认为向下。 |
| ScreenUpdating            | Boolean             | 设置屏幕刷新属性，当设置为True时，每一个单元格的刷新时都会刷新整个屏幕，一般地在编程时，为了提升速度，在代码处理的过程中禁止屏幕刷新，待数据填充完成之后，再开启屏幕刷新. |
| StandardFont              | String              | 获取或者设置Excel中显示的默认字体，重启后生效。              |
| StandardFontSize          | Long                | 获取或者设置Excel默认显示的字体大小，重启后生效。            |
| StartupPath (read-only    | String              | 返回Excel外接插件启动项的加载目录.                           |
| TemplatesPath (read-only) | String              | 返回Excel模板加载的路径，通常为Windows的特殊目录.            |
| DisplayAlerts             | Boolean             | 如果设置为true，在某些情况下，比如我们的代码删除一个sheet页，Excel会弹出提示框提醒用户。如果设置为false，则不显示提示框，Excel默认选择默认项。 |

​	上面列出的属性中，最可能用到的是ScreenUpdating属性，正确使用该属性能够大幅提高应用程序的性能。默认的，该属性为true，即每一次修改就会刷新整个界面，这会使得应用程序变慢，尤其是在往单元格填充大量数据的时候。所以一般的做法是，在填充数据之前保存ScreenUpdating属性，然后将ScreenUpdating属性设置为false，禁止屏幕刷新，然后填充数据，最后将之前保存的ScreenUpdating属性赋值回来。下面的代码演示了这一做法：

```
Boolean oldScreenUpdate = this.Application.ScreenUpdating;
try
{
    this.Application.ScreenUpdating = false;
    //to fill in a large range that time comsuming

}
finally
{
    this.Application.ScreenUpdating = oldScreenUpdate;
}
```

## 2.2 Application中返回的对象

​	从Application对象中可以获取很多有用的对象。如ActiveCell返回当前活动的单元格;ActiveChart,返回当前选中的活动的图表；ActiveSheet、ActiveWindows分别返回活动的Sheet页和窗口；Selection属性返回当前选中的对象，可能是Range，Worksheet或者是一个窗体；Workbooks，Sheets，Charts返回当前Excel中所有工作簿，工作表，图表的集合。

​	通常，我们接触最多的是Application对象的Workbooks属性，该对象是当前Excel打开的所有的工作簿文件。一个Workbook就是一个.xls或者.xlsx文件。下面简单讲解Workbooks对象。

- 创建一个新的workbook对象 通过Applicaition的Workbooks对象的Add方法可以创建一个新的工作簿。

```c#
// Create a new workbook object
Excel.Workbook wb = this.Application.Workbooks.Add(Type.Missing);
```

- 关闭所有的workbook对象 通过调用close对象可以关闭所有的工作簿。

```c#
// Close all workbooks
this.Application.Workbooks.Close();
```

- 打开一个Excel文件 通过Open方法可以打开一个本地的Excel文件，Open方法有很多定制化参数，如果不需要制定的话，传入Type.Missing即可。

```c#
// Open an exist workbook
Excel.Workbook wbOpenExistFile = this.Application.Workbooks.Open(
    "C:\\YourPath\\Yourworkbook.xls",
    Type.Missing, Type.Missing, Type.Missing, Type.Missing,
    Type.Missing, Type.Missing, Type.Missing, Type.Missing,
    Type.Missing, Type.Missing, Type.Missing, Type.Missing,
    Type.Missing, Type.Missing);
```

- 打开文本文件，数据库文件，XML文件

这些操作可以通过OpenText，OpenDatabase，OpenXml方法来实现，方法参数可能需要您详细指定。

- 返回指定的工作簿文件

有时候我们可能需要从当前的工作簿文件中，找到指定的工作簿文件进行操作。一般的我们可以通过Workbooks属性通过索引器传入index来返回，或者通过工作簿名称来返回。需要注意的是，工作簿没有保存前，不需要后缀，保存后需要带上后缀来进行访问，代码如下：

```c#
//Get an exist workbook form current workbooks
Excel.Workbook wbFind =  this.Application.Workbooks[1];
// Before Book1 is saved:
wbFind =  this.Application.Workbooks["Book1"];
// After Book1 is saved:
wbFind =  this.Application.Workbooks["Book1.xls"];
```

## 2.3 Application中的方法

Application对象提供了一些方法，包括单元格的重新计算，撤销操作等。

- Calculate方法：该方法强制所有打开的工作簿，特定的工作簿，或者指定的Range对象进行重新计算。

```c#
//  Cell calculate
this.Application.Calculate();
// Or...
this.Application.Calculate();
// Or...
this.Application.get_Range("A1", "B12").Calculate();
```

- Quit方法:如果要退出Excel，则可以调用Quit方法，如果DisplayAlerts设置为false，则不会弹出提示用户保存的对话框。
- Undo：撤销用户界面上的最后一次操作，该撤销操作对代码执行的操作不起作用，并且只能撤销最后一次操作哦。

## 2.4 Application中文件操作方法

- DefaultFilePath 获取或者设置Excel默认加载和保存文件的路径
- DefaultSaveFormat 获取或者设置Excel默认保存的文件格式，该格式是XlFileFormat枚举类型的对象。
- RecentFiles 最近使用文件属性，返回一系列最近使用的文件名
- FileDialog 属性，该属性返回一个FileDialog对象，他能够处理四种类型的文件操作，包括：选择文件并打开，选择文件路径并保存当前工作簿，选择目录和选择文件名。使用Dialog窗体，我们可以利用Office提供的各种文件处理能力。其文件类型通过指定FileDialog类型来实现，该类型是一个msoFileDialogType枚举，包含msoFileDialogFilePicker，msoFileDialogFolderPicker，msoFileDialogOpen和msoFileDialogSaveAs四个枚举值。FileDialog对象存在于Microsoft.Office.Core命名空间中。FileDialog的Show方法弹出一个对话框，如果返回-1表示拥护点击了OK按钮，如果是0表示拥护按下了Cancel按钮，如果使用msoFileDialogOpen或者msoFileDialogSaveAs枚举值，FileDialog的Execute方法会执行打开或者保存文件的操作。SelectedItems属性包含了一些列的字符串，它表示选中的一些列文件名称。下面代码演示了如何使用。

```c#
//using FileDialog to open an exist file
Office.FileDialog dlg = this.Application.get_FileDialog(
    Office.MsoFileDialogType.msoFileDialogOpen);
dlg.Filters.Clear();
dlg.Filters.Add("Excel Files", "*.xls;*.xlw", Type.Missing);
dlg.Filters.Add("All Files", "*.*", Type.Missing);
if (dlg.Show() != 0)
    dlg.Execute();
```

## 2.5 Application中其他一些有用的对象

Application中还有一些其他有用的对象，如WorksheetFunction，该对象包括了一系列静态或者共享方法，这些方法都是对Excel内置函数的包装。

- WorksheetFunction 下面演示了WorksheetFunction的用法：

```c#
Excel.Worksheet ws = (Excel.Worksheet)this.Application.ActiveSheet;
Excel.Range rng = ws.get_Range("RandomNumbers", Type.Missing);
System.Random rnd = new System.Random();

for (int i = 1; i <= 20; i++)
    ws.Cells[i, 2] = rnd.Next(100);

rng.Sort(rng, Excel.XlSortOrder.xlAscending,
    Type.Missing, Type.Missing, Excel.XlSortOrder.xlAscending,
    Type.Missing, Excel.XlSortOrder.xlAscending,
    Excel.XlYesNoGuess.xlNo, Type.Missing, Type.Missing,
    Excel.XlSortOrientation.xlSortColumns,
    Excel.XlSortMethod.xlPinYin,
    Excel.XlSortDataOption.xlSortNormal,
    Excel.XlSortDataOption.xlSortNormal,
    Excel.XlSortDataOption.xlSortNormal);

Excel.WorksheetFunction wsf = this.Application.WorksheetFunction;
ws.get_Range("Min", Type.Missing).Value2 = wsf.Min(rng,
    Type.Missing, Type.Missing, Type.Missing, Type.Missing,
    Type.Missing, Type.Missing, Type.Missing, Type.Missing,
    Type.Missing, Type.Missing, Type.Missing, Type.Missing,
    Type.Missing, Type.Missing, Type.Missing, Type.Missing,
    Type.Missing, Type.Missing, Type.Missing, Type.Missing,
    Type.Missing, Type.Missing, Type.Missing, Type.Missing,
    Type.Missing, Type.Missing, Type.Missing, Type.Missing,
    Type.Missing);
```

- Windows对象 Application的Windows对象提供了对Excel窗体进行打开，关闭重新排列的方法。可以调用该对象的Arrange方法来对所有的窗体进行重新排列，我们需要指定XlArrangeStyle枚举：

```c#
// Arrange the windows
this.Application.Windows.Arrange(
  Excel.XlArrangeStyle.xlArrangeStyleTiled,
  Type.Missing, Type.Missing, Type.Missing);
```

- Name对象 该对象对应了Excel中的名称管理器，这些名称对应了一些Range对象，这在绘制图表，以及一些对函数公式长度有限制的地方很有用处，Application对象的Name属性返回了Excel中有所名字对象的集合。要创建命名Range对象，调用Names的Add方法即可。

```c#
//Add a name range
Excel.Name nm = this.Application.Names.Add(
"NewName", @"='Other Application Members'!$A$6",
Type.Missing, Type.Missing, Type.Missing,
Type.Missing, Type.Missing, Type.Missing,
Type.Missing, Type.Missing, Type.Missing);
```

后面使用该名称即可找到该名称代表的Range对象：

```c#
// Retrive a name Range
this.Application.get_Range("NewName", Type.Missing).Value2 = "Hello, World!";
```

## 2.6 Application对象中的事件

Application对象除了上面讲解的一些有用的方法和属性之外，还有一些事件。这些事件大致分为Sheet行为相关的事件、Window行为相关事件Workbook管理相关的事件。下面简要介绍这些事件的作用。

Sheet相关事件：

- SheetActive事件：当任意Sheet页变为活动工作表时触发。
- SheetClculate事件：当任意Sheet重新计算时触发，其参数包含了被重新计算的Object对象
- SheetChange事件：当工作步中，单元格的值发生改变时触发，参数中包含了发生变化的Range对象。
- SheetFollowHyperlink事件：当用户点击工作簿中的超链接时触发。参数中包含了包含超链接的Object对象，以及一个Hyperlink对象包含了需要跳转到的对象。
- SheetSelectionChange事件：当工作簿中的选择区域发生变化时触发。

以上application上的事件在Workbook类上也存在。application上的事件对所有的工作簿都有效，而Workbook上的这些事件仅对该Workbook有效。

Windows行为相关事件：

- WindowsActivate事件：当任意一个窗体被激活时触发。
- WindowsResize事件：当窗体大小发生改变时触发。

Workbook行为相关事件：

- NewWorkbook事件：当新的工作簿(workbook)被创建时触发。方法中包含新创建的Workbook类型的变量。
- WorkbookBeforeClose事件：在工作簿被关闭时触发，方法中传递了被关闭工作簿的对象，以及一个表示是否处理的Boolean型值。
- WorkbookBeforeSave事件：在工作簿保存时触发的事件。
- WorkbookNewSheet事件：在工作簿中创建新的工作表时触发的事件。
- WorkbookOpen事件：在工作簿被打开始触发的事件。

# 三 Workbook对象

Workbook对象也有很多属性和方法，下面仅介绍一些比较常用的方法和属性。

Workbook属性

- Name，FullName，Path：Name返回文件的名称，不好含路径；FullName返回包含路径的文件名称；Path返回文件所在的文件夹。
- Password：设置或者返回与该工作簿相关的密码。如果文档由密码保护，则HasPassword属性返回True，通过Password属性可以获取到密码，密码显示为“*****”。
- PrecisionAsDisplayed：如果为True，则Excel进行数值计算时，精度按照显示的精度来进行。如果为false(默认值)，则Excel将会按照所有可用的精度进行计算。
- ReadOnly：只读属性，如果为True，则标为只读。即不能对文档进行修改。
- Saved：获取或者设置保存工作簿的状态。如果用户对工作表的内容或者结构进行过修改，则该属性为True。在试图退出或者关闭Excel时，如果Application.DisplayAlerts为False时，会弹出提示框提示用户是否保存。但是如果将Saved属性设置为False，则Excel会认为您已经保存过，所以不会弹出提示框。

文档属性

Excel文档允许用户将一些信息保存到文件属性中。Excel提供了一些列内置的属性，我们也可以添加自己的属性。

 

[![Excel Document Property](http://images.cnitblog.com/blog/94031/201308/09010007-7ac63b578aef4166a877a23ea3ddd51a.png)](http://images.cnitblog.com/blog/94031/201308/09010007-ba05e69e871643c9b3f3b163160264de.png)

 

Workbook类的BuiltInDocumentProperties属性可以获取和设置那只的属性，CustomDocumentProperties可以获取和设置自定义属性。属性以键值对表示，我们可以使用属性的关键字或者Index来获取属性。下面的代码演示了获取所有的内置和自定义的属性，DumpPropertyCollection方法用来打印属性。

```c#
//Display the document property
private void DisplayDocumentProperties()
{
    Office.DocumentProperty prp = null;
    Office.DocumentProperties prps =
        (Office.DocumentProperties)
        this.Application.ActiveWorkbook.BuiltinDocumentProperties;

    Excel.Range rng = this.Application.
        get_Range("DocumentProperties", Type.Missing);
    int i = 0;

    try
    {
        this.Application.ScreenUpdating = false;

        try
        {
            // Set the Revision Number property:
            prp = prps["Revision Number"];
            prp.Value = Convert.ToInt32(prp.Value) + 1;

            // Dump contents of the collection:
            i = DumpPropertyCollection(prps, rng, i);
        }
        catch (Exception ex)
        {
            MessageBox.Show(ex.Message, this.Application.Name);
        }

        // Work with custom properties:
        try
        {
            prps = (Office.DocumentProperties)
                this.Application.ActiveWorkbook.CustomDocumentProperties;
            DumpPropertyCollection(prps, rng, i);
        }
        catch (Exception ex)
        {
            MessageBox.Show(ex.Message, this.Application.Name);
        }

        // Add a custom property:
        try
        {
            // Delete the property, if it exists.
            prp = prps["Project Name"];
            prp.Delete();
        }
        catch
        {
            // Do nothing if you get an exception.
        }
        try
        {
            // Add a new property.
            prp = prps.Add("Project Name", false,
                Office.MsoDocProperties.msoPropertyTypeString,
                "White Papers", Type.Missing);
        }
        catch (Exception ex)
        {
            MessageBox.Show(ex.Message, this.Application.Name);
        }
    }
    finally
    {
        this.Application.ScreenUpdating = true;
    }
}

private int DumpPropertyCollection(
    Office.DocumentProperties prps, Excel.Range rng, int i)
{
    foreach (Office.DocumentProperty prp in prps)
    {
        rng.get_Offset(i, 0).Value2 = prp.Name;
        try
        {
            if (prp.Value != null)
            {
                rng.get_Offset(i, 1).Value2 =
                    prp.Value.ToString();
            }
        }
        catch
        {
            // Do nothing at all.
        }
        i += 1;
    }
    return i;
}
```

一般地，我们可以将一些和文档相关的信息或者临时数据保存到自定义信息中。

文档样式

在Excel开发中，我们经常要对单元格进行格式化，这时，我们可能需要自定义一些样式，然后给其命名，然后下次直接按照名称赋给样式即可。

 

[![Excel Style Manager](http://images.cnitblog.com/blog/94031/201308/09010008-2c7d9a9d9c284938b0ccd00146c5674f.png)](http://images.cnitblog.com/blog/94031/201308/09010007-ef700e4b44f94ab3828f0e05a08e7f30.png)

我们可以通过Workbook的Styles属性来对这些文档样式进行添加，修改和删除。下面代码演示了如何创建或者修改一个样式：

```c#
// Apply Style
private void ApplyStyle()
{
    const String STYLE_NAME = "PropertyBorder";
    // Get the range containing all the document properties.
    Excel.Range rng = GetDocPropRange();
    Excel.Style sty;
    try
    {
        sty = this.Application.ActiveWorkbook.Styles[STYLE_NAME];
    }
    catch
    {
        sty = this.Application.ActiveWorkbook.Styles.Add(STYLE_NAME, Type.Missing);
    }

    sty.Font.Name = "Verdana";
    sty.Font.Size = 12;
    sty.Font.Color = ColorTranslator.ToOle(Color.Blue);
    sty.Interior.Color = ColorTranslator.ToOle(Color.LightGray);
    sty.Interior.Pattern = Excel.XlPattern.xlPatternSolid;
    rng.Style = STYLE_NAME;
    rng.Columns.AutoFit();
}
```

 

工作表对象

Workbook的Sheets属性返回该工作簿包含的所有工作表对象。这些对象可以是工作表也可以是Chart对象，下面的代码列出了当前工作簿中的所有对象。

```c#
// Show all the workSheet name in the active workbook
private void ListSheets()
{
    int i = 0;

    Excel.Range rng =
        this.Application.get_Range("Sheets", Type.Missing);
    foreach (Excel.Worksheet sh in this.Application.ActiveWorkbook.Sheets)
    {
        rng.get_Offset(i, 0).Value2 = sh.Name;
        i = i + 1;
    }
}
```

```
WorkSheet有一些很有用的属性和方法：
```

- Visible属性：该属性控制工作表的可见性：Visibility属性是一个XlSheetVisibility枚举类型，之分别为XlSheetHidden，XlSheetVeryHidden，XlSheetVisible。使用XlSheetHidden，允许用户通过Excel界面来显示工作表。而XlSheetVeryHidden，则需要使用代码来显示工作表。一般的，我们可以将一些临时数据存放到VeryHidden的工作表中，然后使用名字管理器或者直接地址来引用。下面代码展示了如何设置WorkSheet的Visible属性。

```c#
// Hide Worksheet
private void HideTheSheet()
{
    ((Excel.Worksheet)this.Application.ActiveWorkbook.Sheets[1]).Visible =
        Excel.XlSheetVisibility.xlSheetVeryHidden;
}
```

- Add方法：Add方法允许我们创建新的工作表。

```c#
Excel.Worksheet sh = this.Application.Sheets.Add(
    Type.Missing, Type.Missing, Type.Missing, Type.Missing);
```

- Copy方法：Copy方法允许我们对工作表进行整体拷贝。拷贝的时候，可以指定新工作表的位置，是位于某一个指定的工作表之前还是之后。下面的代码，将工作表1种的内容拷贝到第三个工作表之后的新建的工作表中。

```c#
//Copy Worksheet
((Excel.Worksheet) this.Application.ActiveWorkbook.Sheets[1]).
    Copy(Type.Missing, this.Application.ActiveWorkbook.Sheets[3]);
```

- Delete方法：该方法用于从工作簿中删除指定的工作表。
- FillAcrossSheets方法用于拷贝某个Sheet中的Range对象到该工作簿中的其他工作表中。可以指定一个区间，然后指定拷贝的方式，是拷贝数据，样式，还是所有的都拷贝。下面的代码演示拷贝名为Data的Range的数据及样式到该工作簿中的所有其他工作表中。

```c#
// Fill across sheet method
this.Application.ActiveWorkbook.Sheets.FillAcrossSheets(
    this.Application.get_Range("Data", Type.Missing),
    Excel.XlFillWith.xlFillWithAll);
```

- Move方法：Move方法和Copy方法类似。他将Sheet移动到某一个Sheet之前或者之后。下面的代码将第一个Sheet也移动到最后。

```c#
// move Worksheet
Excel.Sheets shts = this.Application.ActiveWorkbook.Sheets;
((Excel.Worksheet)shts[1]).Move(Type.Missing, shts[shts.Count]);
```

- PrintOut方法：该方法用于打印指定的对象，方法接受众多参数，包括，需要打印的页数，打印的份数，打印之前是否预览，打印机名称，是否打印到文件中，是否校对，指定打印的文件名称等。下面的例子展示了打印方法，该方法指定了纸打印第一页，打印两份，打印之前预览，并采用默认的打印机打印。

```c#
// print out method
((Excel.Worksheet)this.Application.ActiveWorkbook.Sheets[1]).
    PrintOut(1, 1, 2, true, Type.Missing, Type.Missing,
    Type.Missing, Type.Missing);
```

- PrintPreview方法：打印预览方法。
- Select方法：该方法将特定的对象选中。他会是的之前选中的对象失去选中状态。如果不想失去或者改变用户之前的选中的对象，而仅仅指向把该对象获得焦点，那么可以使用Active方法。

 

```
Workbook类的方法
```

Workbook代表一个工作簿，他也提供了很多方法，其中一些方法用来处理一些非常特殊的场景。和前面介绍其他对象一样，这里仅介绍我们在开发中会经常使用到的属性和方法。

- Active方法，该方法用来激活一个工作簿，并将该工作簿中的第一个工作表选中。

```c#
// Active a workbook
((Excel._Workbook)this.Application.Workbooks[1]).Activate();
```

- Close方法用来关闭一个工作簿，可以指定是否在关闭之前保存修改，如果该工作簿是新建的，没有保存过，您可以指定一个文件名。下面的代码演示了保存一个工作簿并放弃修改。

```c#
// Close a workbook without save changes
this.Application.Workbooks[1].Close(false,Type.Missing, Type.Missing);
```

- Protect和Unprotect方法：该方法用来保护和解除保护一个工作表不被用户添加或者修改，一般在自定义模板中用的比较多。方法可以指定密码，以及指定是否保存文档的结构，比如是否允许用户自由移动里面的工作表；指定是否工作簿的窗口需要保护。对工作簿进行保护并不能阻止用户编辑工作表里面的内容。 要保护工作表里面的内容，您需要对工作表Worksheets进行保护。使用Unprotect方法传递密码可以解除保护。下面的代码演示了如何对一个工作簿进行保护。

```c#
// Protect a workbook use password
this.Application.Workbooks[1].Protect("your password", Type.Missing, Type.Missing);
```

- Save方法，该方法用来对工作簿进行保存。如果是新建的工作簿，之前没有进行过保存，那么您应该调用SaveAs方法，传入方法路径加名称。如果没有保存过，调用Save方法的话，Excel会以创建时默认的工作簿名称以及在用户文档目录下保存文件。

```c#
// Save all open workbooks.
foreach (Excel.Workbook wb in this.Application.Workbooks)
{
    wb.Save();
}
```

- SaveAs方法，该方法比Save方法更复杂，能够允许保存指定的工作簿，能够设置工作簿的名称，文件格式，读写模式等。下面的代码演示了保存当前的工作表到一个特定的目录，格式为xml。需要注意的是，在调用SaveAs方法的时候，可能需要将Application.DisplayAlerts属性设置为false，因为在另存为某些其他格式的时候，可能会弹出交互界面需要进行一些其他的设置。比如说，将工作簿保存为XML格式的时候，Excel会提醒你会不会将工作簿中的VBA保存到XML格式中去。如果将Application.DisplayAlerts属性设置为false，则不会弹出提示框。

```c#
// Save as the active workbook
this.Application.ActiveWorkbook.SaveAs("C:\\MyWorkbook.xml",
    Excel.XlFileFormat.xlXMLSpreadsheet, Type.Missing,
  Type.Missing, Type.Missing, Type.Missing,
  Excel.XlSaveAsAccessMode.xlNoChange, Type.Missing,
    Type.Missing, Type.Missing, Type.Missing, Type.Missing);
```

- SaveCopyAs方法，该方法拷贝并保存某个文件的一个副本，部队当前在内存中打开的工作表产生影响。通常在我们需要对文件进行备份的时候很有用。但是需要注意的是，在保存或者拷贝的时候，如果没有设置Application.DisplayAlerts为false的时候，当Excel弹出保存提示框的时候，如果您点击取消，那么代码会抛出运行时异常。

```c#
// save a copy of the activeworkbooks
this.Application.ActiveWorkbook.SaveCopyAs("C:\\Test.xls");
```

 

# 四 Worksheet类

虽然Worksheet类也提供了大量的属性方法和事件，但是大部分的属性和方法和Application和Workbook类现相似，这部分重点介绍Worksheet中之前的对象中没有讲到过的，且经常会用到的属性和方法。

没有Sheet类

虽然Workbook对象有一个Sheets集合类，但是并不存在一个所谓的Sheet类，Sheets集合中的类要不是Worksheet元素，要么是Chart对象。可以认为Worksheet和Chart对象是Sheet类对象的实例，虽然公共的对象中并没有看到有Sheet类。

文档保护

通常Excel会对工作簿或者工作表提供一些保护特性，以不允许用户修改工作表中的队形。一旦我们开启了对工作表进行保护，除非进行取消保护，否则用户不能编辑或者修改工作表。在用户界面上，您可以通过菜单审阅-> 保护工作表菜单开启，我们可以设置保护密码。默认情况下，会对所有的工作表中的单元格进行保护。如果您要对特定范围的单元格进行保护，可能需要使用 审阅->允许用户编辑区域实现。

 [![Excel workbook protection](http://images.cnitblog.com/blog/94031/201308/09010009-0e62d9c2452241a1b4a9bf1d457c6381.png)](http://images.cnitblog.com/blog/94031/201308/09010009-b071357d0b6746b29fcc8f00cd0bf339.png)

在代码中，我们可以通过调用Worksheet的Protect方法来实现，该方法有很多参数进行配置。其方法签名如下：

```c#
// Worksheet protect method signature
WorksheetObject.Protect(Password, DrawingObjects, Contents,
  Scenarios, UserInterfaceOnly, AllowFormattingCells,
  AllowFormattingColumns, AllowFormattingRows,
  AllowInsertingColumns, AllowInsertingRows,
  AllowInsertingHyperlinks, AllowDeletingColumns,
  AllowDeletingRows, AllowSorting, AllowFiltering,
  AllowUsingPivotTables);
```

- Password参数，指定大小写敏感的保护密码，如果不设置，那么任何人都可以接触保护。
- DrawingObject参数，如果为true，则保护工作表内的图形对象，默认为false。
- Contents参数，如果为True则保护工作表中的所有单元格，默认为True，一般地，不需要进行修改。
- Scenarios参数，如果为True，则保护工作表内的方案，默认为True。
- UserInterfaceOnly，如果为True，则允许从代码中修改保护，而不是从用户界面上。默认值为False，即不能通过代码或者用户界面来对受保护的工作表进行修改。通常该修改只能对当前的会话有效。如果想要每一次都能对工作表进行操作，那么在每一次打开工作表的时候都需要通过代码进行设置。
- AllowFormattingCells参数，指定对工作表中对象的格式化权限。通常默认情况下，这些属性都是False。

下面是一个使用Protect方法对工作表进行保护的例子，该方法设置了保护密码，并仅允许对数据进行排序:

```c#
((Excel.Worksheet)this.Application.Sheets[1]).Protect(
"MyPassword", Type.Missing, Type.Missing, Type.Missing,
Type.Missing, Type.Missing, Type.Missing, Type.Missing,
Type.Missing, Type.Missing, Type.Missing, Type.Missing,
Type.Missing, true, Type.Missing, Type.Missing);
```

要取消保护，直接调用unprotect方法即可。

Object属性 

Worksheet对象还有几个返回Object类型的属性。

- Comments：在Excel中，我们可以在单元格中添加注释。我们可以通过Range对象的AddComment方法来实现：

[![Excel Document Property](http://images.cnitblog.com/blog/94031/201308/09010010-ac1c28b659034420980cb2688b755ee6.png)](http://images.cnitblog.com/blog/94031/201308/09010009-c7e674c468a040829188b368c9b4c6ec.png)

下面的代码演示了如果注释存在，删除，然后添加注释。后面演示了如何通过代码演示和现实所有注释：

```c#
Excel.Range rng = this.Application.get_Range("Date", Type.Missing);
if (rng.Comment != null)
{
    rng.Comment.Delete();
}
rng.AddComment("Comment added " + DateTime.Now);

// Display all the comments:
ShowOrHideComments(true);
```

Worksheet类提供了Comments属性，该属性返回一个Comments对象，该对象是一个集合，您可以便利该集合中的对象，Comment类提供的属性很少，用的最多的是Visible属性，用来显示或者隐藏注释；在一个就是Delete属性，用来删除注释，最后Text属性可以用来添加或者修改现有的注释。

添加完成注释之后，我们可能希望在工作表中显示注释。下面就是在当前活动工作表中显示或者隐藏注释的代码。

```c#
private void ShowOrHideComments(bool show)
{
    // Show or hide all the comments:
    Excel.Worksheet ws =
        (Excel.Worksheet)this.Application.Sheets["Worksheet Class"];

    for (int i = 1; i <= ws.Comments.Count; i++)
    {
        ws.Comments[i].Visible = show;
    }
}
```

# 五 Range对象

Range对象是在Excel开发中用的最多的队形，在我们对Excel进行操作之前，我们需要获取我们要进行操作的对象。几乎我们对工作表中的内容操作都会涉及到Range对象。Range对象是对工作表中内容的一种抽象，他可以表示一个单元格，一行数据，一列数据，一个选择的单元格区间，或者在不同工作表中的一系列对象。下图是Range的简要对象模型图：

[![Range Object Model](http://images.cnitblog.com/blog/94031/201308/09010010-50c0a2baa68f4b229a9a1c3d060a9cc3.png)](http://images.cnitblog.com/blog/94031/201308/09010010-e7aa39c2891f4357aec19f1b99a74a5f.png)

 

下面就从三个方面介绍Range对象

- 在代码中使用Range对象
- 在代码中对Range对象进行操作
- l通过Range对象来完成一些功能

对选中对象进行操作

虽然可以对当前选中的对象进行各种属性和行为的修改，但是最好避免这样做。Excel中的选中对象代表用户的选择。如果我们再代码中进行修改的话，会导致用户对当前选中的对象失去控制。首要准则是，只有当你试图更改用户的选择区域时，才去调用Range对象的Select方法。作为一个开发者，我们不应该因为该方法比较简单就去使用它。如果我们只想对这些用户选中的范围进行操作的话，通常有其他更好的选择。避免调用Select方法不仅能够使得我们的代码运行的更快，而且也能让用户更高兴使用我们的产品。

下面的代码用来清除用户当前单元格中的内容。

```c#
// clear select content
this.Application.ActiveCell.CurrentRegion.Select();
((Excel.Range)this.Application.Selection).ClearContents();
```

上面的代码会使得用户当前的选择区域丢失。如果之前只有一个单元格被选中，那么在运行上面的代码之后，整个连续的单元格都回被选中了。除非我们的目的就是这样，要选择整个Range返回内的单元格，一个更好的方法可能是：

```c#
this.Application.ActiveCell.CurrentRegion.ClearContents();
```

之前的代码通常是使用宏录制获得的，一般情况下，宏录制其会录制好用户的选择，然后对用户的选择进行修改。当我们对单个单元格或者多个单元格进行操作的时候，一般应该使用Range对象来表示我们操作的对象，而不是通过修改选中的对象来进行操作。如果确实需要修改用户的选择对象，可以使用Range.Select 方法。

在代码中引用Range对象

在开发中，Range对象的使用范围非常广泛和灵活。有时候Range对象表示单个的对象，有时候也表示一个集合。即使一个Range对象只表示一个对象，它也有Item和Count属性，所以我们要注意在有些情况下该如何更好地使用Range对象。

- Application 的ActiveCell属性，该属性返回一个Range对象，表示当前活动的单元格：

```c#
Excel.Worksheet ws = (Excel.Worksheet)this.Application.Worksheets[1];
Excel.Range  rng1, rng2;
rng1 = this.Application.ActiveCell;
```

- 通过其他对象的get_Range方法传入地址获取。

```c#
rng = ws.get_Range("A1", Type.Missing);
rng = ws.get_Range("A1:B12", Type.Missing);
```

- 通过Worksheet的Cells属性，传入行列号获取：

```c#
rng = (Excel.Range)ws.Cells[1, 1];
```

- 指定Range对象的区域边界； 可以通过range对象的Cells，Rows和Columns属性来返回另外一个Range对象。

```c#
rng = ws.get_Range("A1", "C5");
rng = ws.get_Range("A1", "C5").Cells;
rng = ws.get_Range("A1", "C5").Rows;
rng = ws.get_Range("A1", "C5").Columns;
```

- 通过名称管理器引用Range对象

```c#
rng = this.Application.get_Range("SomeRangeName", Type.Missing);
```

- 通过引用行或者列来获取Range对象

```c#
rng = (Excel.Range)ws.Rows[1, Type.Missing];
rng = (Excel.Range)ws.Rows["1:3", Type.Missing];
rng = (Excel.Range)ws.Columns[3, Type.Missing];
```

- 通过对两个Range对象的求并集，返回新的Range对象

```c#
// C#
rng = this.Application.get_Range("A1:D4, F2:G5", Type.Missing);
// You can also use the Application object's Union
// method to retrieve the intersection of two ranges, but this
// is far more effort in C#:
rng1 = this.Application.get_Range("A1", "D4");
rng2 = this.Application.get_Range("F2", "G5");
// Note that the Union method requires you to supply thirty
// parameters: 
rng = this.Application.Union(rng1, rng2,
    Type.Missing, Type.Missing, Type.Missing, Type.Missing,
    Type.Missing, Type.Missing, Type.Missing, Type.Missing,
    Type.Missing, Type.Missing, Type.Missing, Type.Missing,
    Type.Missing, Type.Missing, Type.Missing, Type.Missing,
    Type.Missing, Type.Missing, Type.Missing, Type.Missing,
    Type.Missing, Type.Missing, Type.Missing, Type.Missing,
    Type.Missing, Type.Missing, Type.Missing, Type.Missing);
```

- 通过对两个Range对象的求交集，返回新的Range对象

```c#
rng = this.Application.get_Range("A1:D16 B2:F14", Type.Missing);
// You can also use the Application object's Intersect
// method to retrieve the intersection of two ranges. Note
// that the Intersect method requires you to pass 30 parameters:
rng1 = this.Application.get_Range("A1", "D16");
rng2 = this.Application.get_Range("B2", "F14");
rng = this.Application.Intersect(rng1, rng2,
    Type.Missing, Type.Missing, Type.Missing, Type.Missing,
    Type.Missing, Type.Missing, Type.Missing, Type.Missing,
    Type.Missing, Type.Missing, Type.Missing, Type.Missing,
    Type.Missing, Type.Missing, Type.Missing, Type.Missing,
    Type.Missing, Type.Missing, Type.Missing, Type.Missing,
    Type.Missing, Type.Missing, Type.Missing, Type.Missing,
    Type.Missing, Type.Missing, Type.Missing, Type.Missing);
```

- 通过对原始Range对象的取偏移，获取新的Range对象。对原始Range对象取便宜实用Offset函数实现

```c#
rng = (Excel.Range)ws.Cells[1, 1];
for (int i = 1; i <= 5; i++)
{
    rng.get_Offset(i, 0).Value2 = i.ToString();
}
```

- 通过Range对象的End属性，传入XlDirection参数，可以获取四个方向的边界的Range对象

```c#
Excel.Range rngLeft, rngRight, rngUp, rngDown;
rng = (Excel.Range)this.Application.Selection;
// Note that the Range.End property is parameterized, so 
// C# developers cannot retrieve it. You must call the 
// get_End method, instead:
// E3
rngRight = rng.get_End(Excel.XlDirection.xlToRight);
// A3
rngLeft = rng.get_End(Excel.XlDirection.xlToLeft);
// C1
rngUp = rng.get_End(Excel.XlDirection.xlUp);
// C5
rngDown = rng.get_End(Excel.XlDirection.xlDown);
```

- 通过EntireRow和EntireColumn属性来获取包含某一个特定Range对象的行和列的Range对象

操作Range对象

获得了Range对象之后，我们就可以对Range对象进行各种操作了。

- 自动填充 Range对象的AutoFill方法是的我们可以自动填充某一个区域。大多数的自动填充用于填充连续递增或者递减的值。我们可以设置递增的类型及方式。这些都通过XlAutoFillType 枚举类型来实现 (xlFillDays, xlFillFormats, xlFillSeries, xlFillWeekdays, xlGrowthTrend, xlFillCopy, xlFillDefault, xlFillMonths, xlFillValues, xlFillYears, or xlLinearTrend)。如果不设置自动填充类型，则默认为XlFillDefault，Excel会判断区域的数据类型采用默认的自动填充方式填充。下面的代码演示了如何自动填充区域。

```c#
private void AutoFill()
{
    Excel.Range rng = this.Application.get_Range("B1", Type.Missing);
    rng.AutoFill(this.Application.get_Range("B1:B5", Type.Missing),
        Excel.XlAutoFillType.xlFillDays);

    rng = this.Application.get_Range("C1", Type.Missing);
    rng.AutoFill(this.Application.get_Range("C1:C5", Type.Missing),
        Excel.XlAutoFillType.xlFillMonths);

    rng = this.Application.get_Range("D1", Type.Missing);
    rng.AutoFill(this.Application.get_Range("D1:D5", Type.Missing),
        Excel.XlAutoFillType.xlFillYears);

    rng = this.Application.get_Range("E1:E2", Type.Missing);
    rng.AutoFill(this.Application.get_Range("E1:E5", Type.Missing),
        Excel.XlAutoFillType.xlFillSeries);
}
```

- 对Range对象的查找 Range对象的查找方法允许我们在Range范围内查找特定的字符串。这个功能我们可以通过Range.Find方法实现。

[![Excel Find and Replace](http://images.cnitblog.com/blog/94031/201308/09010011-2da18157742a4b9684e19c0c88f1403b.png)](http://images.cnitblog.com/blog/94031/201308/09010011-f24a4d5b138a4fc48f00011312914ece.png)

Find方法有很多个参数，下面的代码演示了如何使用Find方法：

```
private void DemoFind()
{
    Excel.Range rng = this.Application.
        get_Range("Fruits", Type.Missing);
    Excel.Range rngFound;

    // Keep track of the first range you find.
    Excel.Range rngFoundFirst = null;

    // You should specify all these parameters
    // every time you call this method, since they
    // can be overriden in the user interface.
    rngFound = rng.Find("apples", Type.Missing,
        Excel.XlFindLookIn.xlValues, Excel.XlLookAt.xlPart,
        Excel.XlSearchOrder.xlByRows, Excel.XlSearchDirection.xlNext,
        false, Type.Missing, Type.Missing);
    while (rngFound != null)
    {
        if (rngFoundFirst == null)
        {
            rngFoundFirst = rngFound;
        }
        else if (GetAddress(rngFound) == GetAddress(rngFoundFirst))
        {
            break;
        }
        rngFound.Font.Color = ColorTranslator.ToOle(Color.Red);
        rngFound.Font.Bold = true;
        rngFound = rng.FindNext(rngFound);
    }
}
```

- 对Range对象排序 和Find方法一样，Range对象的Sort方法也有很多参数来帮助我们完成自定义排序

 

[![Excel Sort](http://images.cnitblog.com/blog/94031/201308/09010011-6503b705e86c432ca547463dd4ee1693.png)](http://images.cnitblog.com/blog/94031/201308/09010011-e1c484e793a441b6bae604ace90bfb70.png)

 

下面的代码演示了自定义排序：

```
private void DemoSort()
{
    Excel.Range rng = this.Application.
        get_Range("Fruits", Type.Missing);

    rng.Sort(rng.Columns[1, Type.Missing],
        Excel.XlSortOrder.xlAscending,
        rng.Columns[2, Type.Missing], Type.Missing,
        Excel.XlSortOrder.xlAscending,
        Type.Missing, Excel.XlSortOrder.xlAscending,
        Excel.XlYesNoGuess.xlNo, Type.Missing, Type.Missing,
        Excel.XlSortOrientation.xlSortColumns,
        Excel.XlSortMethod.xlPinYin,
        Excel.XlSortDataOption.xlSortNormal,
        Excel.XlSortDataOption.xlSortNormal,
        Excel.XlSortDataOption.xlSortNormal);
}
```

# 六 结语

​    要进行Excel开发，绕不开对Excel中对象模型的理解， 本文简要介绍了Excel中的对象模型，介绍了这些对象中比较重要的几个对象，Application，Workbook，Worksheet，Range对象，这些对象不论在何种Excel开发方式中，只要需要对Excel进行交互，都会使用的到，本文介绍了这四个对象中的一些常用的属性，方法及事件。他们之间有很多对象都有相同的属性方法或者事件，这篇文章主要是想让大家对Excel对象模型有一个简单的认识，具体全部的对象模型，大家可以直接到MSDN或者Google上面去查找，下一篇文章将会介绍Excel中比较核心的功能：自定义函数。