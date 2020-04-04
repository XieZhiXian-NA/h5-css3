# css

## 选择器

+ 伪元素：表示页面中一些特殊的并不真实存在的元素（特殊的位置）
  + ::first-letter 第一个字母
  + ::befor  标签元素开始位置
  + ::after  标签元素结束位置
    > ---必需结合content属性 才能展示出来

+ 伪类：不存在的类 描述一个元素的特殊状态 被点击、鼠标移入、第一个子元素
  + :first-child li:first-child li是第一个子元素
  + li:nth-child(x) li是第x个子元素
    > 特殊值 n:0-正无穷 全选中 (2n | even)偶数位 （2n+1 | odd）奇数位
  + li:first-of-type相同类型的元素 选择第一个
  + :not()排除某些符合条件的元素  
    > ----li:not(:nth-child(3))

  + :link 没访问过的链接
  + :visited 访问过的链接 只能修改颜色
  
  + :hover 移入鼠标 所有的元素都可用
  + :active 鼠标点击 -------------
  
## 样式

+ 样式的继承：发生在祖先与后代之间 将统一的样式设置到共同的祖先元素上
  > 并不是所有的样式都会被继承 背景(background-color)、布局等
      没有设置背景默认就是透明的  子元素的背景是透明的 父元素的背景透过了子元素 子元素也就像继承一样显示父元素的背景

+ 权重：!important 》 内联样式 》 id选择器 》 类/伪类选择器 》元素选择器 》通配选择器* 》继承样式
  + 相加计算权重 除了分组选择器div,p,span{}单独计算 不相加
  + 选择器的相加 单独的一种类型 如：多个类选择器相加最大值即使很大优先级也不会超过id/内联
  + 权重相同时，优先选择最下面的选择器 
  + *任何选择器都会覆盖它
  + 样式冲突 不同的选择器选择同一个的元素同一个属性不同的值 

## 单位

+ 长度单位 像素px越小 越清晰
  > 相同的像素在不同的显示屏下 大小不一样
  + 百分比
    > 属性值相对于父元素内容区属性值的百分之几 随父元素改变而该变
  + em 移动端
    > 相对于自身元素字体大小 默认字体大小16px 随字体的大小而改变
  + rem 移动端
  > 相对于根元素字体的大小 html

+ 颜色单位
  + 颜色名设置 red
  + rgb(1,0,0)  三种颜色的不同浓度来表示不同的颜色 0-255
  + rgba(1,0,0,.5)
  + 十六进制 00~ff  #bbffaa
  + p标签不能放任何的块元素

## 文档流

+ 文档流 网页有多层 一层一层堆叠而成 css为每一层设置样式 最下面一层称为文档流
  > 所创建的元素默认都是在文档流中排列
  + 元素状态 ：在文档流中  脱离文档流
    + --在文档流中
      + 块元素 会在页面中独占一行
        > 默认宽：把父容器铺满
        > 默认高：被内容撑开(子元素)
      + 行内元素 不会独占一行 水平排列 一行排列不了 下一行
        > 默认宽、高：都是被内容撑开
      + 盒模型
        > 对页面的布局就是摆放盒子到指定的位置
          content:内容区   大小由height、width设置
          padding:内边距 背景色设置会延申至内边距 不仅仅只是内容区显示
                        padding-top padding-bottom
                        padding-right padding-left

          border:边框   width 样式(solid) color   
          > border-width 指定四个方向的边框的宽度 值按顺时针 上右下左
            border-right:none不设置样式           三个值 上 左右 下
            border-top-width 单独指定
            border-color 边框的颜色

          margin:外边距 设置与其它盒子的间距 不会影响盒子可见宽的大小 会影响位置
          > 设置正值 向相同的方向
            元素在页面中是自左向右的顺序排列 设置左、上移动元素自身 设置下、右移动的是其他元素
            设置负值 向相反的方向移动
            margin-right 设置默认不会有任何影响 一般由浏览器自动调整
      + 块元素盒模型
        > 水平方向布局
          元素在父元素中的水平方向的位置由以下几个属性决定
          margin-left 0
          border-left 0
          padding-left 0
          width auto
          padding-right 0
          border-right 0
          margin-right 0
          >> 子元素在父元素中 父元素内容区=（margin-left + border-left + padding-left + width + padding-right + border-right + margin-right）
          以上等式必须成立 若等式不成立 过度约束 等式会自动调整
          1:如果没有auto 会自动调整margin-right 使等式成立
          2:有三个值 width margin-left margin-right三个值可以设置为auto 若其中有一个设置了auto 调整设置了auto的值
          3:若width:auto且margin-left:auto 则宽度会最大 margin-left=0
          4:margin-left=auto且margin-right=auto width设置为固定 则左右两边宽度一样 用来设置水平居中 A---maign:0 auto B--子元素宽度设置固定值 
          5:若width>父元素的内容区 为了使等式成立 则浏览器调整margin-right为负值

      + 垂直方向布局
        > 父容器的高度：默认子元素撑开的高度
          如果子元素的高度超出了父元素的高度 子元素会从父元素中溢出
          在父元素上设置overflow处理溢出
          visible:溢出部分会显示
          hidden:溢出部分隐藏 看不见
          scroll:生成两个滚动条 查看完整的内容
          auto:根据需要自动生成滚动条 水平/垂直/水平-垂直

      + 相邻垂直方向的外边距折叠(重叠)                      兄弟A       兄弟B
        > -兄弟元素：相邻垂直外边距 两者都为正值 取Math.max(margin-top,margin-bottom) good
          -父子元素：相邻垂直上外边距 子元素的上外边距会传递给父元素 erro

      + 行内元素盒模型 像一个字 两个字之间会有间隙
        > 不支持设置width height
          垂直方向padding  A 不会影响页面布局 但是会覆盖B元素一部分
          垂直方向border---------------------------------------
          垂直方向margin--------------------margin-bottom不会使相邻元素下移
          水平方向上的margin-right margin-left不会折叠 会相加

      + display:设置元素显示的状态 为块元素还使行内元素
        > 将行内《=》块元素互相转化
          inline-block 既可以设置宽高又不会独占一行 //不推荐使用
          table表格 
          none元素不在页面中显示不占据位置
          visibility:
              visible:元素正常显示
              hidden:隐藏 位置依然占据位置

  + 浏览器默认样式
    > 默认样式的存在会影响页面的布局 通常情况下 去除浏览器默认的样式
      简单页面布局:
  
      ```css
            *{
            margin:0;
            padding:0
        }
      ````

      复杂页面布局清除干净 引入别人写好的重置样式表 reset完全清除 normalize会统一样式
+ 图片只要设置一个值 高度会自动按比例缩放 
+ 让文字在父元素中居中 则只要在父元素中设置line-height = 父元素的高度height 
  > line-height: 25px;

+ 盒子大小
  + 设置盒子尺寸的计算方式(width height)
  + box-sizing:
    > content-box 宽度和高度是设置内容区域的大小
  
## 轮廓

+ outline:设置元素的轮廓线 
  > 用法与border一样 不会影响到可见框的大小 不会影响到页面的布局
+ 阴影
  > box-shadow:用来设置元素的阴影效果  不会影响到页面的布局 10px 10px 10px color
    默认是在元素的正下方
    >> 设置阴影的偏移量:
       水平偏移量--margin-left 
       垂直偏移量--margin-top
       阴影的模糊半径 值越大 越模糊越像影子
       颜色rgba(0,0,0,.3)透明的颜色
+ 圆角
  > border-radius 
    border-top-left-radius :10px 10px;  水平方向半径 垂直方向半径  不同是是椭圆 相同时是圆
    圆 border-radius:50%
  
## 浮动 

> 可以使多个元素横向排列
  使一个元素向其父元素的左侧或者右侧浮动

+ float:none
  > left 向左浮动(移动)
    right
  > 元素设置为浮动，水平布局的等式不需要强制成立
    且其完全从文档流中脱离 不再占据文档流（父元素）的位置 所以处于其下方的元素会自动向上移动
    1：元素移动时特点 默认不会从父元素中移出 父元素有边界 只能在父元素边界:范围内浮动
    2：浮动元素向左、向右浮动时，不会超过他前边的其他浮动元素A B C的排列 水平
    3：浮动元素不会超过它上边浮动的兄弟元素，最多最多就是和它一样的高垂直 A
    浮动元素A不会盖住文字(p标签) 文字环绕浮动元素                       B C
+ 脱离文档流特点
  + 块元素
    1. 块元素不在独占页面一行
    2. 块元素的宽度和高度默认都被内容撑开
    3. 不再区分块元素和行内元素
+ 浮动缺点
  + 高度塌陷
    > 父元素高度一般不写死 就是为了随着子元素内容变化而变化
      父元素高度（不设置height）默认是子元素内容撑开 
      但是当子元素浮动后 脱离文档流 无法撑起父元素的高度 导致父元素的高度丢失 处于下面的元素就会上移 页面布局混乱
  + 解决方式
    + BFC(block Formatting Context)块级格式化环境
      > 是css隐含的属性，可以为一个元素开启BFC 开启BFC该元素会变成一个独立的布局区域
      > 特点：
        不会被浮动元素所覆盖A A设置为Float后  B开启BFC B不会上移 不会被覆盖
                          B
        子元素和父元素的外边距不会重叠 父元素开启BFC
        开启BFC元素可以包含浮动的子元素
    + overflow:hidden最常见的开启BFC方式
    + clear 清除浮动元素对当前元素产生的影响
      > left  清除float：left的元素    A
        right 清除float:right的元素     b
        both  清除两者最大影响的元素     c  为c清除浮动
        设置清除浮动以后 浏览器会自动为当前元素添加一个上外边距 以使其位置不会受浮动元素的影响
        >> :这种方式是在页面中多添加一个标签 还是要用css解决
        >>:添加伪元素  但是是行内元素不独占一行显示 还是撑不起高度

          ```css
            .box2::after{
                content:''; 
                clear:both;
                display:table
            }
          ```
        解决子元素和父元素的外边距重叠

        ```css
          父元素::before{
          content:'';
          display:table
        }
        ```
        clearfix类 解决了高度塌陷和外边距重叠 

## position

+ 通过定位 将元素摆放到任意位置
+ 浮动宏观上 微观细节上使用定位
+ 只有当元素开启了定位 才可以设置offset(偏移量) 只会移动自己 不会影响他人 margin-top会影响其 他元素 其他元素也会移动

     1. 垂直方向 top bottom
     2. 水平方向 left right
+ static:元素是静止的没有开启定位
+ relative:相对定位
     1. 不设置偏移量 元素不会发生任何变化
     2. 偏移坐标 相对于元素自己之前的位置
     3. 相对定位会提升元素的层级但没有脱离文档流
     4. 是灵魂出窍，原来的位置还在占据着
+ absolve:绝对定位  
    1. 开启绝对定位后 不设置偏移量 元素的位置不会发生变化
    2. 元素会从文档流中脱离
    3. 会改变元素的性质 行内变块 块的高度被内容撑开
    4. 绝对定位会使元素提升一个层级
    5. 偏移坐标 相对于其包含块进行定位的
       > 包含块：
           正常情况下 就是离当前元素最近的祖先块元素  
       > 绝对定位的包含块：
            离他最近的开启了定位的祖先元素
            如果所有的祖先元素都没有开启定位 则根元素(html)是包含块
+ fixed:固定定位 把元素固定到可视窗口中
    1. 也是一种绝对定位
    2. 唯一不同的是 偏移坐标是参照于浏览器的视口(大小固定不变)进行定位
    3. 位置不会随滚动条的滚动而变化位置
+ sticky:粘滞定位 兼容性不好 不推荐使用
    1. 可以在一定高度时固定位置 就不再随滚动条滚动
    2. 类似于相对定位
    3. 偏于坐标 相对于body
+ 绝对定位布局
    1. 水平方向等式 left + margin-left + border-left + padding-left + width + padding-right + border-right + margin-right + right = 父元素的宽度 
    > 如果有auto 则自动设置auto值以调整等式成立
       margin width left right可设置auto  
       left right默认为auto 会自动调整这两个值 left:0 right:0 其他设置为auto才起作用
    > margin 0px auto left:0 right:0 水平居中 
    2. 垂直方向的等式也必须成立 top + margin-top + border-top + padding-top + height + padding-bottom + border-bottom + margin-bottom + bottom = 父元素的高度
    > top bottom默认为auto
    > margin auto 0px top:0 bottom:0 垂直居中
    3. 居中 margin:auto auto; top:0 ;bottom:0;left:0;right:0; 

## 层级

+ 对于开启了定位的元素 z-index设置层级 值越大 层级越高 盖住别人
+ 只要是定位 层级都是一样的  层级一样的时候 默认显示的是最下面（样式表）的元素
+ 祖先元素的层级再高 也不会盖住后代元素
  
## font 矢量图 字体不会失真

+ color 设置字体颜色
+ font-size 字体大小
  > em 相当于当前元素的一个font-size
  > rem 相对于根元素的一个font-size
+ font-family 字体格式 建议用户用什么字体 字体格式是用户电脑里安装的字体格式才能在浏览器中显示
  > 字体类别 大的分类 浏览器会自动使用具体类别的字体
    serif 衬线字体(像钢笔字)
    sans-serif 非衬线字体
    monospace 等宽字体(英文字母 每个字母宽度一样)
  > 可以同时指定多个字体,字体生效时从左到右优先级逐渐降低 最先使用第一个
+ font-face 
  > 可以将服务器上的字体提供给用户使用 font-family:指定字体的名字  src:字体在服务器上的路径 
    `@font-face{font-family:'xzx';src:url('./font.ttf)}`

### 图标字体
  
+ 在网页中 将图标设置为字体 通过font-face形式对字体进行引入 现在直接就是svg
  
### 行高 单行的行高

+ 行高指的是文字占有的实际高度 line-height 
  > 行高为正数 1 = 字体（font-size）的倍数
+ 字体框 font-size 字体存在的格子 实际字体大小 font-size
+ line-height设置为与盒子一样的高度 则字体框就会居中于盒子(line-height-font-size )=剩余的高度被平均分配到字体框的上下 字体框就会居中显示
+ 行间距 = 行高-字体框大小
  
> font:font-style(可省略 默认值normal) font-style(可省略 默认值normal) font-size/行高（行高可省略 默认值normal） font-family 字体简写顺序 后两个为必填项

+ font-weight 字重
  > 默认值 normal 
  > 不加粗 bold加粗 
  > 100-900 九个级别(不推荐使用)
+ font-style 字体风格
  

## 文本

+ text-align 文字的水平对齐
  > left right center-居中对齐 justify-两端对齐
+ vertical-align
  > baseline:默认值 基线对齐 top子元素的顶部和父元素的顶部对齐 bottom middle:
+ 图片的对齐和文本一样 也有个基线 导致图片下边距没有紧贴着底部 设置vertical-align:top 改变基线对齐 则可以紧贴
+ text-decoration        划线 划线的颜色
  > none underline line-through横穿线 overline上划线
    underline red 划线 划线的颜色
+ white-space 设置网页如何处理空白
  > normal nowrap 不换行(出现滚动条) pre保留空白
    多余的字设为省略号:`width:200px white-space:nowrap overflow:hidden text-over-flow:ellipsis`

## 背景

+ 全写没有顺序 
  > position/size(位置/大小)
    origin 在 clip的前面
+ background-color
+ backgroung-image:url('图片位置')
  > 背景图片 > 元素 将会有一部分背景无法完全显示
    背景图片 < 元素  则背景图片会自动在元素中平铺满元素
            =       正常显示
+ background-repeat：背景图片的重复方式
  > repeat 默认值 背景图片沿着x y轴双方向重复
    repeat-x 背景图片只沿着x轴重复
    repeat-y 背景图片只沿着y轴重复
    no-repeat 不重复 背景图片的默认起始坐标0，0 是padding区，不会延申至border区
+ background-position:背景图片的位置 将元素分为九宫格
  > top leftf right bottom center
    使用方位词需要同时指定两个值 background-position：top left  上面左边
  > 通过偏移量指定背景图片的位置                    :100px 100px 水平方向偏移量 垂直方向偏移量
+ background-clip 裁剪 背景色会衍生至border 需要裁剪背景色
  > border-box 默认值 背景色会出现在边框中 
    padding-box 背景色只会出现至内边距
    content-box 背景色只会出现在内容区
+ background-origin 背景图片偏移计算的原点
  > padding-box 默认值 图片的原点从内边距处开始计算
  > content-box 图片的原点是内容区
  > border-box 图片的原点是border区
+ background-size:背景图片的大小
  > cover图片的比例不会改变 将元素铺满 会缺失某一部分
    container 比例不变 将图片完正的在页面中显示

## 渐变

 复杂背景色 可以实现背景由一个颜色向其他颜色过渡的效果

+ 线性渐变 颜色沿着一条直线发生变化 
  > linear-gradient() 可以指定渐变的放向
    >> to left to right to top to bottom
       xxx deg 度数 角度改变方向  turn表示的是圈

  > 可以指定多个颜色 默认平均分配
    >> (red 10px,yellow 20px )red则从10px开始向下渐变  yellow从20px向上渐变  
+ 径向渐变 默认下 正方形：圆 长方形：椭圆
  > radial-gradient(100px 100px at center center,red,yellow)----->radial-gradient(大小 at 位置,颜色)
  > 指定渐变的大小(半径):
    >> circle:圆 ellipse:椭圆 
      close-side只渐变到最近的边

  > 指定渐变的位置:
    >> at center center中心 top left right bottom


## 添加 

+ 隐藏文字
  > text-indent: -9999px;
+ 设置网站的图标 在标题栏和收藏栏显示
  > 网站图片一般都存储在网站的根目录下 名字一般都叫favicon.ico


## 动画

+ transition 过渡 可以指定一个属性发生变化时的切换方式（速度的快慢等）
  > 过渡可以带了一些非常好的效果，提升用户的体验
    transition:all 3s;
    >> transition-property:指定要执行过渡的属性--->只要值是可以计算出来的属性 width,height
       >>> 多个属性间  ，隔开 all表示(多个/所有)的属性
           过渡时 是属性从一个有效值过渡到另一个有效值 auto不是有效值
    >> transition-duration:指定执行过渡的持续时间 0.3s 
       >>> 多个属性间  ，隔开
    >> transition-timing-function:过渡的时序函数 过渡的方式
       >>>  ease 默认值 慢速开始--先加速---再减速
            linear 匀速运动（不常用）
            ease-in 加速运动
            ease-out 减速运动
            ease-in-out 先加速--再减速
            cubic-bezier() 贝塞尔曲线[https://cubic-bezier.com](https://cubic-bezier.com)
            steps(步数，start/end) 10s 完成过渡 分步数（2步就是5s一次）完成---是在5s开始才过渡 还是在5s结束时过渡
    >> transition-delay 过渡的延迟时间 等待一段时间再执行过渡
    transition: 同时设置没有顺序  但是在写时间时 前面是持续时间 后面的是延迟时间

+ animation 自动触发动态效果 设置动画效果 要先设置一个关键帧
  > annimation-name:帧的名字
    animation-duration:帧的执行时间
    animation-delay:帧的延迟时间
    animation-timing-function:过渡的形式
    animation-iteration-count:动画执行的次数 infinite无限次数 steps  有几个小图片 就写多少步 
    animation-direction:每次动画运行的方向
    >> normal默认值每次都是从from--to
       reverse 没次从to-from
       alternate from-to 去的时候从from-to 回来时从to--from
       alternate-reverse
    animation-play-state:动画的执行状态 动画暂停 继续
    >> running默认值 动画执行
       paused 动画暂停
    animation-fill-mode 动画的填充模式
    >> none 默认值 动画执行完毕 回到元素原来的位置
       forwards 元素停止在动画执行完成的位置
       backwards 动画执行延时等待时 元素就会处于开始位置
       both--forwards+backwards
  transition 
    ``` css 
    @keyframes 帧的名字 { 
    <!-- 动画的开始位置  等价于0%-->
           from{
             margin-left:0;
           } 
    <!-- 动画的结束位置 等价于100%  就写图片的宽度或者高度-->
           to{
             margin-left:100px
           }
    } ```

### 变形

+ 水平x 向上y 屏幕穿出来 z
+ 改变元素的形状或者位置 变形不会影响到页面的布局 
+ transfrom 
  + translate()平移 只折腾自己 元素没有旋转时
    > translateX 沿着x轴平移 
       50% 百分比 是相对于自身位置计算
       垂直水平居中 元素的大小不确定 width不知道 比较灵活 使用absolute需要知道width height固定大小  
     ``` css
          left:50%
          top:50%
          transform:translateX(-50%) translateY(-50%)
    ```
    > translateY沿y轴平移
       translateY + 阴影 实现点击飘出来的动态
     ``` css
         transition:all 3s
         box:hover{
           transform:translateY(-4px)
           box-shadow:0 0 10px rgba(0,0,0,.3)} 
     ```
    > translateZ沿着z轴平移 调整元素与人眼之间的距离 属于立体效果 近大远小 默认情况下 网页不支持透视 必须设置透视
       设置网页的视距 800px 或者1200px
    ```css  
       html{ perspective:800px}
       transform:translateZ(100px)
    ```
  + rotate 使元素沿着x,y,z旋转指定的角度 旋转---->元素自身坐标的位置在旋转
    > rotateX (36deg)
    > rotateY
    > rotateZ
    > backface-visibility：hidden沿着y轴旋转以后 背面是否显示

### 缩放

+ scaleX(2) 沿着x轴放大 .2缩小 实际是坐标轴拉大缩小
+ scaleY()
+ scale()双方向缩放
+ sacleZ()要有显示效果 要设置为3D 类似左右被拉大
  
### 变形的原点 
transform-origin:0 0  左上角 center中心
