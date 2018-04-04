

- 首先管理端模板的话还是使用官方提供的，参考链接：[点此打开后台布局页面](http://www.layui.com/demo/layuiAdmin.html)

- 以下我只列举出关键代码，各位根据实际情况拷贝到自己项目适当位置
- 相比上一篇教程([点击此处查阅](https://github.com/TangHanF/ProjectRecord/blob/master/%E5%89%8D%E7%AB%AF/LayUI/%E4%B8%BALayui%E7%9A%84Tab%E9%80%89%E9%A1%B9%E5%8D%A1%E5%A2%9E%E5%8A%A0%E5%85%B3%E9%97%AD%E5%BD%93%E5%89%8D%E3%80%81%E5%85%B3%E9%97%AD%E5%85%B6%E5%AE%83%E6%93%8D%E4%BD%9C.md))来说，此次除了：
    - 关闭当前
    - 关闭所有
    
    之外，又新增了：
    - 关闭非当前
    - 关闭左侧所有
    - 关闭右侧所有
    - 取消

    同时又对代码逻辑进行了优化处理。

    你会发现关闭左侧所有、关闭右侧所有真的很简单，其实就是**把所有已打开的Tab的ID放入一个集合，而且我也能拿到当前激活的Tab的ID值，所以我不是通过遍历处理，而是想着截取数组的形式处理**。下面代码可以好好观察一下，顿时就简单多了
# 效果图
![](https://github.com/TangHanF/ProjectRecord/raw/master/前端/LayUI/img/tab右键菜单2.0.png)

----------
# HTML
首先在body里面插入以下一段html:
``` html
    <ul class="rightmenu">
        <li data-type="closethis">关闭当前</li>
        <li data-type="closeall">关闭所有</li>
        <li data-type="closeothers">关闭非当前</li>
        <li data-type="closeleft">关闭左侧所有</li>
        <li data-type="closeright">关闭右侧所有</li>
        <li data-type="cancel"><i class="layui-icon layui-icon-yinshenim"></i>取消</li>
    </ul>
```
    相关CSS样式请看下面《CSS样式》部分


-------

# JS

``` javascript
/**
    * 注册tab右键菜单点击事件
    */
$(".rightmenu li").click(function () {
    var currentActiveTabID = $("li[class='layui-this']").attr('lay-id');// 获取当前激活的选项卡ID
    var tabtitle = $(".layui-tab-title li");
    var allTabIDArr = [];
    $.each(tabtitle, function (i) {
        allTabIDArr[i] = $(this).attr("lay-id");
    })

    switch ($(this).attr("data-type")) {
        case "closethis"://关闭当前，如果开始了tab可关闭，实际意义不大
            tabDelete(currentActiveTabID);
            break;
        case "closeall"://关闭所有
            tabDeleteAll(allTabIDArr);
            break;
        case "closeothers"://关闭非当前
            $.each(allTabIDArr, function (i) {
                var tmpTabID = allTabIDArr[i];
                if (currentActiveTabID != tmpTabID)
                    tabDelete(tmpTabID);
            })
            break;
        case "closeleft"://关闭左侧全部
            var index = allTabIDArr.indexOf(currentActiveTabID);
            tabDeleteAll(allTabIDArr.slice(0, index));
            break;
        case "closeright"://关闭右侧全部
            var index = allTabIDArr.indexOf(currentActiveTabID);
            tabDeleteAll(allTabIDArr.slice(index + 1));
            break;
        default:
            $('.rightmenu').hide();

    }
    $('.rightmenu').hide();
})
```
--------------------
``` javascript
tabDelete = function (id) {
    console.log("删除的TabID："+id)
    element.tabDelete("你的Tab选项卡ID", id);//删除
}
tabDeleteAll = function (ids) {
    $.each(ids, function (i, item) {
        element.tabDelete("你的Tab选项卡ID", item);
    })
}
```

--------------------

``` javascript
// 点击空白处关闭右键弹窗
$(document).click(function () {
    $('.rightmenu').hide();
})
```
----------------

``` javascript
/**
* 绑定右键菜单
* @constructor
*/
function CustomRightClick () {
    //屏蔽Tab右键菜单
    $('.layui-tab-title li').on('contextmenu', function () {
        return false;
    })
    $('.layui-tab-title,.layui-tab-title li').click(function () {
        $('.rightmenu').hide();
    });
    $('.layui-tab-title li').on('contextmenu', function (e) {
        var popupmenu = $(".rightmenu");
        l = ($(document).width() - e.clientX) < popupmenu.width() ? (e.clientX - popupmenu.width()) : e.clientX;
        t = ($(document).height() - e.clientY) < popupmenu.height() ? (e.clientY - popupmenu.height()) : e.clientY;
        popupmenu.css({left: l, top: t}).show();
        return false;
    });
}
```

-------
# CSS样式
``` css
<style>
    /**右键菜单*/
    .rightmenu {
        position: absolute;
        width: 110px;
        z-index: 9999;
        display: none;
        background-color: #fff;
        padding: 2px;
        color: #333;
        border: 1px solid #eee;
        border-radius: 2px;
        cursor: pointer;
    }

    .rightmenu li {
        text-align: center;
        display: block;
        height: 30px;
        line-height: 32px;
    }

    .rightmenu li:hover {
        background-color: #666;
        color: #fff;
    }
</style>
```


# 问题
- 右击关闭暂时只能关闭当前已经激活的Tab，没法在任意一个Tab右击自动激活再去关闭，各位可优化一下