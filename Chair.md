# Chair

## 第一课

Shift+A选择image - Reference
找到上视图，导入，按N将角度重置
点击x轴视角，添加侧视图，将侧视图像旁边移动一点，向上也移动一点
正视图同理
在右侧菜单栏Object Data Properties 中将参考图的不透明度降低一点

新建一个cube，开始做椅子腿
切到wireframe方便看参考图
移动到椅子脚的位置，缩放使其宽度和椅子脚差不多
然后进入x-ray mode，拖拽cube的上面至与椅腿同高，注意倾斜角度
调整右上的边，使之与另一条边重合

在转角处添加loop cut（CTRL+R），如果位置选错了，按两次G，能重新调整cut的位置
选中转角的4个顶点，按E（Extrude），拉到有凹陷的位置停止（凹陷之后做）

切到正视图，调整椅子腿的左右位置，缩放一下

切到侧视图，添加Subdivision Modifier
添加loop cut，将cut移动到转折处(横向纵向都有)
然后将转角处多出来的面合并（编辑模式下按A选中整个物体，按M，选择distance）
或者使用右上角的auto merge

增加mirror modifier，并删除一半的顶点
然后删除顶部的面，使顶部变平
