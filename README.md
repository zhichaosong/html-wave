【前端】CSS3、Canvas、SVG等5种方式实现水波纹波浪动画特效

演示地址：https://zhichaosong.github.io/html-wave/index.html

# 一、CSS3动画+图片波浪效果
这种方式代码量最小也最简单，算上HTML、CSS一共63行，主要使用 Animation 动画和一张波浪图片大约 7k 也不算大，先上效果图。
## 1. 效果图
![效果图](https://img-blog.csdn.net/20180919165125314?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3poaWNoYW9zb25n/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)
## 2. 代码
```html
<!DOCTYPE html>
<html>
	<head>
		<style>
			.water-group{
				position: relative;
				height:110px;
				width: 100%;
				overflow: hidden;
				background: linear-gradient(to bottom, #3ec4fc, #0081cc);
			}
			.water-group .water{
				position: absolute;
				width: 200%;
				height:100%;
				background-size: 50% 100%;
			}
			.water-group .water1{
				top:20px;
				left: -100%;
				opacity: 0.2;
				animation: water-right 20s infinite linear;
			}
			.water-group .water2{
				top:30px;
				left: 0;
				opacity: 0.3;
				animation: water-left 30s infinite linear;
			}
			.water-group .water3{
				top:45px;
				left: -100%;
				animation: water-right 40s infinite linear;
			}
			@keyframes water-right{
				0% {
					transform: translateX(0) translateZ(0) scaleY(1)
				}
				50% {
					transform: translateX(25%) translateZ(0) scaleY(0.85)
				}
				100% {
					transform: translateX(50%) translateZ(0) scaleY(1)
				}
			}
			@keyframes water-left{
				from{
					transform: translate(0%,0px);
				}
				to{
					transform: translate(-50%,0px);
				}
			}
		</style>
	</head>
	<body>
		<div class="water-group">
			<div class="water water1" style="background-image: url('wave.png')"></div>
			<div class="water water2" style="background-image: url('wave.png')"></div>
			<div class="water water3" style="background-image: url('wave.png')"></div>
		</div>
	</body>
</html>
```
## 3. 原理
① **波浪图**：需要一张首尾衔接的边缘透明波浪图，3 层波浪通过```opacity ```属性改变透明度；
② **布局**：整个波浪块使用```water-group ```限定```relative ```布局，保证 3 个波浪子元素使用的绝对布局可以限定在其中，且波浪之间有一定高度差凸显层次感；
③ **动画**：通过```keyframes ```使波浪图片沿 X 轴无限循环平移实现波动；
④ **要点**：
几个关键参数：
- 波浪块宽度：```width: 200%;```
- 波浪图片背景重复：```background-size: 50% 100%;```
- 波浪块初始位置：```left: -100%;```
- 波浪块平移终点位置：```translateX(25%);```

对应说明：
- 波浪块宽度为屏幕的 2 倍，这样每次平移一个屏幕的距离可以做到无缝衔接；
- 波浪图片原本为一个屏幕大小，变成 2 倍后如果拉伸的话就做不到首尾衔接了，只能是复制了另外一半；
- 波浪块初始位置跟屏幕右对齐，左边多了一个屏幕的距离，这样可以向右移动不留空白；
- 波浪块平移终点位置跟屏幕左对齐，由于波浪块是两个相同图片拼接的，所以左对齐和右对齐在屏幕这边是完全相同的，就相当于初始和终止时刻完全一样，这样下一个循环刚好衔接上；

⑤ **示意图**：
![示意图](https://img-blog.csdn.net/20180919165140435?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3poaWNoYW9zb25n/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)


# 二、纯CSS3杯中水效果
# 三、纯CSS3涟漪效果
# 四、Canvas波浪效果
# 五、SVG+jQuery波浪效果
# 六、源码下载
https://github.com/zhichaosong/html-wave.git
