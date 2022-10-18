---
title: CSS学习
---

## CSS(Cascading Style Sheets，层叠样式表)

### CSS样式
* 网页实际上是一个多层的结构，通过CSS可以分别为网页的每一个层来设置样式，最终看到的是网页的最上边的一层。总之，CSS用来设置网页中元素的样式。
* 方式一(内联样式，行内样式)
  * 在标签内部通过style属性来设置元素的样式
    * eg. <p style="color:red;front-size:30px;">
    * 不方便使用，开发时达咩！
* 方式二(内部样式表)
  * 通过CSS选择器来选中元素并设置样式，将样式编写到head中的style标签里
  * 元素名{color: green;front-size:50px}

* 方式三(外部样式表)
  * CSS样式编写到外部CSS文件中
  * 越发离谱通过link标签引入外部的CSS文件<link rel="stylesheet" href="">
  * CSS样式编写到外部，可以使用到浏览器的缓存机制，加快网页的加载，提高用户体验
  * 样式可以在不同网页间复用，开发时常用！


#### 1 CSS语法

* 注释
* 基本语法
  * 选择器 声明块

#### 2 常用选择器

* 元素选择器
  * 标签名{}
* id选择器
  * #id{}
* class选择器
  * class是一个标签属性，和id类似，class可以重复，id不能重复
  * class可以对元素分组
  * 可以同时为一个元素指定多个class属性 class="blue aaa"
  * .class{}
* 通配选择器
  * 选中页面中的所有元素
  * *{}

#### 3 复合选择器

* 交集选择器
  * 选择器1选择器2选择器n{}
  * 注意：交集选择器中如果有元素选择器，必须使用元素选择器开头
  * eg. div.red{} .a.b.c{} div#box1{}(不常用，box1本来就是唯一id)
* 选择器分组（并集选择器）
  * 同时选择多个选择器对应的元素
  * 选择器1,选择器2,选择器n{}
  * eg. #b1,.p1,h1,div{}

#### 4 关系选择器

* html元素关系
  * 父元素
    * 直接包含子元素
  * 子元素
    * 直接
  * 祖先元素
    * 直接或间接包含后代
    * 一个元素的父元素也是它的祖先元素
  * 后代元素
    * 直接或间接
  * 兄弟元素
    * 拥有相同父元素的元素
* 子元素选择器
  * 父元素 > 子元素{}
* 后代元素选择器
  * 祖先 后代{}
* 选择下一个兄弟
  * 前一个 + 下一个{}
  * 两个元素必须紧挨着，中间不能有其它元素
* 选择下边所有的兄弟元素
  * 兄 ~ 弟{}

#### 5 属性选择器

* [属性名] 选择含有指定属性的元素
* [属性名=属性值]
* [属性名^=属性值] 属性值以指定值开头的元素
* [属性名$=属性值] 结尾
* [属性名*=属性值] 包含 

#### 6 伪类选择器

* 伪类（不存在的类，特殊的类）

  * 用于描述一个元素的特殊状态

    * eg. 第一个子元素、被点击的元素、鼠标移入的元素...

  * 伪类一般以:开头

    * eg. :first-child 第一个子元素 :last-child 

    * :nth-child(n) n表示0到正无穷 2n(even)表示偶数位 2n+1(odd)表示奇数位

  * 以上伪类都是根据所有子元素进行排序

  * :first-of-type :last-of-type :nth-of-type

    * 只在同类型中排序

  * :not() 否定伪类

* 超链接的伪类 <a>

  * 没访问过的链接
    * :link，正常的链接
  * 访问过的链接
    * :visited
    * 由于隐私原因，:visited伪类只能修改颜色
  * 鼠标移入的状态
    * :hover（针对所有元素）
  * 鼠标点击
    * :active（针对所有元素）

#### 7 伪元素选择器

* 页面中一些特殊的并不真实存在的元素（特殊的位置）
  * ::first-letter
  * ::first-line
  * ::selection
  * ::before 元素的开始
  * ::after 元素的结尾
    * before和after必须结合content属性使用
    * content:'abc'; 通过CSS加入无法选中

#### 8 样式的继承

* 为元素设置的样式也会应用到它的后代元素上
* 并不是所有的样式都会被继承，背景相关、布局相关等不会被继承（可查文档）

#### 9 选择器的权重

* 样式的冲突
  * 不同选择器，选择相同元素，为相同样式设置不同的值
  * 发生样式冲突时，应用哪个样式由选择器权重（优先级）决定
* 选择器的权重
  * 内联样式 -> 1000
  * id选择器 -> 100
  * 类和伪类选择器 -> 10
  * 元素选择器 -> 1
  * 通配选择器 -> 0
  * 继承的样式 -> 没有权重
  * 比较优先级时，将所有选择器权重相加计算后比较（分组选择器单独计算）
  * 选择器权重累加不会超过其最大的数量级 eg. 类选择器再高也不会超过id选择器
  * 优先级计算后相同，优先使用靠后的样式
* ！important
  * 在样式后加上！important，该样式会获得最高优先级（慎用）

#### 10 单位

* 长度单位：
  * 像素px
  * 百分比%：属性值可以设置为相对于父元素的百分比
  * em：相对于元素字体大小计算 (elememt)
    * 1em = 1 front-size，根据字体大小改变（默认16px）
  * rem：相对于根元素(html)的字体大小计算 (root element)
    * html{front-size}
* 颜色单位：
  * 颜色名
  * RGB值 rgb(红色，绿色，蓝色) 0-255(0-100%) 光的三原色
    * (0, 0, 0)灯关了 黑色
    * (255, 255, 255)最强光 白色
  * RGBA rgb(红色，绿色，蓝色，透明度)
  * 十六进制的RGB值
    * #红色绿色蓝色 浓度 00-ff
    * 如果颜色两位两位重复可以简写 #aabbcc -> #abc
  * HSL值 HSLA值
    * H hue 色相 0-360
    * S  saturation 饱和度 0-100% 
    * L lightness 亮度 0-100%
* 表格样式
  * border-spacing 指定边框间距
  * border-collapse: collapse 设置边框合并
  * 间隔行变色
    * tr:nth-child(odd){background-color: red}

  * tr不是table的子元素
    * 如果表格中没有tbody而是直接使用tr，那么浏览器会自动创建一个tbody，并且将tr全部tbody中

  * 默认元素在td中是垂直居中的
    * vertical-align可以修改 top/bottom
    * text-alighn: center

  * display: table-cell


### CSS布局

#### 1 文档流 normal flow

* CSS分层中的最底层是文档流，文档流是网页的基础，创建的元素默认在文档流中排列
* 元素在文档流中的特点：
  * 块元素
    * 独占一行，自上向下
    * 默认宽度是父元素的全部
    * 默认高度是被内容撑开
  * 行内元素
    * 只占自身大小，自左向右，可以换行（书写习惯一致）
    * 默认高度和宽度都被内容撑开

#### 2 盒子模型 box model

* CSS将页面中的所有元素都设置为了一个矩形盒子

* 因而页面布局变成将不同的盒子摆放到不同的位置

* 一个盒子的可见框大小 = 内容区 + 内边距 + 边框

* 每一个盒子都有以下几个部分组成
  * 内容区 content
    * 子元素和文本内容在内容区排列
    * 大小由width、height属性设置
  * 内边距 padding
    * 内容区和边框之间的距离
    * 四个方向：padding-xxx(top, right, bottom, left)
    * 内边距设置会影响盒子大小
    * 背景颜色会延伸到内边距上
    * 赋值同width
  * 边框 border
    * 边框属于盒子边缘，边框里边属于盒子内部，出了边框都是盒子外部
    * 边框大小会影响整个盒子大小
    * border-width: 默认3px，可以指定四个方向的边框宽度
      * 四个值：上 右 下 左
      * 三个值：上 左右 下
      * 两个值：上下 左右
      * 一个值：上下左右
      * border-xxx-width top right bottom left
    * border-color: 默认使用color值
      * border-xxx-color
      * 赋值同width
    * border-style: 默认值none
      * solid 实线
      * dotted 点状虚线
      * dashed 虚线
      * double 双线
      * 赋值同width
    * border简写 border: solid 10px orange 无顺序要求，border-xxx同理
  * 外边距 margin
    * 不会影响盒子可见框大小，但是会影响盒子的位置，盒子的实际占用空间
    * 四个方向：margin-xxx(top, right, bottom, left)
    * 可以为负值，表示相反方向
    * 赋值同padding
  
* 水平方向布局
  * 元素在其父元素中水平方向的位置由几下几个属性共同决定
    * margin-left
    * border-left
    * padding-left
    * width 默认auto
    * padding-right
    * border-right
    * margin-right
  * 一个元素在其父元素中，水平布局必须满足以下等式
    * margin-left + border-left + padding-left + width + padding-right + border-right + margin-right = 其父元素内容区的宽度
    * 等式不成立成为过度约束，那么等式会自动调整
    * 浏览器会自动调整margin-right值使等式满足
    * width/margin-left/margin-right可以设置为auto，如果某个值设置为auto则会自动调整auto那个值以使等式成立
    * 如果将一个宽度和一个外边距设置为auto，则宽度会调整到最大，设置为auto的外边距会自动为0 (宽度优先)
    * 如果将两个编剧设置为auto，宽度固定值，则会将外边距设置为相同的值
      * 用于使一个元素在父元素中居中 eg. width:xxxpx; margin:0 auto;
  
* 垂直方向的布局
  * 默认情况下父元素高度被内容撑开
  * 子元素在父元素内容区中排列
    * 如果子元素大小超过了父元素，则子元素会从父元素中溢出
    * 属性overflow来设置父元素如何处理溢出的子元素
      * 可选值：
        * visible 默认值  会溢出在外部显示
        * hidden 溢出内容会被剪裁
        * scroll 生成两个滚动条，通过滚动条查看完整内容
        * auto 根据需要生成滚动条
    * overflow-x overflow-y
  
* 垂直外边距的折叠（重叠）
  * 相邻的垂直方向的外边距会发生重叠现象
  
  * 兄弟元素
    * 垂直外边距取两者之间的较大值
    
    * 特殊情况：如果相邻的外边距一正一负，则取两者的和
    
      ​					如果相邻的外边距都是负，则取两者绝对值较大的
    
  * 父子元素
  
    * 父子元素间相邻外边距，子元素的会传递给父元素（上外边距）
    * 会影响布局，需要处理
    * 思路：让元素不相邻
      * .box1::before{content: ''; display: table;}
      * 完整版+高度塌陷问题，使用clearfix类
        * .clearfix::before, .clearfix::after{content: '';display: table; clear: both;}

#### 3 行内元素盒模型

* 行内元素不支持设置宽度和高度
* 可以设置padding，但是垂直方向padding不会影响页面的布局
* 可以设置border，但是垂直方向border不会影响页面的布局
* 可以设置margin，但是垂直方向margin不会影响页面的布局
* display属性
  * 可选值：
    * inline 将元素设置为行内元素
    * block 设置为块元素
    * inline-block 设置为行内块元素（既可以设置宽度和高度，又不会独占一行）
    * table 设置为表格
    * none 元素不在页面中显示 隐藏不占据位置f
* visibility
  * 可选值
    * visible
    * hidden 隐藏不显示，但仍占据位置
* opacity:0 透明度为0隐藏元素，仍占据位置

#### 4 浏览器的默认样式

* 浏览器存在默认样式

* 会影响页面的布局，通常情况下编写网页时必须去除浏览器的默认样式（PC端）

* *{

  ​	margin: 0;

  ​	padding: 0;

  }

* 充值样式表：专门用来对浏览器的样式进行重置

  * reset.css 直接去除浏览器默认样式
  * normalize.css 对浏览器默认样式进行统一



#### 5 盒子的大小

* 默认情况，盒子可见框大小由内容区、内边距和边框共同决定
* box-sizing用来设置盒子尺寸的计算方式（设置width和height的作用）
  * 可选值
    * content-box 默认值，宽度和高度用来设置内容区的大小
    * border-box 宽度和高度用来设置整个盒子可见框的大小

#### 6 轮廓阴影和圆角（边框）

* outline 用来设置元素的轮廓线
  * 用法和border一模一样
  * 和border不同点，轮廓不会影响可见框大小，即不会影响页面布局
* box-shadow 用来设置元素的阴影效果，阴影不会影响页面布局
  * 第一个值 水平偏移量 设置阴影水平位置
  * 第二个值 垂直偏移量
  * 第三个值 阴影的模糊半径
  * 第四个值 颜色
* border-radius 用来设置圆角
  * border-xxx-yyy-radius (xxx -> top/bottom, yyy -> left/right)
    * 单位px
    * 一个值 圆
    * 两个值 椭圆
  * border-radius 
    * 四个值
    * 三个值
    * 两个值
    * 一个值

#### 7 浮动

* 通过浮动可以使一个元素向其父元素的左侧或右侧移动
  * float设置元素的浮动
    * 可选值
      * none 默认值 不浮动
      * left
      * right
  * 注意：元素设置浮动以后，水平布局等式失效
* 元素设置浮动以后，会完全从文档流中脱离，不再占用文档流的位置，所以元素下边的还在文档流中的元素会自动向上移动
* 总结浮动特点
  * 浮动元素会完全从文档流中脱离，不再占用文档流的位置
  * 设置浮动以后元素会向父元素的左或右侧移动
  * 浮动元素默认不会从父元素中移除
  * 浮动元素向左右移动时，不会超过它前边的其他浮动元素
  * 如果浮动元素的上边是一个没有浮动的块元素，则浮动元素无法上移
  * 浮动元素不会超过它上边的浮动的兄弟元素，最多就是和它一样高
* 简单总结：浮动用于水平布局

#### 8 浮动的特点

* 浮动元素不会盖住文字，文字会自动环绕在浮动元素周围
* 元素设置浮动以后，会从文档流中脱离，元素的特点也会发生变化
* 元素脱离文档流后的特点
  * 块元素：
    * 不再独占一行，display属性完全失效
    * 宽度和高度可以设置，
    * 默认都被内容撑开
  * 行内元素
    * 变成块元素，特点和块元素一样
  * 脱离文档流以后，不需要区分块和行内元素了

#### 9 简单的布局

* 浮动布局

#### 10 高度塌陷

* 在浮动布局中，父元素的高度默认是被子元素撑开的
  * 当子元素浮动后，其会完全脱离文档流，无法撑起父元素的高度，导致父元素高度丢失
  * 父元素高度丢失后，其下的元素会自动上移，导致页面布局混乱
* 高度塌陷是浮动布局中比较常见的一个问题，这个问题必须处理
* BFC block formatting context 块级格式化环境
  * BFC是一个CSS的一个隐含属性，可以作为一个元素开启BFC
  * 开启该元素会变成一个独立的布局区域
  * 元素开启BFC后特点
    * 元素不会被浮动元素所覆盖
    * 父元素开启BFC，子元素和父元素外边距不会重叠
  * 特殊方式开启BFC
    * 设置元素的浮动（不推荐）
    * 元素设置为行内块元素（不推荐）
    * 元素的overflow设置为一个非visible的值
      * overflow: hidden（常用）
* clear属性：清楚浮动元素对当前元素所产生的的影响
  * 可选值
    * left
    * right
    * both 清楚两侧中最大影响的那侧
  * 原理：设置清楚浮动以后，浏览器会自动为元素添加一个上外边距，以使其位置不受其他元素的影响
* 高度塌陷最终节约方案
  * .box1::after{content: '';display: block;clear: both;}
  * 高度塌陷 + 外边距重叠问题，使用clearfix类
    * .clearfix::before, .clearfix::after{content: '';display: table; clear: both;}

#### 11 定位 position

* 定位是一种更加高级的布局方法
* 通过定位可以将元素摆放到页面的任意位置
* 使用position属性来设置定位
  * 可选值
    * static(默认)：元素框正常生成。块级元素生成一个矩形框，作为文档流的一部分；行内元素则会创建一个或多个行框，置于其父元素中。
    * relative：元素框相对于之前正常文档流中的位置发生偏移，并且原先的位置仍然被占据。发生偏移的时候，可能会覆盖其他元素。
    * absolute：元素框不再占有文档流位置，并且相对于包含块进行偏移(所谓的包含块就是最近一级外层元素position不为static的元素)
    * fixed：元素框不再占有文档流位置，并且相对于视窗进行定位
    * sticky：(这是css3新增的属性值)粘性定位，官方的介绍比较简单，或许你不能理解。其实，它就相当于relative和fixed混合。最初会被当作是relative，相对于原来的位置进行偏移；一旦超过一定阈值之后，会被当成fixed定位，相对于视口进行定位。
* 偏移量(offset)
  * 当元素开启了定位以后，可以通过偏移量来设置元素的位置
  * top
    * 定位元素和定位位置上边的距离
  * bottom
    * 定位元素和定位位置上边的距离
    * 垂直方向由top和bottom两个控制，通常只会使用其一
  * left
  * right
* 相对定位 relative
  * 开启后，如果不设置偏移量，元素不会发生任何的变化
  * 相对定位是参照于元素在文档流中的位置定位的
  * 相对定位会提升元素的层级
  * 相对定位不会使得元素脱离文档流
  * 相对定位不会改变元素的性质（块、行内元素）
* 绝对定位 absolute
  * 开启后，不设置偏移量，元素的位置不会发生变化
  * 开启后，元素会从文档流中脱离
  * 绝对定位会改变元素的性质，行内变成块，块的宽高被内容撑开
  * 绝对定位会提升元素的层级
  * 绝对定位元素是相对于其包含块进行定位的
    * 包含块(containing block)
      * 正常情况：包含块是离当前元素最近的祖先块元素
      * 绝对定位情况下：包含块是离它最近的开启了定位的祖先元素
        * 如果所有的祖先元素都没有开启相对定位，则根元素就是它的包含块
        * html -> 根元素、初始包含块
* 固定定位 fixed
  * 固定定位也是一种绝对定位，所以固定定位的大部分特点都和绝对定位一样
  * 唯一不同的是，固定定位永远参照于浏览器视口进行定位
  * 固定定位元素不会随网页的滚动条滚动
* 粘滞定位 sticky （兼容性不好）
  * 粘滞定位和相对定位的特点基本一致，不同的是粘滞定位可以在元素到达某个位置时将其固定

#### 11 绝对定位元素的布局

* 开启绝对定位之后
  * 水平布局等式变为 7个属性 + left + right = 包含块的内容区的宽度
  * 此时规则和之前一样，当发生过度约束时：
    * 如果9个值中没有auto则自动调整right值以满足等式
    * 如有auto，则自动调整auto
    * 可设置auto的值
      * magrin width left right
      * 因为left和right的默认值是auto，所以如果不指定left和right，则等式不满足时会自动调整这两个值
  * 垂直方向的等式也必须要满足
    * top + margin-top/bottom + padding-top/bottom + border-top/bottom + height = 包含块的高度

#### 12 元素的层级

* 对于开启了定位的元素，可以通过z-index属性来指定元素的层级
  * z-index需要一个整数作为参数，值越大优先级越高
  * 层级相同，优先显示靠下的
  * 祖先元素的层级再高也无法盖住后代元素

#### 13 字体和背景 font&background

* color 前景色

* font-size

  * 单位 em rem

* font-family 字体族

  * 可选值
    * serif 衬线字体
    * sans-serif 非衬线字体
    * monospace 等宽字体
      * 指定字体类别，浏览器自动使用该类别下的字体
  * 可以同时指定多个字体，逗号隔开，优先匹配使用最前面的字体

* font-face可以讲服务器中的字体直接提供给用户使用

  * @font-face{ font-family:'myfont';src: url(path) format("truetype");}

* 图标字体 iconfont

  * 将图标设置为字体，然后通过font-face引入

  * 比图片小、灵活

  * fontawesome 使用步骤

    1. 下载

    2. 解压

    3. css和webfonts移动到项目中，同一级目录下

    4. all.css引入网页

    5. 使用图标字体

    6. 直接通过类名使用

       * <i class="fas xxxxx"></i>

       * <i class="fab xxxxx"></i>

  * 通过伪元素设置图标字体

    1. 找到要设置图标的元素通过before或after选中
    2. 在content中设置字体的编码
    3. 设置字体的样式

  * 通过实体来使用图标字体

    * &#x图标编码
    * <span calss='fas'>&#xxxxx;</span

  * iconfont 阿里！

* 行高 line height

  * 文字占有的实际高度
  * line-height设置行高 px/em/整数，字体的倍数，默认1.33
  * 字体框
    * 字体存在的格子，front-size实际就是设置字体框的高度
  * 行高会在字体框上下平均分配
  * 可以将line-height和height设置一样的值，使单行文字在一个元素中垂直居中
  * 行高也常用于设置文字的行间距
    * 行间距 = 行高 - 字体大小

* 字体的简写属性

  * 简写属性font
  * 语法
    * front: （可省略的： font-weight font-style）字体大小/行高 字体族（必须是倒数两个属性）
    * 行高 可以省略不写 如果不写就使用默认值1.2
  * font-weight 
    * normal 默认 不加粗
    * bold 加粗
    * 100-900 9个级别（需要电脑里有对应级别的字体）
  * font-style
    * normal 默认
    * italic 斜体

* 文本的水平和垂直对齐

  * text-align 文本水平对齐
    * 可选值
      * left 默认
      * right
      * center
      * justify 双端对齐
  * vertical-align 设置元素垂直对齐方式
    * 可选值
      * baseline 默认值 基线对齐
      * top 顶部对齐
      * bottom
      * middle
      * 数值 正负px

* 其他的文本样式

  * text-decoration 设置文本修饰
    * 可选值 + （颜色 + 样式dotted...）
      * none 
      * underline 下划线
      * line-through 删除线
      * overline 上划线
  * white-space 设置网页如何处理空白
    * 可选值
      * normal
      * nowrap 不换行
      * pre 保留空白
    * overflow: hidden
    * text-overflow: ellipsis

#### 14 背景

* background 背景相关简写属性 
  * position/size size必须在postion后面 “/”隔开
  * origin在前clip在后 
  * 其他属性无要求 
* background-color 背景颜色
* background-image: url() 背景图片
* background-repeat 设置背景图片重复方式
  * 可选值
    * repeat 默认x y轴重复
    * repeat-x
    * repeat-y
    * no-repeat
* background-positon 设置背景图片位置
  * 方式一：top left right bottom center
    * 用两个词组合在九宫格中定位
    * 如果只写一个值，第二个默认center
  * 方式二：通过偏移量设置 水平 + 垂直
* background-clip 设置背景范围
  * 可选值
    * border-box 默认值，背景会出现在边框下边
    * padding-box 背景只出现在内容区和内边距
    * content-box 只出现在内容区
* background-origin 背景图片的偏移量计算的原点
  * 可选值
    * padding-box 默认值
    * content-box 
    * border-box
* background-size 设置背景图片大小
  * 第一个值宽度 第二个值高度
  * 只写一个宽度 第二个默认auto
  * 可以用百分比
  * cover 图片比例不变，将元素铺满
  * contain 比例不变，在元素中完整显示
* background-attachment 设置背景图片是否跟随元素移动
  * 可选值
    * scroll 默认值 跟随移动
    * fixed 固定不移动

* 图片属于网页中的外部资源，外部资源都需要浏览器单独发送加载请求。浏览器加载外部资源是按需加载的，用时才加载。
* 解决图片闪烁问题
  * 可以将多个图片保存到同一张大图片中，然后通过调整background-position来显示图片
  * 这样图片会同时加载到网页中，有效避免闪烁问题出现
  * CSS-Sprite 雪碧图
* 渐变
  * ！渐变是图片，如要通过background-image设置
  * background-image
    * linear-gradient(to right, red,yellow) 线性渐变 
      * 开头可以指定方向
        * to left/right/bottom/top/xxxdeg/xturn
        * 可以指定多种颜色，默认情况平均分布
        * 也可以手动指定渐变分布情况，red 50px，红色从50px开始
    * repeating-linear-gradient 平铺的线性渐变 
      * repeating-linear-gradient(red 0px, yellow 50x)
    * redial-gradient(red, yellow) 径向渐变 发散
      * 语法：radial-gradient(大小 at 位置, 颜色 位置, 颜色 位置, ...)
      * 默认情况下渐变形状根据元素的形状要计算
        * 正方形 -> 圆形 长方形 ->椭圆
      * 手动指定径向渐变大小 redial-gradient(100px 100px, red, yellow)
        * circle/ellipse  
        * redial-gradient(circle, red, yellow)
      * 指定渐变的位置
        * redial-gradient(100px 100px at center ,red, yellow)
        * redial-gradient(100px 100px at 100px 0px ,red, yellow)

#### 15 雪碧图 CSS-Sprite

* 使用步骤

  1. 确定好要使用的图标

  2. 测量图标大小
  3. 根据测量结果创建一个元素
  4. 将雪碧图设置为元素的图片背景
  5. 设置一个偏移量以显示正确的图片
* 特点

  * 解决图片闪烁问题
  * 一次性将多个图片加载进页面，降低请求次数，加快访问速度，提升用户体验

#### 16 设置网站的图标

* 网站的图片一般存在网站根目录下，名字一般叫favicon.ico
* link rel="icon" hef="./favicon.ico"

#### 17 弹性盒 flex

* 是CSS的又一种布局手段，它主要用来代替浮动来完成页面的布局
* flex可以使元素具有弹性，让元素可以跟随页面的大小的改变而改变
* 弹性容器
  * 要使用弹性盒，必须先将一个元素设置为弹性容器
  * 通过display设置弹性容器
    * display: flex 设置为块级弹性容器
    * display: inline-flex 设置为行内的弹性容器
* 弹性元素
  * 弹性容器的子元素（子元素潜在说明是直接后代）是弹性元素（弹性项）
  * 一个元素可以同时是弹性容器和弹性元素
* 弹性容器的样式
  * flex-direction 指定容器中弹性元素的排列方式
    * 可选值
      * row 默认值，弹性元素在容器中水平排量，左到右
        * 主轴 自左向右
      * row-reverse
        * 主轴 自右向左
      * column 上到下
      * column-reverse
    * 主轴
      * 弹性元素的排列方向称为主轴
    * 侧轴
      * 与主轴垂直的方向称为侧轴
  * flex-wrap
    * 设置弹性元素是否在弹性元素中自动换行
    * 可选值
      * nowrap 默认值
      * wrap 元素沿着侧轴方向自动换行
      * wrap-reverse 沿着侧轴反方向换行
  * flex-flow(wrap 和 direction的简写属性)
    * flex-flow: row wrap
  * justify-content 如何分配主轴上的空白空间 justify表示主轴 align表示侧轴
    * 可选值
      * flex-start 元素沿着主轴起边排列
      * flex-end 元素沿着主轴终边排列
      * center 居中排列
      * space-around 空白分布到每个元素的两侧
      * space-between 空白均匀分布到元素间
      * space-evenly 空白分布到元素的单侧
  * align-items 元素在侧轴上如何对齐（元素间的关系）单行
    * 可选值
      * stretch 默认值，将元素的长度设置为相同的值
      * flex-start 元素不会拉伸，沿着侧轴起边对齐
      * flex-end
      * center
      * baseline 基线对齐
  * align-content 侧轴空白空间的分布 多行
  * align-self 用来覆盖当前弹性元素上的align-items（弹性元素的属性）
* 弹性元素的样式
  * flex-grow 指定弹性元素伸展的系数
    * 当父元素有多余的空间时，子元素如何伸展
    * 父元素的剩余空间，按照系数比例分配
  * flex-shrink 指定弹性元素收缩的系数
    * 缩减多少是根据 缩减系数 和 元素大小 来计算的
    * 当父元素的空间不足以容纳所有子元素时，如何对子元素进行收缩
    * 默认值为1等比例收缩，0不收缩
  * flex-basis 元素基础长度
    * 指定元素在主轴上的基础长度
      * 如果主轴为横向，指定元素宽度
      * 如果主轴为纵向，指定元素高度
      * auto 默认值，参考元素自身
      * 如果传递了具体的数值，以该值为准
  * flex 简写属性
    * 分配剩余空间的长度份数
    * flex 增长 缩减 基础
      * initial 0 1 auto
      * auto 1 1 auto
      * none 0 0 auto
  * order 决定弹性元素的排列顺序





### CSS动画 Animation

#### 1 过渡效果

* transition 过渡效果的简写，可以同时设置
  * 如果要写延迟，两个时间中第一个是持续时间，第二个是延迟时间，其它无顺序要求
  * 通过过渡可以指定一个属性发生变化时的切换方式
  * 提升用户体验
* transition-property 指定要执行过渡的属性
  * 多个属性间,隔开
  * 所有属性都要使用,all关键字
  * 大部分属性都支持过渡效果，注意过渡效果必须是一个有效值向另一个有效值过渡，auto不支持
* transition-duration 指定过渡效果持续时间
  * 时间点为s和ms
  * 可以按照属性分别指定时间
* transition-timing-function 过渡的时序函数，指定过渡的执行方式
  * 可选值
    * ease 默认值，慢速开始，先加速再减速
    * linear  匀速运动
    * ease-in 慢速开始，加速运动
    * ease-out 慢速结束，减速运动
    * esae-in-out 先加速再减速
    * cubic-bezier() 指定时序函数 cubic-bezier.com
    * steps() 分步执行过渡效果
* transition-delay 过渡效果的延迟
  * 等待一段时间后再执行过渡

#### 2 动画 animation

* 动画和过渡类似，都是实现动态效果

  * 过渡需要在某个属性发生变化时触发，动画自动触发

* 设置动画效果，必须要设置一个关键帧，关键帧设置了动画执行的每一个步骤

  * @keyframes test {

    ​	from(0%){

    ​	}

    ​	to(100%){

    ​	}

    }

* animation-name 要对当前元素生效的关键帧名字

* animation-duration

* animation-timing-function

* animation-delay

* animation-iteration-count 动画执行次数

  * 可选值
    * 次数
    * infinite

* animation-direction 指定动画运行方向

  * 可选值
    * normal 默认值 从from到to
    * reverse
    * alternate 从from到to 反复来回
    * alternate-reverse

* animation-play-state 设置动画的执行状态

  * 可选值
    * running 默认值
    * paused 暂停

* animation-fill-mode

  * 可选值
    * none 默认值 动画执行完毕元素回到原来的位置
    * forwards 动画执行完毕元素停止在动画结束的位置
    * backwards 动画延迟等待时，元素就会处于开始状态
    * both 结合forwads和backwards

* animation简写同transition

#### 3 变形

* 通过CSS个改变元素的形状或位置
  * 变形不会影响到页面的布局
* transform 用来设置元素的变形效果
  * 可选值
    * translateX(100px) 沿着x轴平移100px
    * translateY()
    * translateZ() 调整元素在z轴的位置，正常情况是调整元素和人眼之间的距离，距离越大，元素离人越近
      * 默认情况下不支持透视，如果需要看见效果，需要设置网页的视距
      * perspective: 800px
    * 百分比相对于自身计算的

#### 4 旋转

* 使元素沿着x/y/z旋转指定角度
* transform
  * 可选值
    * rotateX()
    * rotateY()
    * rotateZ()
      * deg/turn/
* 变形旋转可以拼接
  * transform: translateZ(100px) rotateY(180deg)
* backface-visibility: 显示元素背面
  * hidden
  * visible
* 3D变形
  * transform-style: preserve-3D

#### 5 缩放

* transform
  * 可选值
    * scaleX()
    * scaleY()
    * scale
    * scaleZ()
* transform-origin
  * 可选值
    * center 默认值
    * x y坐标

#### 6 像素

前端开发中，像素要分成两种情况讨论：CSS像素 和 物理像素

* 物理像素：屏幕小点点

* CSS像素：编写网页时的像素

  * 浏览器在显示网页时，需要将CSS像素转换为物理像素然后再呈现
  * 一个CSS像素最终由几个物理像素显示，由浏览器决定
    * 默认情况下 PC端 一个CSS像素 = 一个物理像素

* 视口（viewport）

  * 视口就是屏幕中用来显示网页的区域

  * 可以通过查看视口的大小，来观察CSS像素和物理像素的比值

  * 默认情况

    * 视口宽度 1920px（CSS像素）

      ​				1920px （物理像素）

  * 可以通过改变视口的大小来改变CSS像素和物理像素的比值

#### 7 移动端像素

智能手机的像素点 远远小于 计算机的像素点

* 问题： 一个宽度为900px的网在ip6（750 x 1334）中如何显示？

  * 默认情况下，移动端的网页都会将视口设置为980像素（css像素）
  * 以确保pc端网页可以在移动端正常访问
  * 如果网页宽度超过了980，移动端浏览器会自动对网页缩放以完整显示网页
  * 所以，基本上大部分的pc端网站都可以在移动端正常浏览，但往往都不会有一个好的体验
    * ​	为了解决这个问题，大部分网站会专门为移动端设计网页

* 编写移动页面时，必须要确保一个比较合理的像素比

  * 1css像素对应2个物理像素
  * 1css像素对应3个物理像素

* 可以通过meta标签设置视口大小

* 完美视口

  * 每一款移动设备设计时，都会有一个最佳像素比

    * 只需要将江苏必设置为该值即可得到一个最佳效果

  * width=device-width 表示设备的宽度（完美视口）

  * <meta name="viewport" content="width=device-width, initial-scale=1.0">
    </meta>

* 移动端开发不能用px布局

  * 不同设备视口不一样，显示效果会不同
  * vw表示视口的宽度 （viewport width）
  * 100 vw =  一个视口的宽度
  * 1vw = 1%一个视口的宽度
  * vw这个单位相对于视口宽度进行计算

* vm适配

  * 1 rem = 1 html字体大小
  * 网页中字体大小最小（除了0）为12px
  * 所以一般是用100/750

### 练习

#### 2 京东左导航

* 要让一个文字在父元素中垂直居中，秩序将父元素的line-height设置为一个和父元素height一样的值
* 去除文本下划线 texe_decoration: none;

#### 3 网易新闻列表

* 文字加粗：font-weight: bold;

#### 4 w3school导航条

#### 5 京东轮播图

* background-clip: content-box;
  * 将背景颜色值设置到内容区，边框和内边距不再有背景颜色

#### 6 京东顶部导航

### 项目实践 mi.com

1. 创建项目文件夹 css/fa/img 和首页index.html
2. 导入fontawesome中的css和webfonts、导入清除默认样式reset.css
3. 创建公共base.css、首页index.css
4. 往index.html导入需要的项目css文件
5. 往base.css写入
   * .clearfix 解决高度塌陷
   * body 项目字体设置等
   * .w 项目宽度 和 居中
6. 对首页顶部导航条布局
   * 左侧导航
   * 右侧导航
   * 购物车
7. 导航条基本样式





