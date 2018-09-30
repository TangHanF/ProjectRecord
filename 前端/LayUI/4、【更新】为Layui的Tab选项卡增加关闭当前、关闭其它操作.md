

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
首先在body里面适当位置处插入以下一段html:
``` html
    <ul class="rightmenu">
        <li data-type="closethis">关闭当前</li>
        <li data-type="closeall">关闭所有</li>
        <li data-type="closeothers">关闭非当前</li>
        <li data-type="closeleft">关闭左侧所有</li>
        <li data-type="closeright">关闭右侧所有</li>
        <li data-type="refresh">刷新当前页</li>
        <li data-type="cancel"><i class="layui-icon layui-icon-yinshenim"></i>取消</li>
    </ul>
```
    相关CSS样式请看下面《CSS样式》部分

-------

# JS

请在适当位置加入以下代码：

``` javascript
//屏蔽Tab选项卡的右键
$('.layui-tab-title li').on('contextmenu', function () {
    return false;
})

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
        case "closethis"://关闭当前，如果开启了tab可关闭，实际意义不大
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
        case "refresh":
        // 重新加载iFrame，实现更新。注意：如果你不是使用的iFrame则无效，具体刷新实现自行处理                          //document.getElementById(currentActiveTabID).contentWindow.location.reload(true);//这种方式也可以，下面这个也可以
             refreshiFrame();
             break;
        default:
            $('.rightmenu').hide();

    }
    $('.rightmenu').hide();
})

/*
*重新加载iFrame，实现更新
*/
function refreshiFrame() {
    var $curFrame = $('iframe:visible');
    $curFrame.attr("src",$curFrame.attr("src"));
    return false;
}
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

> 注意：
>
> - 以上的“element”为LayUI的“element”模块，引入：
>
> ```javascript
> layui.use(["element"],function(){
> 	var element = layui.element;
> 	// .....
> })
> ```
>
>
>
> - “你的Tab选项卡ID”：是指你在页面添加的LayUI的选项卡指定的“lay-filter”，例如：
>
> ```html
> <!-- 内容主体区域 -->
> <div class="layui-body">
>     <!-- 顶部切换卡 -->
>     <div class="layui-tab " lay-filter="main-tab" lay-allowClose="true">
>         <div class="layui-tab-tool open" title="收起">
>             <i class="wdfont wdicon-xiangzuojiantou"></i>
>         </div>
>         <ul class="layui-tab-title" style="z-index: 999;">
>             <li lay-id="0" class="layui-this"><i class="wdfont wdicon-shouye"></i>首页</li>
>         </ul>
>         <div class="layui-tab-content">
>             <div class="layui-tab-item layui-show">
>                 <iframe id="0" src="desktop.html" class="layui-tab-iframe"></iframe>
>             </div>
>         </div>
>     </div>
> </div>
> ```

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
* 注册并绑定右键菜单
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

> CustomRightClick()方法实现在右键时弹出菜单，方法的具体调用位置请根据实际情况确定，例如在页面渲染完成之后调用该方法。

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