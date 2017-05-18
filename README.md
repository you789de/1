$(function(){
    $(".nav_list").css("left",sessionStorage.left+"px");
    $(".nav_list li").each(function(){
        if($(this).find("a").text()==sessionStorage.pagecount){
            $(".sideline").css({left:$(this).position().left});
            $(".sideline").css({width:$(this).outerWidth()});
            $(this).addClass("nav_cur").siblings().removeClass("nav_cur");
            navName(sessionStorage.pagecount);
            return false
        }
        else{
            $(".sideline").css({left:0});
            $(".nav_list li").eq(0).addClass("nav_cur").siblings().removeClass("nav_cur");
        }
    });
    var nav_w=$(".nav_list li").first().width();
    $(".sideline").width(nav_w);
    $(".nav_list li").on('click', function(){
        nav_w=$(this).width();
        $(".sideline").stop(true);
        $(".sideline").animate({left:$(this).position().left},300);
        $(".sideline").animate({width:nav_w});
        $(this).addClass("nav_cur").siblings().removeClass("nav_cur");
        var fn_w = ($(".nav").width() - nav_w) / 2;
        var fnl_l;
        var fnl_x = parseInt($(this).position().left);
        if (fnl_x <= fn_w) {
            fnl_l = 0;
        }else {
            fnl_l = fn_w - fnl_x;
        }
        $(".nav_list").animate({
            "left" : fnl_l
        }, 300);
        sessionStorage.left=fnl_l;
        var c_nav=$(this).find("a").text();
        navName(c_nav);
    });
    var fl_w=$(".nav_list").width();
    $(".nav_list").on('touchstart', function (e) {
        var touch1 = e.originalEvent.targetTouches[0];
        x1 = touch1.pageX;
        y1 = touch1.pageY;
        ty_left = parseInt($(this).css("left"));
    });
    $(".nav_list").on('touchmove', function (e) {
        var touch2 = e.originalEvent.targetTouches[0];
        var x2 = touch2.pageX;
        var y2 = touch2.pageY;
        if(ty_left + x2 - x1>=0){
            $(this).css("left", 0);
        }else{
            $(this).css("left", ty_left + x2 - x1);
        }
        if(Math.abs(y2-y1)>0){
            e.preventDefault();
        }
    });
});
function navName(c_nav) {
    switch (c_nav) {
        case "资讯":
            sessionStorage.pagecount = "资讯";
            break;
        case "分析":
            sessionStorage.pagecount = "分析";
            break;
        case "原创":
            sessionStorage.pagecount = "原创";
            break;
        case "技术":
            sessionStorage.pagecount = "技术";
            break;
        case "项目":
            sessionStorage.pagecount = "项目";
            break;
        case "评价":
            sessionStorage.pagecount = "评价";
            break;
        case "在线查询":
            sessionStorage.pagecount = "在线查询";
            break;
        case "新闻":
            sessionStorage.pagecount = "新闻";
            break;
        case "下载":
            sessionStorage.pagecount = "下载";
            break;
    }
}
