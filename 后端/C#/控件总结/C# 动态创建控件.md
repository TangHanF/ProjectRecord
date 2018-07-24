一、添加GroupBox控件

 1.实例化并显示

```C#
//实例化GroupBox控件
GroupBox groubox = new GroupBox();
groubox.Name = "gbDemo";
groubox.Text = "实例";
//设置上和左位置
//groubox.Top = 50;
//groubox.Left = 50;
//通过坐标设置位置
groubox.Location = new Point(12, 12);
//将groubox添加到页面上
this.Controls.Add(groubox);
```

二、在GroupBox控件中添加TextBox控件

 1.实例化并显示

```C#
//实例化TextBox控件
TextBox txt = new TextBox();
txt.Name = "txtDemo";
txt.Text = "txt实例";
//将TextBox在GroupBox容器中显示
//txt.Parent = groubox;
//将TextBox在GroupBox容器中显示
groubox.Controls.Add(txt);
```

 

2.置于顶层和置于底层

 

```C#
//置于顶层
txt.BringToFront();

//置于底层
txt.SendToBack();
```

 

3.添加事件

 

```C#
//添加Click单击事件
txt.Click += new EventHandler(btn_Click);


//定义Click单击事件
private void btn_Click(object sender, EventArgs e)
{
MessageBox.Show("事件添加成功");
}
```

 

三、添加多个

1.动态添加多个

```C#
//添加控件
public void AddGroupBox() 
{
	string name = "gbox";
	for (int i = 0; i < 3; i++) 
	{
		GroupBox gbox = new GroupBox();
		gbox.Name = name + i;
		gbox.Text=name+i;
		gbox.Width = 300;
		gbox.Height = 100;
		gbox.Location = new Point(32, 20 + i * 150);
		this.Controls.Add(gbox);
		//调用添加文本控件的方法
		AddTxt(gbox);
	}
}
//添加文本控件
public void AddTxt(GroupBox gb) 
{
	string name = "txt";
	for (int i = 0; i < 3; i++) 
	{
		TextBox txt = new TextBox();
		txt.Name =gb.Name+ name + i;
		txt.Text =gb.Name+"|"+ name + i;
		txt.Location = new Point(12, 15 + i * 30);
		gb.Controls.Add(txt);
	}
}
```

 

实例：

```C#
using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Data;
using System.Drawing;
using System.Linq;
using System.Text;
using System.Windows.Forms;
namespace Select_ListBox 
{
	public partial class Form2 : Form 
	{
		TextBox txt = new TextBox();
		public Form2() 
		{
			InitializeComponent();
		}
		private void Form2_Load(object sender, EventArgs e) 
		{
			AddGroupBox();
			////实例化GroupBox控件
			//GroupBox groubox = new GroupBox();
			//groubox.Name = "gbDemo";
			//groubox.Text = "实例";
			////设置上和左位置
			////groubox.Top = 50;
			////groubox.Left = 50;
			////通过坐标设置位置
			//groubox.Location = new Point(12, 12);
			////将groubox添加到页面上
			//this.Controls.Add(groubox);
			////实例化TextBox控件
			//TextBox txt = new TextBox();
			//txt.Name = "txtDemo";
			//txt.Text = "txt实例";
			////将TextBox在GroupBox容器中显示
			////txt.Parent = groubox;
			////将TextBox在GroupBox容器中显示
			//groubox.Controls.Add(txt);
			////置于顶层
			//txt.BringToFront();
			////置于底层
			//txt.SendToBack();
			////添加Click单击事件
			//txt.Click += new EventHandler(btn_Click);
		}
		////定义Click单击事件
		//private void btn_Click(object sender, EventArgs e)
		//{
		//    MessageBox.Show("ss");
		//}
		//添加控件
		public void AddGroupBox() 
		{
			string name = "gbox";
			for (int i = 0; i < 3; i++) 
			{
				GroupBox gbox = new GroupBox();
				gbox.Name = name + i;
				gbox.Text=name+i;
				gbox.Width = 300;
				gbox.Height = 100;
				gbox.Location = new Point(32, 20 + i * 150);
				this.Controls.Add(gbox);
				//调用添加文本控件的方法
				AddTxt(gbox);
			}
		}
		//添加文本控件
		public void AddTxt(GroupBox gb) 
		{
			string name = "txt";
			for (int i = 0; i < 3; i++) 
			{
				TextBox txt = new TextBox();
				txt.Name =gb.Name+ name + i;
				txt.Text =gb.Name+"|"+ name + i;
				txt.Location = new Point(12, 15 + i * 30);
				gb.Controls.Add(txt);
			}
		}
	}
}
```

 

 

 