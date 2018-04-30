## Css3之transition实现下划线

在这里先看看我们的demo

![]()

### 认识transition

这是CSS3中新增的一个样式，可以实现动画的过度。通常使用在添加某种效果可以从一种样式转变到另一个的时候。

#### transition属性

- transition： 简写属性，用于在一个属性中设置四个过渡属性。
- transition-property： 规定应用过渡的 CSS 属性的名称。
- transition-duration： 	定义过渡效果花费的时间。默认是 0。
- transition-timing-function： 规定过渡效果的时间曲线。默认是 "ease"。
	- linear： 规定以相同速度开始至结束的过渡效果（等于 cubic-bezier(0,0,1,1)）
	- ease： 规定慢速开始，然后变快，然后慢速结束的过渡效果（cubic-bezier(0.25,0.1,0.25,1)）
	- ease-in： 规定以慢速开始的过渡效果（等于 cubic-bezier(0.42,0,1,1)）
	- ease-out： 规定以慢速结束的过渡效果（等于 cubic-bezier(0,0,0.58,1)）
	- ease-in-out： 规定以慢速开始和结束的过渡效果（等于 cubic-bezier(0.42,0,0.58,1)）
	- cubic-bezier(n,n,n,n)： 在 cubic-bezier 函数中定义自己的值。可能的值是 0 至 1 之间的数值。
- transition-delay： 规定过渡效果何时开始。默认是 0。

```
transition: width 1s linear 2s;		/*简写实例*/

/*等同如下*/
transition-property: width;
transition-duration: 1s;
transition-timing-function: linear;
transition-delay: 2s;
```

#### tranform属性

- translate() 根据左(X轴)和顶部(Y轴)位置给定的参数，从当前元素位置移动。
- rotate() 在一个给定度数顺时针旋转的元素。负值是允许的，这样是元素逆时针旋转。
- scale() 该元素增加或减少的大小，取决于宽度（X轴）和高度（Y轴）的参数：
- skew() 包含两个参数值，分别表示X轴和Y轴倾斜的角度，如果第二个参数为空，则默认为0，参数为负表示向相反方向倾斜。
- matrix() matrix 方法有六个参数，包含旋转，缩放，移动（平移）和倾斜功能。

### 实现我们需要的效果
当然，在这就直接放出代码，代码中有注释方便理解

```
/*css代码*/

h2{
	position: relative;
	padding: 15px;
	text-align: center;	
}
button{
	width: 100px;
	height: 40px;
	border-radius: 15px;
	border: none;
	background: #188FF7;
	color: #fff;
	outline: none;
	cursor: pointer;
	font-weight: bold;
}
button:hover{
	background: #188EA7;
}
.container{
	width: 600px;
	display: flex;
	flex-direction: column;
	align-items: center;
	margin: 0 auto;
	
}
.line{
	position: absolute;
	left: 0;
	bottom: 0;
	height: 3px;
	width: 100%;
	transition: transform .5s;
	background: #188EA7;
	color: #188EA7;
	transform: scaleX(0);
	z-index: 1111;			
}

@keyframes changeColor1{
	from{
		color: #000;
	}
	to{
		color: #188EA7;
	}
}
@keyframes changeColor2{
	from{				
		color: #188EA7;
	}
	to{
		color: #000;
	}
}
```

```
<!--html代码-->

<div class="container">
	<h2 id="title">
		百度前端学院
		<i class="line" id="line"></i>
	</h2>
	<button id="change">Change</button>
</div>
```

```
//js部分代码

(function () {
	let btn = document.getElementById('change');
	let h2 = document.getElementById('title');
	let line = document.getElementById('line');
	let count = 0;
	btn.onclick = function () {
		if(count%2===0){
			line.style.transform = "scaleX(1)";
			h2.style.animation = "changeColor1 1s";
			h2.style.color = "#188EA7";
			count++;
		}else{
			line.style.transform = "scaleX(0)";
			h2.style.animation = "changeColor2 1s";
			h2.style.color = "#000";
			count++;
		}
		
	}
})();
```

## 总结
到这里我们就已经将此效果完全呈现，同时我们也学习了CSS3中的transition属性和tranform属性。当然完成此动画还需要有一些html和css基础。

成功不在一朝一夕间，我们都需要努力