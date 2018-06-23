一.Range属性

1.选择单个单元格(例如A5)

​              Range("A5").Select

2.选择一个单元格区域(例如A6:A10)

​              Range("A6:A10").Select

3.选择一些不相邻的单元格(例如A1,B6,C8)

​              Range("A1,B6,C8").Select

4.选择一些不相邻的单元格和单元格区域(例如A11:D11,B7,C9)

​              Range("A11:D11,B7,C9").Select

二.Cells属性

1.选择单个单元格(例如A5)

​              Cells(5,1).Select                   Cells(5,A).Select

2.选择一个单元格区域(例如A6:A10)

​              Range(Cells(6,1),Cells(10,1)).Select

3.选择工作表中的所有单元格

​              Cells.Select

三.Offset属性

1.选择单元格A1下面一行和右边三列的单元格

​              Range("A1").Offset(1,3).Select

2.选择单元格D15上面两行和左边一列的单元格

​              Range("D15").Offset(-2,-1).Select

3.选择同列单元格(上一行)

​              ActiveCell.Offset(-1,0).Select

4.重新选取区域

​              ActiveCell.Offset(2,2).Resize(2,4).Select

四.END属性(移动到连续有内容的单元格)

1.选择任何行的最后一个单元格

​              ActiveCell.End(xlToRight).Select

2.选择任何行的最前一个单元格

​              ActiveCell.End(xlToLeft).Select

3.选择任何列的最后一个单元格

​              ActiveCell.End(xlDown).Select

1.选择任何列的最前一个单元格

​              ActiveCell.End(xlUp).Select