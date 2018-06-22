> 作者：TangHanF（GuoFu）
>
> 日期：2018年6月22日
>
> 说明：转载请注明出处，谢谢！🤝
>
> 联系方式：guofu_gh@163.com

[TOC]

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

## 在Ribbon类中调用ThisAddIn类中的方法

只需要：`Globals.ThisAddIn.xxxx` 即可

## 工作表的Cells属性

> 当前激活的工作表.Cells[1,2] //表示选择第一个第二列的单元格

 