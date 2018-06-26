> 作者：TangHanF（GuoFu）
>
> 日期：2018年6月22日
>
> 说明：转载请注明出处，谢谢！🤝
>
> 联系方式：guofu_gh@163.com

[TOC]

# 公共代码封装

```C#
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using Microsoft.Office.Interop.Excel;
/****************************************************************************
*Copyright (c) 2018 Microsoft All Rights Reserved.
*CLR 版本： 4.0.30319.42000
*机器名称：GUOFUC62B
*命名空间：ExcelAddIn_刷新插件.interfaces.impl
*文 件 名：  VSTOCommon
*唯一标识：6cdd46a5-c7de-47e0-874a-6f0d18fe405c
*当前的用户域：GUOFUC62B
*创 建 人：  GuoF
*电子邮箱：guofu_gh@163.com
*创建时间：2018/6/22 下午7:34:29
*描述：
*****************************************************************************/

namespace ExcelAddIn_刷新插件.interfaces.impl
{
    public class VSTOCommon : VSTOInterface
    {
        private static VSTOCommon vSTOCommon;

        /// <summary>
        /// 获取VSTOCommon对象实例
        /// </summary>
        /// <returns></returns>
        public static VSTOCommon Instance
        {
            get
            {
                if (vSTOCommon == null)
                {
                    vSTOCommon = new VSTOCommon();
                }
                return vSTOCommon;
            }
        }

        /// <summary>
        /// 获取Application对象
        /// </summary>
        /// <returns></returns>
        public Application GetApplication => Globals.ThisAddIn.Application;

        /// <summary>
        /// 获取当前活动工作簿
        /// </summary>
        /// <returns></returns>
        public Workbook GetCurrentActiveWorkbook => Globals.ThisAddIn.Application.ActiveWorkbook;

        /// <summary>
        /// 获取当前活动单元表
        /// </summary>
        /// <returns></returns>
        public Worksheet GetCurrentActiveWorksheet => GetCurrentActiveWorkbook.ActiveSheet;

        /// <summary>
        /// 获取Range范围
        /// </summary>
        /// <param name="range">传入一个范围，例如："A1:B3"、"A1"</param>
        /// <returns></returns>
        public Range GetRange(string range) => GetApplication.Range[range];

        /// <summary>
        /// 获取Range范围
        /// </summary>
        /// <param name="rowIndex">行，例如:"A1"</param>
        /// <param name="colIndex">列，例如:"B1"</param>
        /// <returns></returns>
        public Range GetRange(string rowIndex, string colIndex) => GetApplication.Range[rowIndex, colIndex];



        /// <summary>
        /// 获取所有工作表。返回Excel.sheets对象，其中Excel.sheets中的每一个成员都是一个Excel.Worksheet对象。因此一般多对Excel.sheets进行遍历操作
        /// </summary>
        /// <returns> </returns>
        public Sheets GetWorksheets => GetApplication.Worksheets;

        /// <summary>
        /// 获取活动表中选择的区域。返回一个多维（二维）数组
        /// </summary>
        /// <returns></returns>
        public Range GetSelectRange => GetApplication.Selection;

    }
}
```



# VSTO外接应用程序

## 当前激活的工作簿

  ```c#
Excel.Workbook workBook = Globals.ThisAddIn.Application.ActiveWorkbook;
  ```

## 当前激活的工作表

 ```c#
 Excel.Worksheet workSheet =  workBook.ActiveSheet;
 ```

可对以上进行封装，方便使用：

```c#
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using Excel = Microsoft.Office.Interop.Excel;
namespace ExcelAddIn_刷新插件
{
    public class CommonExcelUtils
    {

        /// <summary>
        /// 获取当前激活的工作簿
        /// </summary>
        /// <returns></returns>
        public static Excel.Workbook getCurrentActiveWorkbook()
        {
            return Globals.ThisAddIn.Application.ActiveWorkbook;
        }

        /// <summary>
        /// 获取当前活动的工作表
        /// </summary>
        /// <returns></returns>
        public static Excel.Worksheet getCurrentWorksheet()
        {
            return getCurrentActiveWorkbook().ActiveSheet;
        }
    }
}
```

## 获取Excel所选区域

Ribbon类中：

```c#
Excel.Range rng;//声明一个Excel的单元格区域变量
rng = Globals.ThisAddIn.Application.Selection;//获得Excel所选区域
```

ThisAddIn类中：

```c#
Excel.Range rng;//声明一个Excel的单元格区域变量。
rng = this.Application.Selection;//获得Excel所选区域
```

二者其实就 Globals.ThisAddIn 的区别，即获取方式的不同。

## 自动设置列宽

> 自动调整列宽要保证单元格不能处于编辑状态，如果单元格处于编辑状态则会触发异常。
>
> EntireColumn的使用

```C#
private void button8_Click(object sender, RibbonControlEventArgs e)
{
    //选择区域自动调整列宽
    Excel.Range range = VSTOCommon.Instance.GetSelectRange;
    range.EntireColumn.AutoFit();

    //设定指定区域自动调整列宽
    Excel.Range range2 = VSTOCommon.Instance.GetRange("A1", "B3");
    range2.EntireColumn.AutoFit();
}
```

## 退出Excel单元的编辑状态

> 思路：模拟发送ESC按键。
>
> 经过测试，Globals.ThisAddIn.Application.SendKeys(object keys,[object wait])这个接口不生效：
>
> Globals.ThisAddIn.Application.SendKeys("{ESC}",true);
>
> 并未等待按钮结束。后改为：System.Windows.Forms.SendKeys.SendWait("{ESC}") 即可。

## 删除行

```c#
// 删除行
Excel.Worksheet sheet = VSTOCommon.Instance.GetCurrentActiveWorksheet;
//删除第二行
Excel.Range sel_row_range = sheet.Rows["2", Type.Missing];
//Excel.Range sel_row_range = sheet.Rows["2:2", Type.Missing];
sel_row_range.Delete(Excel.XlDeleteShiftDirection.xlShiftUp);
```

## 删除列

删除B列、C列：

```c#
Excel.Range range2 = VSTOCommon.Instance.GetRange("B:B,C:C");
range2.Delete();
```

## 合并单元格

> 合并单元的本质就是首先获取一个要进行合并的Range范围，然后执行Merge方法进行合并。

```c#
/// <summary>
/// 合并单元格
/// </summary>
/// <param name="startRow">开始点，例如：A1</param>
/// <param name="endCol">结束点，例如：C3</param>
public void MergeCells(string startRow, string endCol)
{
    //本质上就是获取一个Range范围，然后执行Merge方法进行合并
    Microsoft.Office.Interop.Excel.Range mergeRange = VSTOCommon.Instance.GetRange(startRow, endCol);
    mergeRange.Merge(Type.Missing);
}
```

调用：

```
VSTOCommon.Instance. MergeCells("A1","A3");//合并行
VSTOCommon.Instance. MergeCells("A1","C3");//合并列
```



## 获取所选区域数据

结合以上代码：

![](https://ws2.sinaimg.cn/large/006tKfTcly1fsnev91h0mj31f40ec3zz.jpg)

```c#
object[,] arr = rng.Value ;//返回一个二维数组
```

> ```
> arr:
> [1, 1]: "需求变更（新增）工作量统计表"
> [1, 2]: null
> [1, 3]: null
> [1, 4]: null
> [1, 5]: null
> [1, 6]: null
> [1, 7]: null
> [1, 8]: null
> [1, 9]: null
> [2, 1]: "序号"
> [2, 2]: "系统名称"
> [2, 3]: "变更编号"
> [2, 4]: "变更内容"
> [2, 5]: "原合同10%工作量约定"
> [2, 6]: "原合同10%工作量使用情况"
> [2, 7]: "新增变更工作量（超出10%部分）"
> [2, 8]: "分包价(单价*人月)"
> [2, 9]: "总包价(分包价*116%)"
> [3, 1]: 1
> [3, 2]: "xxxxx"
> [3, 3]: 1
> [3, 4]: "xxxxxx"
> [3, 5]: "xx0"
> [3, 6]: "xx1"
> [3, 7]: "xx2"
> [3, 8]: "xx3"
> [3, 9]: "xx4"
> ```
>
> 可以把数组[1,1]理解为Excel的第一行第一列数据，[3,9]理解为Excel的第三行第九列数据....



## 在Ribbon类中调用ThisAddIn类中的方法

只需要：`Globals.ThisAddIn.xxxx` 即可

## 工作表的Cells属性

> Cells利用两点进行单元格的定位。例如A5单元格，两种写法：
>
> Cells(5,1)或者Cells(5,"A")
>
> 当前激活的工作表.Cells[1,2] //表示选择第一个第二列的单元格

## 新增Sheet表

使用Worksheets对象的Add方法，

`dynamic Add(object Before, object After, object Count, object Type) `

**新增工作表在最后：**

> Globals.ThisAddIn.Application.Worksheets.Add(After: Globals.ThisAddIn.Application.Sheets[Globals.ThisAddIn.Application.Sheets.Count]); 

## 当前工作薄表1复制到一新建工作薄中

> Application.ActiveWorkbook.Sheets[1].Copy();    

## 当前工作薄表1复制到表1的前面    

> Application.ActiveWorkbook.Sheets[1].Copy(Application.ActiveWorkbook.Sheets[1]); 

## 当前工作薄表1复制到表1的后面

> Application.ActiveWorkbook.Sheets[1].Copy(missing,Application.ActiveWorkbook.Sheets[1]); 

## 删除工作表1

> this.Application.ActiveWorkbook.Sheets[1].Delete();

有提示框提示，如果不需要提示，加上Application.DisplayAlerts = false;只是别忘了删后要改回来，且在这种情况下被删的表不得为Activesheet. 

## 选择第一张表 

> this.Application.ActiveWorkbook.Sheets[1].Select(); 

## 移动工作表

> this.Application.ActiveWorkbook.Sheets[1].Move(this.Application.ActiveWorkbook.Sheets[3]); 

## 隐藏工作表

> this.Application.ActiveWorkbook.Sheets[1].Visible = 0;//隐藏工作表，=-1显示，=2深度隐藏

## 操作Range

> 有关Range的操作基本是频率比较高的操作，像获取数据、设置数据、拷贝数据、粘贴数据等。

获取ActiveSheet单元格A2的值有以下等等方式：

```c#
Excel.Worksheet sht = Globals.ThisAddIn.Application.ActiveWorkbook.ActiveSheet;
var s = sht.Range("a2").Value;
var s = sht.Range("a1").Offset(1,0).Value;
var s = sht.Cells(2,"a").Value;
var s = sht.Cells(2, 1).Value;
var s = sht.Range("a2").Value;
var s = sht.Cells(1, 1)(2,1).Value;
```

​	由于C#是强类型的语言，变量必须声明类型，但单元格中的值却有文本、数字等，所以这里的变量s定义为var（也可为object）。可见，单元格的表示与VBA中相比，只是要在前面加点东西就成了，其余都一样，如下面的选择单元格：

## 选择单元格（单个、多个、多列）

```c#
sht.Cells[2, 3].Select();//选择行2列3的单元格，即C2单元格
sht.Range["d3:J8"].Select();//选择D3开始，J8结尾的区域
sht.Range["d:J"].Select();//选择D到J列
```

## 复制粘贴单元格

```c#
sht.Range["d3:e3"].Copy(sht.Range["d6"]); //拷贝并粘贴。将D3：E3区域的数据拷贝到D6为起点的区域（自动扩充） 

sht.Range["d3:e3"].Copy();//仅仅拷贝数据。拷贝D3:E3区域数据到内存
sht.Range["a6:b8"].Select();//选择A6:B8的区域
sht.Paste();//然后将数据粘贴到该区域


sht.Range["h6:i6"].Select();
sht.Paste();
```

## 单元格区域写进数组、数组写回单元格

```c#
var  ar = sht.Range["d3:e3"].Value;
```

或

```c#
object[,] ar = sht.Range["d3:e3"].Value; 
sht.Range["d5:e5"].Value =ar;
```

## 给Range区域赋值

```c#
Excel.Range range = Globals.ThisAddIn.Application.Range["A1:B3"];

string[,] arr = new string[,] { { "姓名", "性别" }, { "张三", "男" }, { "李丽", "女" } };

range.Value = arr;
```

也可以：

```c#
range.Value="数据"
```

但是这样range区域就会被“数据填充”

--------







## 方法/属性

### Application

#### 方法

##### Range/get_Range方法

> get_Range方法属于Application级别的方法，表示选取一个范围（注意，一个单元格也属于一个范围）。
>
> get_Range("A1")：表示选取A1这一个区域
>
> get_Range("A1","B5")：表示选取A1到B5这片区域

注意，get_Range方法属于Application父类（_Application）的方法，可用Range属性代替，例如：Application.Range["A1","B4"];

```c#
Excel.Range range = Globals.ThisAddIn.Application.get_Range("a1");

int i = 0;
Excel.Range rng = Globals.ThisAddIn.Application.get_Range("a1");  
foreach (Excel.Worksheet sht in Globals.ThisAddIn.Application.Worksheets)
{
     rng.get_Offset(i++, 0).Value = sht.Name; 
}

// 以上代码实现将当前工作簿的所有sheet表名称插入到从A1开始的一列单元格中
```

![](https://ws1.sinaimg.cn/large/006tNc79ly1fsk1fukmjjj30o0110djb.jpg) 

> //Excel.Range range = Globals.ThisAddIn.Application.Range["A1", "B5"];
>
>    Excel.Range range = Globals.ThisAddIn.Application.Range["A1:B5"];

以上二者等效。



#### 属性

##### ActiveWorkbook 

> 当前处于激活或者活动状态的工作簿，返回`Excel.Workbook`对象：
>
> Excel.Workbook workboot = Globals.ThisAddIn.Application.ActiveWorkbook; 

-------

### WorkBook

#### 方法

##### 

#### 属性

##### ActiveSheet

> 当前处于激活或者活动状态的工作表，返回`Excel.Worksheet worksheet`对象：
>
> Excel.Worksheet worksheet = 当前活动工作簿.ActiveSheet 
>
> （如何获取当前活动工作簿参考上面Application的属性一节）

#### 方法

##### 

#### 属性

-------

### WorkSheet

#### 方法

#####  

#### 属性



-------

### Range

#### 方法

#####Select方法

> ##### 选择区域。
>
> Range.Select();

![](https://ws3.sinaimg.cn/large/006tNc79ly1fsk2h8pix1j30bs09cdga.jpg)

#### 属性

> 

---------

##  事件

其它部分事件参考：[《浅谈 Excel 对象模型.md》](https://github.com/TangHanF/ProjectRecord/blob/master/其它/Excel插件开发/VSTO/浅谈%20Excel%20对象模型.md)

### SheetSelectionChange事件

> 单元格选择改变事件。每次选择一个单元格触发该事件。

案例：点击单元格显示当前单元格的坐标位置

```c#
 public partial class ThisAddIn
    {
        private void ThisAddIn_Startup(object sender, System.EventArgs e)
        {

            this.Application.SheetSelectionChange += Application_SheetSelectionChange;
        }

        private void Application_SheetSelectionChange(object Sh, Excel.Range Target)
        {
            MessageBox.Show(Target.Address);
        }

        private void ThisAddIn_Shutdown(object sender, System.EventArgs e)
        {
        }

        #region VSTO 生成的代码

        /// <summary>
        /// 设计器支持所需的方法 - 不要修改
        /// 使用代码编辑器修改此方法的内容。
        /// </summary>
        private void InternalStartup()
        {
            this.Startup += new System.EventHandler(ThisAddIn_Startup);
            this.Shutdown += new System.EventHandler(ThisAddIn_Shutdown);
        }
        
        #endregion
    }
```

![](https://ws3.sinaimg.cn/large/006tNc79ly1fsk0ua8pbhj30nc0iyjsz.jpg)

### SheetChange事件



> Application.EnableEvents = false
>
> Application.EnableEvents = true
>
> 可以控制是否响应相关事件