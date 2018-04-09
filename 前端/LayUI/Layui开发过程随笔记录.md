## ==========开发随笔==========

# 数据表格相关
- **表格顶部【删除已选】：$('.layui-btn[data-type="delSelected"]')**
- **分页的【确定】按钮：$(".layui-laypage-btn")**
- **数据表格内是否显示操作按钮控制开关**

    - `config.isShowInLineOperationTool=true|false`

- **数据表格内是否显示数据表格行内复选框按钮开关**

    - `config.isShowTableCheckbox = true|false`
- **对于数据表配置的加载时隐藏的字段可在js逻辑进行设置后强制显示：`config.forceShowField=["insId"]`,将要强制加载显示的id放在一个数组中即可** （注意:这是我自己项目相关的，可忽略）


- **数据表格table选择**

    ``` javascript
        var checkStatus = table.checkStatus('tableID')
        var data = checkStatus.data;
    ```

- **数据表格列宽自适应出现横向滚动条的解决方案**
    1. 如果 table 是在 layui 的后台布局容器中（注意：不是在 iframe 中），在你的页面加上这段 CSS：

        ``` css
            .layui-body{overflow-y: scroll;}
        ```

    2. 如果 table 是在独立的页面，在你的页面加上这段 CSS：

        ``` css
            body{overflow-y: scroll;}
        ```
    > 总体而言，table 列宽自适应出现横向滚动条的几率一般是比较小的，主要原因是 table 的渲染有时会在浏览器纵向滚动条出现之前渲染完毕，这时 table 容器会被强制减少滚动条宽度的差（一般是 17px），导致 table 的横向滚动条出现。建议强制给你的页面显示出纵向滚动条。

- **数据表格指定行高亮显示**

    目前好像layui可以设置列样式，没法直接指定行样式，但是可能又有些人有高亮显示某一行的需求但又无从下手。我的解决思路其实很简单，甚至是很基础：既然没有现成的相关属性（其实说实在，真不好设置属性，因为列可能是固定的，行可是动态的，不好定位），我们可以自己在数据表格渲染完成之后自己去根据相应条件设置行样式。

    - 数据表格的done回调事件（渲染完成的回调函数）
    - 利用jQuery设置相关行样式

    **示例：**
    ``` javascript
        table.render({
        id: "tableID"// 设定表格的唯一ID进行标识
        , elem: '#tableDataLoad'// 绑定table对应的元素
        , height: 'full-190'
        , url: 'data.json' // 数据源
        , size: 'sm'// 表格尺寸。sm （小尺寸）  lg （大尺寸）
        ,cols: [[ //表头
            {field: 'id', title: 'ID', width:80, sort: true, fixed: 'left'}
            ,{field: 'username', title: '用户名', width:80}
            ,{field: 'sex', title: '性别', width:80, sort: true}
            ,{field: 'city', title: '城市', width:80}
            ,{field: 'sign', title: '签名', width: 177}
            ,{field: 'experience', title: '积分', width: 80, sort: true}
            ,{field: 'score', title: '评分', width: 80, sort: true}
            ,{field: 'classify', title: '职业', width: 80}
            ,{field: 'wealth', title: '财富', width: 135, sort: true}
        ]]
        , done: function (res, curr, count) {// 表格渲染完成之后的回调

            $(".layui-table th").css("font-weight", "bold");// 设定表格标题字体加粗

            $($(".layui-table-body.layui-table-main tr")[2]).css("background-color","yellow")
            $($(".layui-table-body.layui-table-main tr")[3]).css("background-color","yellow")

            // 有固定列（fixed）的同步处理

            $($("div .layui-table-fixed.layui-table-fixed-l .layui-table-body tr")[2]).css("background-color","yellow")
            $($("div .layui-table-fixed.layui-table-fixed-l .layui-table-body tr")[3]).css("background-color","yellow")

            
            $($(".layui-table-body.layui-table-main tr")[6]).css("background-color","yellow")
            $($(".layui-table-body.layui-table-main tr")[7]).css("background-color","yellow")
            
            // 有固定列（fixed）的同步处理

            $($("div .layui-table-fixed.layui-table-fixed-l .layui-table-body tr")[6]).css("background-color","yellow")
            $($("div .layui-table-fixed.layui-table-fixed-l .layui-table-body tr")[7]).css("background-color","yellow")
        }
        });//end table.render
    ```

    #### 对以上样式处理进行封装：
    ``` JavaScript
    function dealLighthigh (rowIndexArr, bgColor) {
        $.each(rowIndexArr, function (index, val) {
            if (typeof val == "number") {
                $($(".layui-table-body.layui-table-main tr")[val]).css("background-color", bgColor ? bgColor : "yellow");
                $($("div .layui-table-fixed.layui-table-fixed-l .layui-table-body tr")[val]).css("background-color", bgColor ? bgColor : "yellow");
            } else if (typeof val == 'object') {
                $($(".layui-table-body.layui-table-main tr")[val.rowIndex]).css("background-color", val.bgColor ? val.bgColor : "yellow");
                $($("div .layui-table-fixed.layui-table-fixed-l .layui-table-body tr")[val.rowIndex]).css("background-color", val.bgColor ? val.bgColor : "yellow");
            }
        })
    }
    ```


    调用示例：
    ``` JavaScript
        dealHighLight([2, 3, 6, 7]);//指定要高亮显示的列，并且黄色高亮
        dealHighLight([2, 3, 6, 7],"red");//指定要高亮显示的列，并且红色高亮

        // 或者

        // 这种方式更加灵活，可以指定不同行的高亮颜色
        dealHighLight([
                {rowIndex: 2, bgColor: 'red'}, {rowIndex: 3, bgColor: 'red'},
                {rowIndex: 6, bgColor: 'yellow'}, {rowIndex: 7, bgColor: 'yellow'}
            ]
        );
    ```

    这的话对以上代码整理，实际应用为：
    ``` javascript
        table.render({
        id: "tableID"// 设定表格的唯一ID进行标识
        , elem: '#tableDataLoad'// 绑定table对应的元素
        , height: 'full-190'
        , url: 'data.json' // 数据源
        , size: 'sm'// 表格尺寸。sm （小尺寸）  lg （大尺寸）
        ,cols: [[ //表头
            {field: 'id', title: 'ID', width:80, sort: true, fixed: 'left'}
            ,{field: 'username', title: '用户名', width:80}
            ,{field: 'sex', title: '性别', width:80, sort: true}
            ,{field: 'city', title: '城市', width:80}
            ,{field: 'sign', title: '签名', width: 177}
            ,{field: 'experience', title: '积分', width: 80, sort: true}
            ,{field: 'score', title: '评分', width: 80, sort: true}
            ,{field: 'classify', title: '职业', width: 80}
            ,{field: 'wealth', title: '财富', width: 135, sort: true}
        ]]
        , done: function (res, curr, count) {// 表格渲染完成之后的回调

            $(".layui-table th").css("font-weight", "bold");// 设定表格标题字体加粗

                dealHighLight([2, 3, 6, 7]);//指定要高亮显示的列，并且黄色高亮
                dealHighLight([2, 3, 6, 7],"red");//指定要高亮显示的列，并且红色高亮

                // 或者

                // 这种方式更加灵活，可以指定不同行的高亮颜色
                dealHighLight([
                    {rowIndex: 2, bgColor: 'red'}, {rowIndex: 3, bgColor: 'red'},
                    {rowIndex: 6, bgColor: 'yellow'}, {rowIndex: 7, bgColor: 'yellow'}
                    ]
                );
        }
        });//end table.render
    ``` 


效果图：

![](https://github.com/TangHanF/ProjectRecord/raw/master/前端/LayUI/img/行高亮效果.png)




--------------
# switch开关相关

- **switch开关必须放在form表单中，否则渲染失败，看不出效果**，例如：

    ``` html
    <form class="layui-form" action="">
        <div class="layui-form-item">
            <label class="layui-form-label">开关</label>
            <div class="layui-input-block">
                <input type="checkbox" name="close" lay-skin="switch" lay-text="是|否">
            </div>
        </div>
    </form>
    ```

- **switch开关监听**

    ```  javascript
        form.on('switch(filter)', function(data){
            console.log(data.elem); //得到checkbox原始DOM对象
            console.log(data.elem.checked); //开关是否开启，true或者false
            console.log(data.value); //开关value值，也可以通过data.elem.value得到
            console.log(data.othis); //得到美化后的DOM对象
        });  
    ```

    > 其中，filter需要自行定义lay-filter的值，例如：

    ```  javascript
        <div class="layui-form-item">
            <label class="layui-form-label">主键</label>
            <div class="layui-input-block">
                <input type="checkbox" name="close" lay-skin="switch" lay-filter="isPrimaryKey" lay-text="是|否">
            </div>
        </div>
    ```
- **switch开关动态开关**

    > 注意点：需要form.render()进行重新渲染，官方文档开头就说的很清楚。但是我想很多人有时都忽略了重新渲染，包括我自己 哈哈。


    - 重要的事说三遍:
        - **凡是涉及到form表单里面的内容，通过js动态处理完必须进行`form.render`渲染**
        - **凡是涉及到form表单里面的内容，通过js动态处理完必须进行`form.render`渲染**
        - **凡是涉及到form表单里面的内容，通过js动态处理完必须进行`form.render`渲染**
    ```  javascript
        // 设置选中状态
        $("#isPrimaryKey").attr('checked','checked');

        // 重新渲染，以便生效。此处为了方便直接render了，没有添加类型参数，各位可根据实际情况填写。
        form.render();
    ```

- **switch开关状态判断问题**

    > 问题背景说明：页面有一个switch开关，叫做“是否开启通知”，发送了一条请求查询一下这个开关是否开始，例如这么判断：

        if ($(switch开关选择器).val() == entity[inputName]){
            $(this).attr("checked", "checked");
            layui.use("form", function () {
                var form = layui.form;
                form.render();
            });
        }

    实际上entity[inputName]返回值为“true”，但是这个if条件不成立，导致出现超出自己预期的结果。如果你好好看文档你会发现，在 [http://www.layui.com/doc/element/form.html#switch](http://www.layui.com/doc/element/form.html#switch)  有这么一句描述：

    > 设置value="1"可自定义值，否则选中时返回的就是默认的on

    所以，实际的if判断是：if("on"=="true")，这显然是不成立的。因此需要改动一下你的html，加一个 `value`属性，例如：

    ``` html
    <input type="checkbox" id="isPrimaryKey" name="isPrimaryKey" value="true" lay-skin="switch" lay-filter="isPrimaryKey" lay-text="是|否">
    ```


-------------
# 下拉框相关

- **select下拉框通过设置 selected=""可以设置当前选择项，例如:**

    ``` html
        <select>
            <option value="请选择表单类型..."></option>
            <option value="1" selected="">1</option>
            <option value="2">2</option>
            <option value="3">3</option>
        </select>
    ```

- **下拉框赋值**
    使用:`$("#下拉框ID值").val("数据")`即可，最后记得form.render()重新渲染一下。

- **通过jQuery的find方法返回的下拉框类型**
    
    返回值：`select-one`

    例如：

    JS：
    ```  javascript
        var selectArray = $("#selectContent").find("select");// 返回selectContent里面所有下拉框对象集合
    ```
    HTML：
    ``` html
        <div id="selectContent">
            <select id="id_ValiteType" name="valiteType">
                <option value="no">不验证</option>
                <option value="date">日期</option>
            </select>
        </div>
    ```

    ----
    这样 selectArray数组里面都是下拉框的对象，每一个对象的type值是：`select-one`，然后各位就可以通过类型判断各自发挥了。

# Form表单
- **表单提交监听**

    - 语法：`form.on('submit(filter)', callback)`

        例如：
        ```  javascript
        form.on('submit(formDemo)', function (data){

        });
        ```

    - 阻止表单提交后跳转
        ```  javascript
        form.on('submit(formDemo)', function (data){

            return false;// 只需要返回false即可
        });
        ```
------------------
# Tab相关
- **在子窗体动态为父窗体增加tab选项卡**
    > 简单的例子，父窗体已经创建好了选项卡，我们暂且使用官方提供的模板吧，然后再第一个选项卡加一个按钮，这个按钮就是触发弹窗的，然后弹窗加载一个html页面，这个页面里面再定一个按钮，叫做“动态增加选项卡”，然后点击这个按钮时父窗体的tab选项卡动态新增。

    父窗体html（简写）:

    ``` html
    <div class="layui-tab" lay-filter="tabDemo">
        <ul class="layui-tab-title">
            <li class="layui-this">网站设置</li>
            <li>用户管理</li>
            <li>权限分配</li>
            <li>商品管理</li>
            <li>订单管理</li>
        </ul>
        <div class="layui-tab-content">
            <div class="layui-tab-item layui-show">
                <button id="openChildWindow" class="layui-btn layui-btn-normal">弹窗</button>
            </div>
            <div class="layui-tab-item">内容2</div>
            <div class="layui-tab-item">内容3</div>
            <div class="layui-tab-item">内容4</div>
            <div class="layui-tab-item">内容5</div>
        </div>
    </div>
    ```
    父窗体js逻辑（简写）：
    ```  javascript
    $("#openChildWindow").click(function () {
        layer.open({
            type: 2,// 定义为iFrame弹出层
            title: "测试窗口，为父类动态添加tab",// 窗口标题
            shadeClose: true,//
            anim: 0,// 动画。0：平滑放大 1：从上掉落 2：从最底部往上滑入 3：从左滑入 4：从左翻滚 5：渐显 6：抖动
            maxmin: true, // 开启最大化最小化按钮
            shadeClose: false,// 是否点击遮罩关闭
            resize: true,// 是否允许拉伸
            content: "Child.html"// 内容（String/DOM/Array，默认：''）
            , end: function () {

            }
        });
    });
    ```
    --------------

    子窗体html（简写）：
    ```  javascript
    $("#btnAdd").click(function () {
        debugger
        window.parent.layui.element.tabAdd('tabDemo',  {
            title: '选项卡的标题'
            ,content: '选项卡的内容' //支持传入html
            ,id: '选项卡标题的lay-id属性值'
        });
    });
    ```
    
    子窗体js逻辑（简写）：
    ``` html
    <div class="layui-form-item">
        <div class="layui-input-block">
            <button class="layui-btn" id="btnAdd">动态增加选项卡</button>
        </div>
    </div>
    ```
    -------

**以上的重点就是：`window.parent.layui.element.tabAdd`**

- **为Tab选项卡加入：关闭当前、关闭其它、关闭所有操作**

    > 因内容较多，详细内容请移步：[点击此处查看](https://github.com/TangHanF/ProjectRecord/blob/master/%E5%89%8D%E7%AB%AF/LayUI/%E4%B8%BALayui%E7%9A%84Tab%E9%80%89%E9%A1%B9%E5%8D%A1%E5%A2%9E%E5%8A%A0%E5%85%B3%E9%97%AD%E5%BD%93%E5%89%8D%E3%80%81%E5%85%B3%E9%97%AD%E5%85%B6%E5%AE%83%E6%93%8D%E4%BD%9C.md)


------

# 弹窗相关
- **机构弹出框选择的自定义行内操作按钮定义：**

    ``` html
        <script type="text/html" id="tableToolBar_tpl">
            <a class="layui-btn  layui-btn-xs" funName="{funName}" id="id_Choose" lay-event="InstitutionChoose">{btnName}</a>
        </script>
    ```


-------
 # Layui数据存储
 **官方说明：**
 > - localStorage 持久化存储：layui.data(table, settings)，数据会永久存在，除非物理删除。
 >- sessionStorage 会话性存储：layui.sessionData(table, settings)，页面关闭后即失效。注：layui 2.2.5 新增

上述两个方法的使用方式是完全一样的。其中参数 table 为表名，settings是一个对象，用于设置key、value。下面与 layui.data 方法为例：
```  javascript
//【增】：向test表插入一个nickname字段，如果该表不存在，则自动建立。
layui.data('test', {
  key: 'nickname'
  ,value: '贤心'
});
 
//【删】：删除test表的nickname字段
layui.data('test', {
  key: 'nickname'
  ,remove: true
});
layui.data('test', null); //删除test表
  
//【改】：同【增】，会覆盖已经存储的数据
  
//【查】：向test表读取全部的数据
var localTest = layui.data('test');
console.log(localTest.nickname); //获得“贤心”
```

 **多值存储示例：**
 ```  javascript
 layui.data('cate', {
  key: 'data'
  ,value: [{
    key: 'id'
    ,value: 1
  },{
    key: 'name'
    ,value: 'abc'
  }]
});

//取值
var cate = layui.data('cate');
console.log(cate.data)
 ```

------

# Upload文件上传
## 注意点：
 1. 文件上传到服务端之后服务端根据处理情况返回一个响应结果，这个响应结果 **必须为合法的JSON字符串** ，例如：
``` JSON
{
  "code": 0
  ,"msg": ""
  ,"data": {
    "src": "http://cdn.layui.com/123.jpg"
  }
} 
```
## 多按钮上传判断是哪个按钮触发的文件选择上传操作

> 此问题由Fly社区的《intuition》网友提出，原帖地址：[点此直达](http://fly.layui.com/jie/24937/#item-1523254855403)

效果图：

![](https://github.com/TangHanF/ProjectRecord/raw/master/前端/LayUI/img/文件选择上传.gif)


该网友的问题描述为：
> 界面中需要两个选择文件的按钮，共同触发上传按钮，但是在choose中希望能够区分到底 是哪个选择文件按钮选择的文件，this.item在choose回调函数中似乎无法使用

同时给出的代码如下：

``` html
<div class="layui-form-item">
    <label for="L_repass" class="layui-form-label">附件</label>
    <div class="layui-input-block">
        <button class="layui-btn demoMore" id="test8" type="button">选择文件</button>
<span class="x-red" id="sFile1"></span>
    </div>
</div>
<div class="layui-form-item">
    <label for="L_repass" class="layui-form-label">预览附件</label>
    <div class="layui-input-block">
        <button class="layui-btn demoMore" id="test10" type="button">选择文件</button>
<span class="x-red" id="sFile2"></span>
    </div>
</div>
<div class="layui-form-item">
    <label for="L_repass" class="layui-form-label"></label>
    <button class="layui-btn" id="test9" type="button">开始上传</button>
</div>
```

``` javascript
layui.use('upload', function () {
    var $ = layui.jquery,
        upload = layui.upload;
    upload.render({
        elem: '.demoMore',
        url: 'FileUpload.ashx',
        auto: false,
        data: {
            desc: function () {
                return $("#desc").val();
            }
        },
        before: function () {
            alert($(this.item[0]).attr('id'));
        },
        choose: function (obj) {
            var files = obj.pushFile(); //将每次选择的文件追加到文件队列 
            alert(obj.length);
            obj.preview(function (index, file, result) {
                $("#sFile1").html(file.name);
            });
        }, multiple: true, number: 2, accept: 'file', bindAction: '#test9', done:
            function (res) {
                console.log(res)
            }
    });
});

```


其实主要问题在于choose回调的处理中，我将choose回调的代码调整如下：

``` javascript
, choose: function (obj) {
    var that = this;// 重新指定对象，防止下面调用时出现对象不一致问题

    var files = obj.pushFile(); //将每次选择的文件追加到文件队列
    obj.preview(function (index, file, result) {

        /* that.item可以获取到当前点击按钮对象
        *  正常思路的话按照DOM结构分析，当前按钮元素后面的元素应该是显示文件名的<span>标签，然后我们为当前按钮后面的span标签设置文本内容即可。
        *  但是实际上我们利用jquery的next方法获取到的是一个隐藏的input，因此直接next是定位不到想要的span标签的；
        *  于是决定用nextAll方法看看后面到底都啥，于是利用$(that.item).nextAll()获取到后面同类所有元素集合，发现span在集合索引值为1的位置，
        *  最后代码就是：
        * */
        $($(that.item).nextAll()[1]).html(file.name);// 利用jquery定位元素的方式可以再优化，请自行优化。此处仅仅是实现功能，尚未优化
    });
}
```


![](https://github.com/TangHanF/ProjectRecord/raw/master/前端/LayUI/img/that1.png)


![](https://github.com/TangHanF/ProjectRecord/raw/master/前端/LayUI/img/that_nextAll.png)


-----

# 其它
- **注意字符串类型的属性**
    例如：
    ```  javascript
    element.tabAdd('demo', {
        title: '选项卡的标题'
        ,content: '选项卡的内容' //支持传入html
        ,id: '选项卡标题的lay-id属性值'
    }); 

     element.tabChange('nav导航ID', "选项卡标题的lay-id属性值");            
      
    ```
    以上新增一个选项卡，新增完成要切换到选项卡，但是因为不小心用了数字作为id导致切换失败，代码如下：
    ```  javascript
    element.tabAdd('main-tab', {
        title: title,
        content: '<iframe id="' + 0 + '" src="' + url + '" class="layui-tab-iframe"></iframe>',
        id: 0
    });

    element.tabChange('main-tab', 0);
    ```
    改成：
    ```  javascript
    element.tabAdd('main-tab', {
        title: title,
        content: '<iframe id="' + 0 + '" src="' + url + '" class="layui-tab-iframe"></iframe>',
        id: "0"
    });

    element.tabChange('main-tab', "0");
    ```   
    之后就可以。所以，注意看文档！


    
