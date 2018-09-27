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
let LayUIDataTable = (function () {
    let rowData = {};
    let $;

    //配置项
    let LayUIDataTableConfig={
        isdblClick:true,// 是否支持行、单元格的双击事件（默认true）,如果为"false"，则默认只支持单击事件
        fixedColumnDBClick:true,// 固定列的标题是否可以触发双击（受限于"isdblClick"配置项是否开启，若"isdblClick"配置为false，则无意义）

    };

    function checkJquery() {
        if (!$) {
            console.log("未获取jquery对象，请检查是否在调用ConvertDataTable方法之前调用SetJqueryObj进行设置！")
            return false;
        } else return true;
    }

    /**
     * 转换表格，处理事件等
     * @param callback 双击行的回调函数，该回调函数返回三个参数，分别为：当前点击行的索引值、当前点击单元格的值、当前行数据
     * @returns {*} 返回当前表格的所有行数据对象集合。数据结构：<br/>
     * [
     *      {字段名称1:{value:"当前字段值",cell:"当前字段所在单元格td对象",row:"当前字段所在行tr对象"}}
     *     ,{字段名称2:{value:"",cell:"",row:""}}
     * ]
     * @constructor
     */
    function ConvertDataTable(callback) {
        let isExistFixColFlag = IsExistFiexColumn();
        if (!checkJquery()) return;
        let dataList = [];
        let trArr = GetTr();
        let trArrFiex = GetFiexColumnArr();

        if (!trArr || trArr.length == 0) {
            console.log("未获取到相关行数据，请检查数据表格是否渲染完毕！");
            return;
        }

        EachRowDealData(trArr, dataList, LayUIDataTableConfig.isdblClick, callback);

        if (isExistFixColFlag) {
            EachRowDealData(trArrFiex, dataList, LayUIDataTableConfig.isdblClick, callback);
        }
        return dataList;
    }

    /**
     * 判断是否存在固定列（左侧固定或者右侧固定任意一个出现即可）
     * @returns {boolean}
     * @constructor
     */
    function IsExistFiexColumn() {
        if (IsExistFiexColumnL() || IsExistFiexColumnR())
            return true;
        else
            return false;
    }

    /**
     * 是否存在左侧固定列
     * @returns {boolean}
     * @constructor
     */
    function IsExistFiexColumnL() {
        if ($(".layui-table-fixed.layui-table-fixed-l").length > 0)
            return true;
        else
            return false;
    }

    /**
     * 是否存在右侧固定列
     * @returns {boolean}
     * @constructor
     */
    function IsExistFiexColumnR() {
        if ($(".layui-table-fixed.layui-table-fixed-r").length > 0)
            return true;
        else
            return false;
    }


    /**
     * 获取行数据
     * @returns {*|jQuery|HTMLElement}
     * @constructor
     */
    function GetTr() {
        let trArr = $(".layui-table-body.layui-table-main tr");// 行数据
        return trArr;
    }

    /**
     * 获取固定列所属行的集合
     * @returns {*}
     * @constructor
     */
    function GetFiexColumnArr() {
        let trArr = [];
        let trArrTmp = [];
        if (IsExistFiexColumn) {
            if ($(".layui-table-fixed.layui-table-fixed-l").length > 0)
                trArr = $(".layui-table-fixed.layui-table-fixed-l tr");
            if ($(".layui-table-fixed.layui-table-fixed-r").length > 0) {
                trArrTmp = $(".layui-table-fixed.layui-table-fixed-r tr");
                //TODO 有优化空间
                $.each(trArrTmp, function (index, value) {
                    trArr.push(value);
                })
            }
            return trArr

        }
        else return null;
    }


    /**
     * 遍历每行并处理每一行处理，将其封装于对象中
     * @param trArr
     * @param dataList 返回数据集合对象（引用类型）
     * @param callback 回调
     * @returns {*}
     * @constructor
     */
    function EachRowDealData(trArr, dataList, isdblClick, callback) {
        if (!trArr) return;

        let fixedCol;
        let indexFixedColumn = 0;
        //TODO 有优化空间
        $.each(trArr, function (index, trObj) {
            let currentClickRowIndex;
            let currentClickCellValue;

            if (isdblClick) {
                $(trObj).dblclick(function (e) {
                    if(LayUIDataTableConfig.fixedColumnDBClick){
                        _click(e);
                    }
                    // 排除固定列标题行的点击事件
                    // let dataIndex = e.currentTarget.dataset.index;//如果是固定列的行标题，那么没有"data-index"属性，通过这一点进行判断
                    // if (dataIndex)
                    //     _click(e);

                });
            } else {
                $(trObj).click(function (e) {
                    _click(e);
                });
            }

            function _click(e) {
                let returnData = {};
                let currentClickRow = $(e.currentTarget);
                currentClickRowIndex = currentClickRow.data("index");
                currentClickCellValue = e.target.innerHTML
                $.each(dataList[currentClickRowIndex], function (key, obj) {
                    returnData[key] = obj.value;
                });
                e.cancelBubble = true;
                // layui.stope(e)
                callback(currentClickRowIndex, currentClickCellValue, returnData);
            }

            let tdArrObj = $(trObj).find('td');
            rowData = {};

            //  每行的单元格数据
            $.each(tdArrObj, function (index_1, tdObj) {
                let td_field = $(tdObj).data("field");
                if ($($(tdObj).find("div.layui-form-checkbox")).length > 0) {
                    rowData["checkbox"] = rowData["checkbox"] || {};
                    // rowData["fixedColumn"] = rowData["fixedColumn"] || {};

                    rowData["checkbox"]["checkbox"] = ($($(tdObj).find("div.layui-form-checkbox")).length > 0 ? $($(tdObj).find("div.layui-form-checkbox")) : undefined);
                    if (IsExistFiexColumn()) {
                        if (!fixedCol)
                            fixedCol = GetFiexColumnArr();
                        if (IsExistFiexColumnL())
                            rowData["fixedColumn_L"] = $(fixedCol[indexFixedColumn + 1]);
                        if (IsExistFiexColumnR()) {
                            rowData["fixedColumn_R"] = $(fixedCol[fixedCol.length / 2 + indexFixedColumn + 1]);
                        }
                        indexFixedColumn++;
                    }
                } else {
                    rowData[td_field] = rowData[td_field] || {};
                    rowData[td_field]["value"] = $($(tdObj).html()).html();
                    rowData[td_field]["cell"] = $(tdObj);
                    rowData[td_field]["row"] = $(trObj);
                }
                //$($(tdObj).find("div.layui-form-checkbox")).addClass("layui-form-checked")//选中
                //$($(tdObj).find("div.layui-form-checkbox")).hide()//隐藏
                //$($(tdObj).find("div.layui-form-checkbox")).show()//显示
            })
            dataList.push(rowData);
        })
        return dataList;
    }


    // 暴露对外访问的接口
    return {
        /**
         * 设置配置对象
         *
         * @constructor
         */
        Config:function(config){
            LayUIDataTableConfig=config;
        },
        /**
         * 设置JQuery对象，第一步操作。如果你没有在head标签里面引入jquery且未执行该方法的话，ParseDataTable方法、HideField方法会无法执行，出现找不到 $ 的错误。如果你是使用LayUI内置的Jquery，可以
         * let $ = layui.jquery   然后把 $ 传入该方法
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

        /**
         * 存在固定列的行高亮显示。对于普通行还是使用：obj['score']["row"].css("background-color", "#FAB000");形式即可
         * @param rowObj 调用LayUIDataTable.ParseDataTable返回的行集合的某一项（即：行对象）。
         * @param bgColor 背景颜色值。格式："red"或者"#ff0000"
         * @constructor
         */
        , DealFixedRowHighLight: function (rowObj, bgColor) {
            if (IsExistFiexColumnL())
            //左侧固定列高亮
                $(rowObj["fixedColumn_L"]).css("background-color", bgColor);
            if (IsExistFiexColumnR())
            // 右侧固定列高亮
                $(rowObj["fixedColumn_R"]).css("background-color", bgColor);
        }
    }
})();

/*
* 2018年08月01日：
* 感谢：（微信：qq86****11反馈）
*   1、修复对于有固定列的表格双击无法获取固定列行数据的BUG
*   2、修改对于有固定列的表格双击固定列事件无效BUG
*   3、优化:优化左右固定列双击事件处理
*
* 2018年08月08日：
* 感谢：（微信：hip-****-Noah反馈）
*   1、修复存在固定列时固定列无法高亮显示问题
*
* 2018年09月27日：
* 感谢：（微信：hip-****-Noah反馈）
*   1、提出双击固定列的标题头也能触发双击事件的问题，现已修复（固定列的标题头取消双击事件）
*
* */
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

                        
                        
                        // LayUIDataTable.Config({isdblClick: true,fixedColumnDBClick: false});
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
                                //固定列的高亮显示
                                 LayUIDataTable.DealFixedRowHighLight(obj,"red")
                            }
                        })
                    }// end done


                });//end table.render

                //以下为测试代码
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

**特别说明**

> 通过 `LayUIDataTable.HideField`隐藏列之后如果进行排序出现被隐藏的列再次出现的问题，解决方案如下：

**监听排序事件，进行隐藏处理**

```javascript
table.on('sort(demo)', function(obj){
    // 此处写你要隐藏的field
    $("[data-field='num']").css('display', 'none');
    //....
    
    
    //.....
    // 其它逻辑自行处理
    //.....
});
```

## 图四：固定列高亮显示

![](https://ws2.sinaimg.cn/large/0069RVTdly1fu2k99d5zaj31e60iyq66.jpg)

## 排序后不生效问题

排序之后双击行事件无效，解决方案如下：

> 在排序事件**table.on(sort(xxx))**排序事件里面重新执行:LayUIDataTable.ParseDataTable方法

```javascript
table.on('sort(demo)', function (obj) {
    debugger
    $("[data-field='id']").css('display', 'none');
    LayUIDataTable.SetJqueryObj($);// 第一步：设置jQuery对象
    // LayUIDataTable.HideField(['num','match_guest']);// 隐藏列-多列模式
    var currentRowDataList = LayUIDataTable.ParseDataTable(function (index, currentData, rowData) {
        console.log("当前页数据条数:" + currentRowDataList.length)
        console.log("当前行索引：" + index);
        console.log("触发的当前行单元格：" + currentData);
        console.log("当前行数据：" + JSON.stringify(rowData));
        var msg = '<div style="text-align: left"> 【当前页数据条数】' + currentRowDataList.length + '<br/>【当前行索引】' + index + '<br/>【触发的当前行单元格】' + currentData + '<br/>【当前行数据】' + JSON.stringify(rowData) + '</div>';
        layer.msg(msg)
    })
});
```

> 上述事件里面的逻辑可封装为方法，便于调用，请自行封装即可。