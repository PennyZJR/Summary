# NGUI

## 三大基础组件

### **Root : 控制分辨率自适应的基础**

> **分辨率概念**

![image-20241213163338909](./assets/image-20241213163338909.png)

![image-20241213163411347](./assets/image-20241213163411347.png)

> **Root是用来干啥的**

![image-20241213163845722](./assets/image-20241213163845722.png)

> **Root相关参数**

```c#
Scaling Style:缩放模式
	Flexible：灵活模式   一般用于PC端
```

![image-20241213164530286](./assets/image-20241213164530286.png)

```c#
Constrained: 约束模式
    做竖屏游戏只勾选content width
    做横屏游戏只勾选content height
```

![image-20241213165145012](./assets/image-20241213165145012.png)

```c#
Constrained on Mobiles
```

![image-20241213170702086](./assets/image-20241213170702086.png)

> **总结**

![image-20241213170843846](./assets/image-20241213170843846.png)

### Panel：控件显示的基础

> **Panel用来干啥**

1.管理一个UI面板的渲染顺序

2.管理一个UI面板上的所有子控件

> **Panel参数相关**

![image-20241213171424799](./assets/image-20241213171424799.png)

![image-20241213172143285](./assets/image-20241213172143285.png)

> **总结**

![image-20241213172435812](./assets/image-20241213172435812.png)

### Event System(Uicamera):输入事件监听的基本组件

> **EventSystem是用来干啥的**

![image-20241213175722619](./assets/image-20241213175722619.png)

> **参数相关**

![image-20241213174503123](./assets/image-20241213174503123.png)

![image-20241213175411717](./assets/image-20241213175411717.png)

> **总结**

![image-20241213175630770](./assets/image-20241213175630770.png)

## 图集制作

> **图集用来干什么**

![image-20241214142638783](./assets/image-20241214142638783.png)

> **打开图集制作工具**

![image-20241214142926763](./assets/image-20241214142926763.png)

> **新建图集**

![image-20241214144021600](./assets/image-20241214144021600.png)

![image-20241214143546162](./assets/image-20241214143546162.png)

## 三大基础控件

### Sprite精灵图片

> **Sprite用来做什么**

![image-20241214145151535](./assets/image-20241214145151535.png)

> **Sprite参数**

![image-20241214145350675](./assets/image-20241214145350675.png)

sliced:切片模式

![image-20241214150659967](./assets/image-20241214150659967.png)

![image-20241214150745493](./assets/image-20241214150745493.png)

![image-20241214151129113](./assets/image-20241214151129113.png)

> **代码设置图片**

```c#
public UISprite sprite;
//改成同一图集中其他图片
sprite.spriteName="bk";
//改成其他图集中的图片
	//先加载图集
NGUIAtlas atlas=REsource.Load<NGUIAtlas>("Atlas/login");
sprite.atlas=atlas;
	//再设置图片
sprite.spriteName="name";
```

### Label文本控件

> **Label用来干什么**

NGUI中所有文本显示都使用Label来显示

> **创建Label**

直接创建即可

> **Label参数**

![image-20241214152905063](./assets/image-20241214152905063.png)

![image-20241214153349572](./assets/image-20241214153349572.png)

![image-20241214153822832](./assets/image-20241214153822832.png)

> **富文本**

![image-20241214154405124](./assets/image-20241214154405124.png)

> **代码设置Label**

```c#
public UILabel label;

label.text="159753";
```

### Texture大图控件

> **Texture用来干什么**

![image-20241214161853813](./assets/image-20241214161853813.png)

> **参数相关**

![image-20241214162437494](./assets/image-20241214162437494.png)

> **代码设置**

```c#
public Texture tx;
//加载图片
Texture texture=Resources.Load<Texture>("path");
if(texture!=null)
{
    tx.mainTexture=texture;
}
```

## 组合控件

> **所有组件的共同特点**

1.在3个基础组件对象上添加相应组件（脚本）

2.如果希望响应点击等事件，需要添加碰撞器

### Button按钮

> **制作Button**

![image-20241215142008466](./assets/image-20241215142008466.png)

> **参数相关**

![image-20241215142857101](./assets/image-20241215142857101.png)

> **监听事件的两种方式**

OnClick可以关联多个对象的脚本

1.拖脚本：方法必须是public的，先把脚本拖到对象上，再把对象拖到button的OnClick上

2.代码设置：

```c#
public UIButton btn;
//EventDelegate是一个无参无返回值的委托函数
btn.onClick.Add(new EventDelegate(ClickDoSomething));
btn.onClickAdd(new EventDelegate(()=>{print("lambda")}))
public void ClickDoSomething()
{
    print("a");
}
```

### Toggle单选多选框

> **制作Toggle**

![image-20241215151424930](./assets/image-20241215151424930.png)

> **参数相关**

![image-20241215151933279](./assets/image-20241215151933279.png)

> **监听事件的两种方式**

和Button组件一样

### Input文本输入控件

> **制作Input**

![image-20241215162703828](./assets/image-20241215162703828.png)

> **参数相关**

![image-20241215163331559](./assets/image-20241215163331559.png)

![image-20241215163756861](./assets/image-20241215163756861.png)

> **监听事件的两种方式**

和Button一样

### Popuplist下拉列表控件

> **制作PopupList**

![image-20241215173608389](./assets/image-20241215173608389.png)

> **参数相关**

![image-20241215173907120](./assets/image-20241215173907120.png)

![image-20241215174611370](./assets/image-20241215174611370.png)

![image-20241215175025838](./assets/image-20241215175025838.png)

> **监听事件的两种方式**

![image-20241215175748331](./assets/image-20241215175748331.png)

### Silder滑动条控件

> **制作Slider**

![image-20241216203121414](./assets/image-20241216203121414.png)

碰撞器添加到背景上时，点击背景就可以更改进度条，
挂在滑块上时，只能通过滑块来滑动

> **参数相关**

![image-20241216203759390](./assets/image-20241216203759390.png)

> **监听事件的两种方式**

1.拖脚本

2.写代码

```c#
onChange()
onDragFinished()
```



### ScrollBar滚动条和ProgressBar进度条

> **ScrollBar和ProgressBar用来干啥**

![image-20241216211004447](./assets/image-20241216211004447.png)

> **制作ScrollBar**

![image-20241216211250729](./assets/image-20241216211250729.png)

> **制作ProgressBar**

![image-20241216211810586](./assets/image-20241216211810586.png)

### ScrollView滚动视图

> **ScrollView是用来干啥的**

![image-20241216221335446](./assets/image-20241216221335446.png)

> **制作ScrollView**

![image-20241216221437131](./assets/image-20241216221437131.png)

```
ScrollView sv;
sv.UpdateScrollbars();//通过代码控制滚动条更新
```



> **参数相关**

通过panel脚本调整可视范围
![image-20241216221934824](./assets/image-20241216221934824.png)
![image-20241216222605397](./assets/image-20241216222605397.png)

![image-20241216223233372](./assets/image-20241216223233372.png)

> **自动对齐脚本：Grid脚本**

![image-20241216223854187](./assets/image-20241216223854187.png)

![image-20241216224206517](./assets/image-20241216224206517.png)

## Anchor锚点组件

> **Anchor是什么**

![image-20241217212537101](./assets/image-20241217212537101.png)

> **老版本锚点组件**

![image-20241217212741602](./assets/image-20241217212741602.png)

> **新版本-基础控件自带锚点信息**

![image-20241217213649273](./assets/image-20241217213649273.png)

## NGUI进阶

### EventListener和EventTrigger特殊事件监听

> **控件自带事件的局限性**

![image-20241217223651946](./assets/image-20241217223651946.png)

> **NGUI事件 响应函数**

![image-20241217223814359](./assets/image-20241217223814359.png)

```
OnDragOver(GameObject obj)
OnDragOut(GameObject obj)
中的obj均是拖拽的物体
```

**缺点：**给子控件添加功能时需要单独写脚本，面向对象思想减弱

> 更加方便的UIEventListener和UIEventTrigger

![image-20241217230300881](./assets/image-20241217230300881.png)

![image-20241217230727410](./assets/image-20241217230727410.png)

### Drawcall

> **Drawcall的概念**

![image-20241219154645806](./assets/image-20241219154645806.png)

![image-20241219154659421](./assets/image-20241219154659421.png)

> **如何降低DrawCall数量**

- 在UI层面上
  小图合大图->即多个小DrawCall贬义词大DrawCall

> **制作UI时降低DrawCall的技巧**

- 通过NGUI Panel上提供的DrawCall查看工具
- 注意不同图集之间的层级关系
  同一图集拼面板时层级区间不要出现其他图集的图片，会增加DrawCall数量
- 注意Label的层级关系

### NGUI字体

> **NGUI字体的作用**

1.降低DrawCall

2.自定义美术字体

> **制作NGUI字体**

![image-20241219160812819](./assets/image-20241219160812819.png)

> **Unity动态字体和NGUI字体如何选择**

- 文字变化较多的用Unity动态字体，变化较少用NGUI字体
- 想要减少DRawCall用NGUI字体
- 美术字体用NGUI字体

### NGUI缓动

> **NGUI缓动是什么**

![image-20241219172228360](./assets/image-20241219172228360.png)

> **使用NGUI缓动**

![image-20241219172309523](./assets/image-20241219172309523.png)

> **Tween Scale参数相关**

![image-20241219172455582](./assets/image-20241219172455582.png)

> **Play Tween组件**

![image-20241219174205395](./assets/image-20241219174205395.png)

![image-20241219174503556](./assets/image-20241219174503556.png)

### 模型和粒子显示在UI之前

> **NGUI中显示3D模型**

![image-20241219175944147](./assets/image-20241219175944147.png)

2.主摄像机不要渲染UI层
4.3D模型不受depth影响，只受z轴影响

> **NGUI中显示粒子特效**

![image-20241219181009771](./assets/image-20241219181009771.png)

### 其他

> **NGUI事件响应播放音效**

PlaySound脚本

> **NGUI控件和键盘按键绑定**

KeyBinding脚本

> **PC端 tab键快速切换选中**

KeyNavigation脚本

> **语言本地化**

![image-20241219205532568](./assets/image-20241219205532568.png)

![image-20241219205924460](./assets/image-20241219205924460.png)

```cpp
Localization.language="简体中文";//修改语言
```

