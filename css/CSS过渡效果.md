##CSS过渡效果

- 首先我们先准备一个盒子

~~~html
<div class="container">
  <div class="box"></div>
</div>
~~~

- 设置一下样式

~~~css
.container{
  padding: 50px 50px;
}
.box{
  width: 35px;
  height: 35px;
  background-color: green;
}
.box:hover{
  border-radius: 50%;
}
~~~

上面我们使用到了`:hover`伪类来设置盒子的悬停样式，当我们鼠标移动到盒子上面后正方形的盒子会变成圆形。

当然还有很多方式触发过渡效果，`:focus`, `:checked`或者媒体查询触发、JavaScript触发等等。

- 使用`transition`属性可以为我们的变化提供动画式的过渡效果。

~~~css
.box{
  width: 35px;
  height: 35px;
  background-color: green;
  transition-property: border-radius;
  transition-duration: 3s;
  transition-delay: 1s;
}
~~~

上面我们在盒子里面增加了两个属性，`transition-property`设置我们需要过渡效果的属性，`transition-duration`设置过渡完成的时间。然后当我们鼠标再次移动到盒子上面时，正方形的盒子会在一个动画的过程中变成圆形。`transition-delay`可以让鼠标放上后延迟1s再发生动画。除此之外我们还可以用`transition-timing-function`来订制我们的动画效果。常见的有：

```
linear        匀速
ease          默认，由慢变快再变慢
ease-in       缓慢开始
ease-out      缓慢结束
ease-in-out   缓慢开始，缓慢结束
```

- 多属性过渡

我们可以在`transition-property`中设置多个过渡效果让他们同时发生，中间用逗号隔开。相对应的在下面的过渡属性中加入相应的值，也用逗号隔开。

上面的那些属性也可以放在一起写，即

~~~
transition: 过渡属性 过渡所需时间 过渡动画效果 过渡延迟时间;
~~~

