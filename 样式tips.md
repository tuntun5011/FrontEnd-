 1. absolute、fixed、float都会脱离文档流，但是float会占位（文字围绕） 

 2. box-sizing:border-box;告诉浏览器元素的边框和内边距都包含在width、height内。

 3. float会引起该元素【其后】的元素围绕该元素，解决方法是其后的元素添加：clear:both(left/right)取消浮动影响。

or添加class .clearfix{overflow:auto}清除浮动（父元素）

 4. vertical-aglin 影响inline和inline-block

 5. div 的width、height 100%是相对于父dom的，父dom必须有宽高子dom的100%才能生效。
如果设置某个div100%，但父dom没有明确宽高，那么可从html、body一级一级设置height100%直到该div,此时该div的height是body的height。
如果不层层设置100%，可设置该div position：absolute；height: 100%；也是相对于body的高度的100%。
  
  
6. 关于flex:
			 
			 类似这种排列的实现：
			 a       b        c
		       ttesy  tttestte  tests
	
	```javascript
		<div class="share-step-No">
                    <div class="share-step-group">
                        <span class="step-No">1</span>
                        <span class="step-tip">下载客户端</span>
                    </div>
                    <div class="share-step-group">
                        <span class="step-No">2</span>
                        <span class="step-tip">完成注册流程</span>
                    </div>
                    <div class="share-step-group">
                        <span class="step-No">OK</span>
                        <span class="step-tip">可以使用啦</span>
                    </div>
             	</div>
		
```javascript
		.share-step-No{	/**父div**/
			display: flex;
			flex-direction: row;
			justify-content: space-between;
		}
		.share-step-group{	/**子div**/
			display: flex;
			flex-direction: column;
			align-items: center;
		}
