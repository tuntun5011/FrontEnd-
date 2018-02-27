absolute、fixed、float都会脱离文档流，但是float会占位（文字围绕） 

box-sizing:border-box;告诉浏览器元素的边框和内边距都包含在width、height内。

float会引起该元素【其后】的元素围绕该元素，解决方法是其后的元素添加：clear:both(left/right)取消浮动影响。

or添加class .clearfix{overflow:auto}清除浮动（父元素）

vertical-aglin 影响inline和inline-block
