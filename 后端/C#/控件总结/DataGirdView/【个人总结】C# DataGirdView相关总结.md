# DataGirdView禁止拷贝

```c#
dataGridView1.ClipboardCopyMode = DataGridViewClipboardCopyMode.Disable;
```

DataGridViewClipboardCopyMode枚举类型如下：

```c#
    //
    // 摘要:
    //     定义常数，指示内容将复制从 System.Windows.Forms.DataGridView 控件添加到剪贴板。
    public enum DataGridViewClipboardCopyMode
    {
        //
        // 摘要:
        //     将复制到剪贴板上处于禁用状态。
        Disable = 0,
        //
        // 摘要:
        //     选定的单元格的文本值可以复制到剪贴板。 行或列标题文本是包含的行或列包含选定的单元格时，才 System.Windows.Forms.DataGridView.SelectionMode
        //     属性设置为 System.Windows.Forms.DataGridViewSelectionMode.RowHeaderSelect 或 System.Windows.Forms.DataGridViewSelectionMode.ColumnHeaderSelect
        //     和至少一个标题为选中状态。
        EnableWithAutoHeaderText = 1,
        //
        // 摘要:
        //     选定的单元格的文本值可以复制到剪贴板。 不包括标头文本。
        EnableWithoutHeaderText = 2,
        //
        // 摘要:
        //     选定的单元格的文本值可以复制到剪贴板。 标头文本是为了让所选单元格的行和列。
        EnableAlwaysIncludeHeaderText = 3
    }
```

