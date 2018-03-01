### passvie 事件监听器

背景：
    底页面height高于一屏，页面上覆弹层（带灰色mask），且弹层可滚动。弹层滚动时禁止底页滚动。
    
方法：
    监听touchMove事件，touchMove区域不是list时调用event.preventDefault()阻止默认事件。
   
    setTimeout(function(){
      document.addEventListener("touchmove", areaStopTouchMove, false);
    },xx);

    function areaStopTouchMove(event){
      if(document.querySelector(".list").contains(event.target) > 0) {//list使用了iscroll
         return;
      }
      stopTouchMove(event);
    }

    function stopTouchMove(event){
      event.preventDefault();
      event.stopPropagation();
    }
问题：
    在某台华为手机上，底层页面仍然可以滚动
    
原因：
    该华为手机内置的webkit内核浏览器版本较高，dom eventTarget事件对象的addEventListener()支持passive属性，且默认是passive的。
    
    target.addEventListener(type, listener, options); 
    type  表示监听事件类型的字符串。 
    listener  当所监听的事件类型触发时，会接收到一个事件通知（实现了 Event 接口的对象）对象。listener 必须是一个实现了 EventListener 接口的对象，或者是一个函数 
    options 可选。 
    一个指定有关 listener 属性的可选参数对象。可用的选项如下： 
      capture:  Boolean，表示 listener 会在该类型的事件捕获阶段传播到该 EventTarget 时触发。 
      once:  Boolean，表示 listener 在添加之后最多只调用一次。如果是 true， listener 会在其被调用之后自动移除。 
      passive: Boolean，表示 listener 永远不会调用 preventDefault()。如果 listener 仍然调用了这个函数，客户端将会忽略它并抛出一个控制台警告。 
  
  此时调用 event.preventDefault();无效，导致底层页面仍可以滚动。
  
  解决：
      判断浏览器是否支持passive，分情况处理。
      
      *** 以下代码待验证 *** 
      var supportsPassive = false;
      document.createElement("div").addEventListener("test", function() {}, {
        get passive() {
          supportsPassive = true;
          return false;
        }
      }
      
      setTimeout(function(){
        if(supportPassive){
          document.addEventListener("touchmove", areaStopTouchMove, {passive:false});
        }else{
          document.addEventListener("touchmove", areaStopTouchMove, false);
        }
      },xx);
      
      
  ### 参考：
  https://www.cnblogs.com/ziyunfei/p/5545439.html
  
  https://developer.mozilla.org/zh-CN/docs/Web/API/EventTarget/addEventListener
  
  https://www.jianshu.com/p/baf61adc8667
