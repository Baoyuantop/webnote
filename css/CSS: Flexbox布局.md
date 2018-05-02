# CSS: Flexbox布局

早期布局主要依赖表格，后来有绝对定位、浮动定位的出现，在CSS3中引入了_Flex-box_布局，伸缩布局盒模型。主要思想是让容器有能力让其子项目能够改变其高度，宽度，甚至顺序，以最佳的方式填充空间。以简单的方式实现复杂的布局。用Flexbox布局有两部分组成，一个是Flex容器`Flex Container`,一个是Flex里面的项目`Flex Item`.在容器上有横着的*主轴*`main axis`,竖着的叫做`cross axis`.在主轴上最左边的点叫做*主轴的起点*`main start`.最右边的点叫做`main end`,_主轴的终点_.在cross axis上也有两个点，上面那个是`cross start`,下面那个是`cross end`.在每一个项目中水平的尺寸叫做`main size`,垂直的高度叫做`cross size`.

1. 设置Flex容器。

- 首先我们写一个元素

~~~html
<div class="container">
  <div class="item-1">1</div>
  <div class="item-2">2</div>
  <div class="item-3">3</div>
  <div class="item-4">4</div>
  <div class="item-5">5</div>
</div>
~~~



默认情况下他们是这样显示的：

![深度截图_选择区域_20180428203353](/home/baoyuan/Desktop/深度截图_选择区域_20180428203353.png)

- 接下来我们设置这个容器为Flex容器：

~~~css
.container{
  display: flex;
}
~~~

我们会发现Flex容器下变成了这个样子：![深度截图_选择区域_20180428203909](/home/baoyuan/Desktop/深度截图_选择区域_20180428203909.png)

2. 项目的排列方向

- 在Flex容器上面我们可以用`flex-direction`这个属性来控制项目的排列方式，这个属性主要设置的就是`main axis`,也就是主轴的方向。有两个主要的方向，一个是`row`,水平方向。另一个是`column`,就是垂直的方向。

我们改变我们的样式为：

~~~css
.container{
  display: flex;
  flex-direction: row;
}
~~~

此时我们的项目会水平排列，并且`row`是默认值。除此之外`row-reverse`可以设置项目反向排列，也就是从右向左。同理如果我们设置为`column`的话项目就会从上往下排列，同样的`column-reverse`可以让我们的项目从下往上排列。

3. 换行显示

- Flex容器中的项目默认的话会在同一行显示，通过`flex-wrap`我们可以设置项目是否要多行显示。

增加我们的项目：

~~~html
<div class="container">
  <div class="item-1">1</div>
  <div class="item-2">2</div>
  <div class="item-3">3</div>
  <div class="item-4">4</div>
  <div class="item-5">5</div>
  <div class="iten-6">6</div>
  <div class="item-7">7</div>
  <div class="item-8">8</div>
</div>
~~~

增加样式：

~~~css
.container{
  display: flex;
  flex-wrap: wrap;
}
~~~

你就会发现每行的项目数目会根据容器的宽度多行显示。同样的`wrap-reverse`会颠倒我们的项目。

上面两个属性我们还可以用一个`flex-flow`共同设置：

~~~css
.container{
  display: flex;
  flex-flow: row wrap;
}
~~~

4. justify-content

这个属性可以帮助我们设置项目的位置以及各自之间的间隔。默认值：`flex-start`.`flex-end`为右对齐，`center`为左对齐。`space-between`会在项目间设置间隔。但是项目与容器间是没有间隔的，如果需要的话可以用`space-around`.

5. align-items

这个属性可以设置项目在垂直方向上的对齐方式，我们的项目高度默认是和容器高度相等，容器高度大的话我们的项目就会去拉伸，这也就对应了他的默认属性`stretch`.除此之外，`align-start`会让我们的项目靠着容器顶部去显示，`flex-end`则是在底部显示。居中的话是`center`,如果项目垂直方向上对齐方式不同，我们可以用`baseline`属性，然后去指定各自顶部的内边距。

6. 多行项目的对齐方式 `align-content`.

默认值`stretch`,拉伸显示的方式。还可以设置`flex-start`,`flex-end`,`center`.他们都是不拉伸的显示方式。`space-between`可以在行与行之间设置间隙。`space-around`会在行的周围也就是上下添加间隔，间隔大小就看容器剩余了多少空间。

7. 项目的顺序

Flex容器中项目的默认属性就是我们书写HTML代码时的顺序，但是我们可以用`order`去改变它。默认情况下所有项目的order属性的值都为0，我们可以把第一个项目放到最后：

~~~css
.item-1{
  order: 1;
}
~~~

这样的话因为1在0的后面，所以第一个项目就会到最后面。类比如果想让哪个元素排到最前面，设置他的`order`为_-1_即可。

8. 项目水平宽度

Flex项目默认的水平宽度是它里面内容的宽度。在水平方向上如果我们想设置项目的宽度从而适应视口的宽度，`flex-grow`属性的默认值为0，将其改变为1就可以实现：

~~~css
.item{
  flex-grow: 1;
}
~~~

此时我们的项目会在水平方向上铺满屏幕，`flex-grow`还可以单独的设置某个元素，通过改变数字的大小控制他的宽度。

`flex-basis`可以设置项目初始的宽度，默认是_auto_.

`flex-shrink`默认值为1，我们可以将某个项目设置为0，他的宽度就不会随着视口的减小而减小。设置的值大的话，在我们缩小页面的时候就会发现它缩小的最多。

上面三个属性可以用一个_flex_全部设置。`flex: flex-grow  flex-shrink  flex-basis;`.

9. align-self

在项目中使用这个属性就可以单独设置他的垂直对齐方式，包括：`flex-start`,`flex-end`,`center`,`stretch`等等。