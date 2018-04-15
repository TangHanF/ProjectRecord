# 前言

> &nbsp;&nbsp;&nbsp;&nbsp;目前LayUI数据表格既美观有不乏一些实用功能。基本上表格应有的操作已经具备，LayUI作者【贤心】肯定是煞费苦心去优化，此处致敬。但是实话实话，如果单纯那数据表格功能来说，EasUI的数据表格更能更加强大、更加灵活，怎奈于丑的没法说，当然可以美化，但是成本太高了。我相信在后续的LayUI版本更新中，作者应该会着重优化数据表格，因为作为一个前端框架，美观度、效率相关、导航相关、数据展现相关无疑是最重要的。

# 操作说明

&nbsp;&nbsp;&nbsp;&nbsp;现在转入我们今天要说的数据表格相关操作。目前LayUI数据表格获取行数据的方式有如下方式（个人理解有限，不全之后望提醒）：

1. 表头加入checkbox列，用户选择一行或者多行数据后通过
``` javascript
var checkStatus = table.checkStatus('表格唯一ID值');
var data = checkStatus.data;
```

获取到相关行数据，其中 `data` 就是当前选中行的数据对象集合。具体参考： [点击此处直达](http://www.layui.com/demo/table/operate.html)

----
但是，如果说没有checkbox，没有行内工具条等设置，就一个常规表格，例如：

![](https://github.com/TangHanF/ProjectRecord/raw/master/前端/LayUI/img/多表头表格.png)

# 目标

- **要做到双击某一个单元格触发获取整行数据操作**，可以拿到当前行tr的DOM对象以及单元格td的DOM对象，以便利用Jquery进行操作，例如高亮显示单元格/行，更改字体颜色等等
- 能够根据相关条件进行数据筛选、进行高亮显示
- 能够获取某一个单元格数据，以及该单元格的DOM对象，以便利用Jquery进行操作，例如高亮显示单元格，更改字体颜色等等
- 能够动态隐藏指定列（实际作用可能不大，因为隐藏数据的话直接在定义`cols`时不定义即可，LayUI的table数据对象还是会指向你服务端返回的数据，即：**你服务端返回哪些字段，table数据容器会原封保留**，只是你不在`cols`定义的话不进行展示，但是数据还是有的），但是有时候可能也需要动态隐藏吧，所以保留了该功能

# 重点

> 相关逻辑写在table.render()方法的`done`回调中，例如：

```javascript
table.render({
    ....
    ,//详细的配置此处就不描述了
    ,....
    ,done:function(res, curr, count){
        // 此处写逻辑即可
    }
});
```



# 相关实现

- **表格数据**
[点击此处直达](https://github.com/TangHanF/ProjectRecord/blob/master/%E5%89%8D%E7%AB%AF/LayUI/data/data.json) 然后下载或者复制其内容自行新建文件即可。

- **JS实现**

新建JavaScript文件，例如新建一个`DataTableExtend.js`的文件，代码如下：
``` javascript
var LayUIDataTable = (function () {
    var rowData = {};
    var $;

    function checkJquery () {
        if (!$) {
            console.log("未获取jquery对象，请检查是否在调用ConvertDataTable方法之前调用SetJqueryObj进行设置！")
            return false;
        } else return true;
    }

    /**
     * 转换数据表格。
     * @param callback 双击行的回调函数，该回调函数返回三个参数，分别为：当前点击行的索引值、当前点击单元格的值、当前行数据
     * @returns {Array} 返回当前数据表当前页的所有行数据。数据结构：<br/>
     * [
     *      {字段名称1:{value:"当前字段值",cell:"当前字段所在单元格td对象",row:"当前字段所在行tr对象"}}
     *     ,{字段名称2:{value:"",cell:"",row:""}}
     * ]
     * @constructor
     */
    function ConvertDataTable (callback) {
        if (!checkJquery()) return;
        var dataList = [];
        var rowData = {};
        var trArr = $(".layui-table-body.layui-table-main tr");// 行数据
        if (!trArr || trArr.length == 0) {
            console.log("未获取到相关行数据，请检查数据表格是否渲染完毕！");
            return;
        }
        $.each(trArr, function (index, trObj) {
            var currentClickRowIndex;
            var currentClickCellValue;

            $(trObj).dblclick(function (e) {
                var returnData = {};
                var currentClickRow = $(e.currentTarget);
                currentClickRowIndex = currentClickRow.data("index");
                currentClickCellValue = e.target.innerHTML
                $.each(dataList[currentClickRowIndex], function (key, obj) {
                    returnData[key] = obj.value;
                });
                callback(currentClickRowIndex, currentClickCellValue, returnData);
            });
            var tdArrObj = $(trObj).find('td');
            rowData = {};
            //  每行的单元格数据
            $.each(tdArrObj, function (index_1, tdObj) {
                var td_field = $(tdObj).data("field");
                rowData[td_field] = {};
                rowData[td_field]["value"] = $($(tdObj).html()).html();
                rowData[td_field]["cell"] = $(tdObj);
                rowData[td_field]["row"] = $(trObj);

            })
            dataList.push(rowData);
        })
        return dataList;
    }

    return {
        /**
         * 设置JQuery对象，第一步操作。如果你没有在head标签里面引入jquery且未执行该方法的话，ParseDataTable方法、HideField方法会无法执行，出现找不到 $ 的错误。如果你是使用LayUI内置的Jquery，可以
         * var $ = layui.jquery   然后把 $ 传入该方法
         * @param jqueryObj
         * @constructor
         */
        SetJqueryObj: function (jqueryObj) {
            $ = jqueryObj;
        }

        /**
         * 转换数据表格
         */
        , ParseDataTable: ConvertDataTable

        /**
         * 隐藏字段
         * @param fieldName 要隐藏的字段名（field名称）参数可为字符串（隐藏单列）或者数组（隐藏多列）
         * @constructor
         */
        , HideField: function (fieldName) {
            if (!checkJquery()) return;
            if (fieldName instanceof Array) {
                $.each(fieldName, function (index, field) {
                    $("[data-field='" + field + "']").css('display', 'none');
                })
            } else if (typeof fieldName === 'string') {
                $("[data-field='" + fieldName + "']").css('display', 'none');
            } else {

            }
        }
    }
})();
```

- **调用**

完整示例：

``` html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <!--<script src="../../js/jquery-3.3.1.js"></script>-->
    <script src="../../js/layui.js"></script>
    <script src="DataTableExtend.js"></script>
    <link rel="stylesheet" href="../../js/css/layui.css" media="all">

    <script>
        (function () {
            layui.use(['table', 'layer'], function () {
                var table = layui.table;
                var layer = layui.layer;
                var $ = layui.jquery;
                table.render({
                    id: "tableID"// 设定表格的唯一ID进行标识
                    , elem: '#tableDataLoad'// 绑定table对应的元素
                    , height: 'full-300'
                    , url: 'data2.json' // TODO: 此处写你实际数据来源
                    , size: 'sm'
                    , page: true
                    , limits: [10, 20, 30, 40, 50]
                    , limit: 30
                    , cols: [[
                        {field: 'match_name', width: 93, align: 'center', title: '比赛名称', rowspan: 2}
                        , {align: 'center', title: '比赛信息', colspan: 3}
                        , {field: 'jingcai', width: 200, align: 'center', title: '竞猜项', rowspan: 2}
                        , {field: 'num', width: 100, align: 'center', title: '竞猜数量', rowspan: 2}
                    ]
                        , [
                            {field: 'match_time_beijing', width: 200, align: 'center', title: '比赛时间'}
                            , {field: 'match_master', width: 100, align: 'center', title: '主队'}
                            , {field: 'match_guest', width: 100, align: 'center', title: '客队'}
                        ]]
                    , done: function (res, curr, count) {// 表格渲染完成之后的回调

                        $(".layui-table th").css("font-weight", "bold");// 设定表格标题字体加粗

                        LayUIDataTable.SetJqueryObj($);// 第一步：设置jQuery对象

                        //LayUIDataTable.HideField('num');// 隐藏列-单列模式
                        //LayUIDataTable.HideField(['num','match_guest']);// 隐藏列-多列模式

                        var currentRowDataList = LayUIDataTable.ParseDataTable(function (index, currentData, rowData) {
                            console.log("当前页数据条数:" + currentRowDataList.length)
                            console.log("当前行索引：" + index);
                            console.log("触发的当前行单元格：" + currentData);
                            console.log("当前行数据：" + JSON.stringify(rowData));

                            var msg = '<div style="text-align: left"> 【当前页数据条数】' + currentRowDataList.length + '<br/>【当前行索引】' + index + '<br/>【触发的当前行单元格】' + currentData + '<br/>【当前行数据】' + JSON.stringify(rowData) + '</div>';
                            layer.msg(msg)
                        })

                        // 对相关数据进行判断处理--此处对【竞猜数量】大于30的进行高亮显示
                        $.each(currentRowDataList, function (index, obj) {
                             /*
                                * 通过遍历表格集合，拿到每行数据对象obj，通过obj["列名"]["row"]可以拿到行对象，obj["列名"]["cell"]可以拿到单元格对象
                                * */
                            if (obj['num'] && obj['num'].value > 30) {
                                obj['num']["row"].css("background-color", "#FAB000");// 对行（row）进行高亮显示
                                obj["num"]["cell"].css("font-weight","bold");// 对单元格（cell）字体进行加粗显示
                            }
                        })
                    }// end done


                });//end table.render

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


            });// end layui use
        })()
    </script>
</head>
<body>
<table id="tableDataLoad" lay-filter="demo"></table>

</body>
</html>
```

# 效果图展示

## 图一：获取行数据
![](https://github.com/TangHanF/ProjectRecord/raw/master/前端/LayUI/img/获取行数据.gif)

## 图二：对符合条件的行进行高亮显示
![](https://github.com/TangHanF/ProjectRecord/raw/master/前端/LayUI/img/对符合条件的行进行高亮显示.gif)

## 图三：隐藏列
![](https://github.com/TangHanF/ProjectRecord/raw/master/前端/LayUI/img/隐藏列.gif)