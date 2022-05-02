# Donut

## 第一课：基础知识

渲染：
顶部菜单栏 Render - Render image
快捷键F12

移动：
左侧菜单栏 Move
快捷键
G(G开始自由移动，鼠标左键停止移动)
按下G之后，再按XYZ可以沿固定坐标轴移动
按下G之后，再按鼠标中键可以吸附到某条坐标轴上

旋转：
左侧边栏 Rotate
快捷键
R(R开始自由旋转，鼠标左键停止旋转)
按下R之后，再按XYZ可以沿固定坐标轴旋转
按下R之后，再按鼠标中键可以吸附到某条坐标轴上

缩放：
左侧边栏 Scale
快捷键
S(S开始自由缩放，鼠标左键停止缩放)
按下S之后，再按XYZ可以沿固定坐标轴缩放
按下S之后，再按鼠标中键可以吸附到某条坐标轴上

取消上述操作：ESC 或 鼠标右键

旋转视角：鼠标中键
平移视角：Shift+鼠标中键
相邻轴视角：alt+鼠标中键
缩放视角：滚动鼠标中键（精细缩放：Ctrl+拖动鼠标中键）
视角菜单：~
只看选中对象：/
视角重置：Shift+C

## 第二课：圆环+粗调形状

删除对象：Del 或 x
新建对象：Shift+A
对象位置大小属性：N

**新建对象后左下角的参数**
Major Segment：主片段数（纵向）
Minor Segment：次片段数（横向）
Major Radios：主半径（大小）
Minor Radios:次半径（粗细）

（如果不小心关掉面板，F9重新打开）

片段数不是越高越好，电脑会很卡而且不便于后期处理
粗糙程度让每个方格刚好能保持正方形就足够了

创建好对象后，将对象缩放到预期大小：
背景中每个方格的长度是1m
选中对象，按N打开属性面板，按S缩放到目标长宽高
**按Ctrl+A选择Scale应用，将Scale重新回归1**

将对象变圆滑：
右键 - Smooth
右侧属性栏 - Modifier Properties - add Modifier - Subdivision Surface

编辑模式：Tab
在编辑模式下，选中要编辑的顶点（vertices），按下G开始拖拽调整
*上述形状编辑适合面数少的形状，面数过的更常用比例编辑：*
顶部第二行菜单 - Proportional Editing
快捷键：o
选中要编辑的单个顶点（Vertex），按下G
默认情况下笔刷非常大，记得用滚轮上搓来调小
小技巧：法向缩放，不要按G而是按alt+s

## 第三课：糖霜模型

思路：复制甜甜圈，切出我们需要的，再调调参数

将视角切到一条水平轴上（x或y，不要开右侧的perspective，会变形）
打开右上角的Toggle X-Ray（快捷键alt+z），这样就可以选中被遮挡的顶点
选中上半部分，复制（Shift+D），然后esc或鼠标右键取消移动
按P - Selection就可以把选中的部分分离成独立的对象了
如果节点不小心没选中了，可以选中其中一个按Ctrl+L来选中关联的所有节点

给甜甜圈和糖霜重命名，方便后续识别对象

给糖霜增加体积：
右侧属性栏 - Modifier Properties - add Modifier - Solidify
进入线框模式（右上角点击 或 Z - Wireframe），可以看清糖霜的实际厚度和位置（此时是向内延展的，需要调整）
将右侧Solidify属性中offset调整为1，将Thickness调整为0.002m

由于Modifier的作用是从上到下，所以糖霜看起来像个帽子盖在上面
把Solidify拖拽到Subdivision Surface上面（先固化再提高分辨率），让糖霜看起来更贴合

## 第四课：糖霜液滴 和 环形收缩

如果糖霜的节点不够，液滴会很尖锐，可以在编辑模式中选中所有节点（快捷键A），右击，选择Subdevide

下面开始制造液滴效果
现在进入编辑模式会发现节点显示不完整了，原因是被固化效果遮盖了，在右侧Solidify属性中取消选择“Display modifier in Edit mode”，这样就能看清所有节点了
现在直接点击节点按G进行拖拽会穿模，所以先在顶部第二行菜单选中吸铁石（Snap），并将旁边的选项改为表面（Face），并勾选上“Project individual Element”，这样拖拽就会吸附在表面而不会穿模了
拖拽记得打开Proportional Editing
如果还是穿模试试将糖霜厚度调大（0.0025m是没问题的）

创建新窗口：
鼠标移动到右侧菜单栏分界线（变成左右箭头时）右击，选择Vertical Split
或者鼠标移动到窗口右上角（option的右上方一点，鼠标变为十字），向左拖拽是新建，向右拖拽是消除
新窗口可以用来放参考图

首先把Subdivision Surface拖拽到Solidify上面，属性中点击下箭头选择apply（因为apply会从上向下作用，避免覆盖solidify），这层应用只作用于糖霜，相当于把糖霜的分辨率提高了，但环没变
开始局部拖拽前，可以通过点击穿模的节点，打开Proportional Editing，按下G和Ctrl直接确认，来修复部分穿模
接下来开始制作液滴
选中边缘相邻的几个点，按E开始挤出（extrude）液滴

接下来进行环形雕刻，首先应用Subdivision Surface
然后选择外环一圈的节点（快捷键alt+鼠标左键），进行法向调整alt+s，让中间一圈凹陷一点
这时候会发现糖霜没有和环贴合了，右侧属性栏 - Modifier Properties - add Modifier - Shrinkwrap
用属性中target的吸管点击环，这样就重新吸附上去了（但是又穿模啦，是因为优先级不对，将Shrinkwrap优先级调到最高就可以恢复了）

## 第五课：雕刻（sculpting）

对糖霜应用所有的Modifier，因为我们进入雕刻模式这些修改将会失效
顶部菜单 - Sculpting
快捷键Ctrl+Tab，并用鼠标选择

常用快捷键
拖拽G
笔刷大小F
笔刷力度Shift+F
抹平笔刷Shift+S（按住Shift可以临时开启）默认强度是0.7，建议先调到0.2
膨胀笔刷I（inflate）

## 第六课：渲染

新建平面，
将ice和Donut绑定：先点ice，再点Donut，按Ctrl+P，选择Object（Keep Transform）

调整相机和灯光的位置
快速移动到原点：alt+G

选中light，点击右侧Object Data Properties，在右侧属性栏，将灯光亮度降低到20w

渲染引擎：右侧Rander Properties可以修改渲染引擎，默认是Eevee，只是一款实时渲染引擎，适合用于游戏，对阴影的渲染会比较粗糙
非实时渲染的有Cycles，会更精细

添加材质：
选中糖霜，右侧菜单选择Material Properties - New
调节Color和Roughness

调节Subsurface（边缘到不透光的部分的距离）

## 第七课：噪点纹理

顶部菜单 - Shading
添加Texture - Noise Texture，
添加Converter - ColorRamp，
添加Input - Texture Coordinate
添加Vector - Bump

## 第八课：绘制纹理texture paint

添加Texture - Image Texture，选择分辨率、颜色，取消勾选alpha，确认
移除ColorRamp
顶部菜单栏 - Texture paint
切换前景色/背景色：x

切到Shading
添加Color - MixRGB

## 第九课：制作sprinkle

**老方法**
创建一个球（面数尽可能少，后面会大量复制），调整好大小
选中上班部分按E拉伸，形成一个柱体
接下来将上下半球稍微压扁，用s缩放来实现（注意不要勾选Proportional Editing，否则整个柱子都会变短）

选中ice对象，右侧菜单栏 - Particle Properties
加号，Hair，Render - Object，Instance Object - 吸管点击制作的sprinkle

勾选Advanced - 勾选Rotation，Orientation Axis - Normal

Ctrl+Tab 选择Weight paint，画上想要让sprinkle展示的区域，切回正常视图
右侧属性中 - Vertex Groups - Density - Group

**新方法**
开个新窗口，在窗口左上角将视图改为“Texture Node Editor”
或者
顶部菜单栏右边的加号 - General - Geometry Nodes（新版本已经开过了直接点就行）

下窗口 - New
此时在右侧的Modifier Properties中会多出一项“GeometryNodes”，如果此时点中别的Modifier，下方窗口内容会消失
为了方便可以用之前New旁边的pin固定住

添加Point - Distribute Points on Faces
添加Geometry - Join Geometry

制作sprinkle

添加Instances - Instance on Points
把Sprinkle从对象中拖到Geometry窗口中，会自动创建一个Object Info

将Sprinkle旋转躺平，连接上Rotate节点

添加Utilities - Rotate Euler，并选中Local
添加Utilities - Random Value，并选择Vector，将x轴和y轴的最大值调为0，在z轴最大值输入pi或者tau

接下来就是weight paint，不再赘述

## 第十课：变换sprinkle各种样式

Loop Cut：Ctrl+R，鼠标滚轮跳切片数，鼠标左键确认

选中创建好的不同样式Sprinkle，按M组成Collection

拖进Geometry窗口替换原来的节点，勾选Pick Instance、Separate Children和Reset Children

给一个Sprinkle添加材质，并将其余的关联上去（最后选中有材质的，然后Ctrl+L，Link Material）

进入Shading

添加Input - Object Info
添加Converter - ColorRamp，将Linear改为Constant

造一个球，上色，随意点缀一下

## 第十一课：Donut旋转动画

删除Plane

在layout页面摆好相机，按i插入关键帧
Ctrl+t可以按秒显示时间轴

在Animation mode中打开Graph editor

## 第十一课：雪花动画

在Donut后面新建一个平面，在Geometry中解除pin之后，在平面上创建一个Distribute Points on Faces
添加Geometry - Set Position
添加Utilities - Random Value，将Float改为Vector
复制Set Position节点

第一种方法：关键帧
鼠标放置在z坐标数值上，按i设置关键帧，Shift+ → 跳到末尾帧，Shift+ ← 跳到开头帧

第二种方法：Math
添加Input - Value，输入“#frame”（如果方框已经变成紫色，则只用输入frame）
添加Vector - Combine XYZ，只绑定z轴，让雪花不再沿xy移动
添加Utilities - Math，为了让雪向下落，值设为负的

对节点创建关键帧：Ctrl+J，按N编辑

想让雪花往左下或右下，则关联上x或y轴，看情况添加上Math，使用Multiply 负一
添加Utilities - Random Value

添加 Instance on Points
添加Utilities - Random Value
添加Utilities - Rotate Euler，从Euler切换到Axis Angle

## 第十二课：打光

添加一个光源，让阴影不要太暗
在World Properties中关掉世界光

## 第十三课：Compositing

勾选Use Nodes
新建窗口，切换到Image Editor，选择Viewer Node

把背景换颜色
右侧菜单栏 - Render Properties - Film - Transparent
添加Input - RGB
添加Color - Alpha Over
添加Matte - Ellipse Mask
Ctrl+Shift+鼠标左键：单独看某个节点
添加 - Filter - Blur，选择Fast Gaussian，勾选Relative
添加Color - Mix
复制Blur节点
右侧菜单栏 - View Layer Properties（记得把渲染模式切到Cycles）
复制Mix节点

接下来调色
新增Color Balance，规则调整为Offset/Power/Slop
添加Distort - Lens Distortion

## 第十四课
