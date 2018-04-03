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

    ```
        var checkStatus = table.checkStatus('tableID')
        var data = checkStatus.data;
    ```

- **数据表格列宽自适应出现横向滚动条的解决方案**
    1. 如果 table 是在 layui 的后台布局容器中（注意：不是在 iframe 中），在你的页面加上这段 CSS：

        ```
            .layui-body{overflow-y: scroll;}
        ```

    2. 如果 table 是在独立的页面，在你的页面加上这段 CSS：

        ```
            body{overflow-y: scroll;}
        ```
    > 总体而言，table 列宽自适应出现横向滚动条的几率一般是比较小的，主要原因是 table 的渲染有时会在浏览器纵向滚动条出现之前渲染完毕，这时 table 容器会被强制减少滚动条宽度的差（一般是 17px），导致 table 的横向滚动条出现。建议强制给你的页面显示出纵向滚动条。

# switch开关相关

- **switch开关必须放在form表单中，否则渲染失败，看不出效果**，例如：

    ```
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

    ```
        form.on('switch(filter)', function(data){
            console.log(data.elem); //得到checkbox原始DOM对象
            console.log(data.elem.checked); //开关是否开启，true或者false
            console.log(data.value); //开关value值，也可以通过data.elem.value得到
            console.log(data.othis); //得到美化后的DOM对象
        });  
    ```

    > 其中，filter需要自行定义lay-filter的值，例如：

    ```
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
    ```
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

    ```
    <input type="checkbox" id="isPrimaryKey" name="isPrimaryKey" value="true" lay-skin="switch" lay-filter="isPrimaryKey" lay-text="是|否">
    ```

# 下拉框相关

- **select下拉框通过设置 selected=""可以设置当前选择项，例如:**

    ```
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
    ```
        var selectArray = $("#selectContent").find("select");// 返回selectContent里面所有下拉框对象集合
    ```
    HTML：
    ```
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
        ```
        form.on('submit(formDemo)', function (data){

        });
        ```

    - 阻止表单提交后跳转
        ```
        form.on('submit(formDemo)', function (data){

            return false;// 只需要返回false即可
        });
        ```

# Tab相关
- **在子窗体动态为父窗体增加tab选项卡**
    > 简单的例子，父窗体已经创建好了选项卡，我们暂且使用官方提供的模板吧，然后再第一个选项卡加一个按钮，这个按钮就是触发弹窗的，然后弹窗加载一个html页面，这个页面里面再定一个按钮，叫做“动态增加选项卡”，然后点击这个按钮时父窗体的tab选项卡动态新增。

    父窗体html（简写）:

    ```
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
    ```
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
    ```
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
    ```
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




# 弹窗相关
- **机构弹出框选择的自定义行内操作按钮定义：**

    ```
        <script type="text/html" id="tableToolBar_tpl">
            <a class="layui-btn  layui-btn-xs" funName="{funName}" id="id_Choose" lay-event="InstitutionChoose">{btnName}</a>
        </script>
    ```

# 其它




    
