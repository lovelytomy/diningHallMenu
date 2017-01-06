# diningHallMenu
食堂周菜谱demo 

美工设计了一个食堂每周菜谱的PSD（如图1），本来这个页面用原生iOS实现并不难，但这个偏偏是微信网页用的，许久未写html代码，所以有些手生，遇到的最大问题是列表左侧的的内容在单元格中垂直居中，虽然网上有很多关于div内容垂直居中的文章，但是大多数情况下都是在已知div高度的情况下实现的，但是这个设计中，右侧的菜谱内容不固定，所以高度也不固定，因此没有办法按照一般的垂直居中来实现。
    #### 基于绝对定位＋transform 的垂直居中
    translate():translate()方法，根据左(X轴)和顶部(Y轴)位置给定的参数，从当前元素位置移动.当我们在translate() 变形函数中使用百分比值时,是以这个元素自身的宽度和高度 为基准进行换算和移动的，这样我们就可以解除对固定尺寸的依赖。

	.translate {
   		transform: translate(50px,100px); 
  		-ms-transform: translate(50px,100px); /* IE 9 */ 
		-webkit-transform: translate(50px,100px); /* Safari and Chrome */ 
		-o-transform: translate(50px,100px); /* Opera */ 
		-moz-transform: translate(50px,100px); /* Firefox */
	}

   ```
   					<li class="mui-table-view-cell">
						<div class="my-left">
							<div class="myMargin">
								<p class="lightGreenColor">周一</p>
								<p class="lightGrayColor myMarginTop">2016-12-01</p>
							</div>
						</div>
						<div class="my-middle">
							<p class="myMarginTop">北京烧鸭饭</p>
							<p class="myMarginTop">宫保鸡丁</p>
							<p class="myMarginTop">北京烧鸭饭</p>
							<p class="myMarginTop">宫保鸡丁</p>
							<p class="myMarginTop">北京烧鸭饭</p>
							<p class="myMarginTop">宫保鸡丁</p>
						</div>
					</li>
   ```
   
   ```
   .mui-table-view-cell {
	  position: relative;
	｝
	```
	
	```
	.myMargin{
		position: absolute;
		top: 50%;
		width:50%;
		-webkit-transform: translateX(-50%) translateY(-50%);
		-moz-transform: translateX(-50%) translateY(-50%);
		-ms-transform: translateX(-50%) translateY(-50%);
		transform: translateX(-50%) translateY(-50%);
		text-align: center;
  }
  ```
  ####  基于Flexbox 的垂直居中
  其实我一直对上个做法不是很满意，因为设置了绝对定位后，水平上居中有所影响，最后还是通过一些magin设置勉强达到水平居中。偶然间看到一个人关于垂直居中的总结，提到了Flexbox的方法，感觉很棒。试着用这种方法修改了我原来的写法，发现代码更少了，逻辑结构更清晰了。详见demo中2.html中的写法。
  使用Flexbox布局只需写两行声明即可:先给这个待居中元素的父元素设置 display: flex(在这个例子中是 class为mui-table-view-cell的li 元素),再给这个元素自身（在这个例子中是class为my-left的div）设置margin: auto
  
  
  ```
  			.mui-table-view-cell {
				display: flex;
			}
			.my-left {
				margin: auto;
			}
  ```
  
    这样就好了，还可以去掉之前class为myMargin的div，而且同时也实现了水平居中，真实一举两得。
