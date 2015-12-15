#TouchSwipe 1.6
A jQuery plugin to be used on touch devices such as iPad, iPhone, Android etc.

Detects single and multiple finger swipes, pinches and falls back to mouse 'drags' on the desktop.

Time and distance thresholds can be set to distinguish between swipe gesture and slow drag.

Allows exclusion of child elements (interactive elements) as well allowing page scrolling or page zooming depending on configuration.

* Detects swipes in 4 directions, "up", "down", "left" and "right"
* Detects pinches "in" and "out"
* Supports single finger or double finger touch events
* Supports click events both on the touchSwipe object and its child objects
* Definable threshold / maxTimeThreshold to determin when a gesture is actually a swipe
* Events triggered for swipe "start","move","end" and "cancel"
* End event can be triggered either on touch release, or as soon as threshold is met
* Allows swiping and page scrolling
* Disables user input elements (Button, form, text etc) from triggering swipes

## Installation  
###NPM
````bash
npm install jquery-touchswipe --save
````
###Bower
````bash
bower install jquery-touchswipe --save
````
###Manual
Include the minified file in your project.
````html
<script type="text/javascript" src="js/jquery.touchSwipe.min.js"></script>
````

##Usage
````javascript
$(function() {
  $("#test").swipe( {
    //Generic swipe handler for all directions
    swipe:function(event, direction, distance, duration, fingerCount, fingerData) {
      $(this).text("You swiped " + direction );  
    }
  });

  //Set some options later
  $("#test").swipe( {fingers:2} );
});
````

For full demos, code examples and documentation, see below.

## Demos, examples and docs

[http://labs.rampinteractive.co.uk/touchSwipe](http://labs.rampinteractive.co.uk/touchSwipe)  
[http://labs.rampinteractive.co.uk/touchSwipe/docs](http://labs.rampinteractive.co.uk/touchSwipe/docs)

### For port to XUI see:
https://github.com/cowgp/xui-touchSwipe

##中文说明

###滑动事件：

* swipe (事件，滑动的方向，滑动的距离，一次滑动的时间 , 几根手指)
* 滑动事件还有 方法和上面相同 swipeLift – 向左滑动  swipeRight-向右滑动 swipeUp-向上滑动  swipeDown-向下滑动
* swipeStatus (事件, 手指状态，滑动的方向，滑动的距离，一次滑动的时间 , 几根手指)
* swipeStatus 和 swipe 不同的是 这个参数是一直在执行的，大家可以看看下面的例子（复制到记事本上打开即可），来了解一下两个事件的不同之处。

###两根手指往里捏或者扩张事件：
* pinchStatus(事件,手指状态 ,方向(in和out，需要注意的一点in是往外扩，out是往里捏),滑动的距离, 一次滑动的时间 , 几根手指, 变焦)
包含：pinchIn（向外扩张），pinchOut （向里捏）
* 其他常用事件还有：doubleTap （双击屏幕） click （单击屏幕） longTap (长按屏幕)

#####滑动事件demo：
````html
<html>
<head>
<meta http-equiv="Content-Type" content="text/html; charset=gb2312" />
<title>无标题文档</title>
<script type="text/javascript" src="http://www.163css.com/myweb/hihilinxuan/template/hihilinxuan/cssjs/2012/12/ifengtouch/js/jquery.min.js"></script>
<script type="text/javascript" src="http://www.163css.com/myweb/hihilinxuan/template/hihilinxuan/cssjs/2012/12/ifengtouch/js/jquery.touchSwipe.min.js"></script>
<script>
$(function() {
//swipe 的dome
$("#test").swipe( {
swipe:function(event, direction, distance, duration, fingerCount) {
$(this).text("你用"+fingerCount+"个手指以"+duration+"秒的速度向" + direction + "滑动了" +distance+ "像素 " );
},
});
//swipeStatus的dome
$("#test2").swipe( {
swipeStatus:function(event, phase, direction, distance, duration,fingerCount) {
$(this).text("你用"+fingerCount+"个手指以"+duration+"秒的速度向" + direction + "滑动了" +distance+ "像素 " +"你在"+phase+"中");
},
});
});
</script>
</head>
<body>
<div id="test" style="height:200px; background:#C63;-webkit-user-select:none; text-align:center; line-height:200px; color:#fff">swipe 的dome</div>
<div id="test2" style="height:200px; background:#C63; margin-top:20px;-webkit-user-select:none; text-align:center; line-height:200px; color:#fff">swipeStatus的dome</div>
</body>
</html>
````
 

#####移动端div内手指滑动内容效果，不出现滚动条： 
````javascript
$(function () {
    //手机滑动效果
    var swiptleft = 0;
    var swiptw = $(".touchswipe").width() - $(".borrowlistcon .block").eq(0).width();
    $(".touchswipe").swipe({
        swipeLeft: function (event, direction, distance, duration, fingerCount) {
            swiptleft = swiptleft - distance;
            if (swiptleft > swiptw) {
                $(".touchswipe .block").animate({
                    left: swiptleft + 'px'
                }, 10)
            }
            else {
                swiptleft = swiptw;
                $(".touchswipe .block").animate({
                    left: swiptw + 'px'
                }, 10)
            }
             
        },
 
        swipeRight : function (event, direction, distance, duration, fingerCount) {
                swiptleft = swiptleft + distance;
                if (swiptleft < 0) {
                    $(".touchswipe .block").animate({
                        left: swiptleft + 'px'
                    }, 10)
                }
                else {
                    swiptleft = 0;
                    $(".touchswipe .block").animate({
                        left: 0 + 'px'
                    }, 10)
                }
             
    }
    });
 
})
````
官方网站
http://labs.rampinteractive.co.uk/touchSwipe/demos/

英文说明地址：
http://labs.rampinteractive.co.uk/touchSwipe/docs/symbols/%24.fn.swipe.html

下载地址
https://github.com/mattbryson/TouchSwipe-Jquery-Plugin

