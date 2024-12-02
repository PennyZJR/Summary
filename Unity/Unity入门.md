# Unity入门

## 场景切换

### SceneManager.LoadScene(string name)

### Application.LoadLevel(string name):已弃用，会报警告

### 前提是把场景资源加到场景列表里面

## 退出游戏

### Application.Quit():在编辑模式下无效

## 隐藏和锁定鼠标

### 隐藏鼠标

- Cursor.visible=false;

### 锁定鼠标

- Cursor.lockState=CrsorLockMode.

	- None:不锁定

	- Locked:锁定，鼠标会被限制在屏幕的中心点，而且会被隐藏，可以通过esc键摆脱编辑模式下的锁定

	- Confined：限制在窗口范围内

### 设置鼠标图片

- Cursor.SetCursor()

	- Texture2D:导入图片在inspector窗口改为cursor类型

	- Vector2：偏移位置，相对于左上角

	- CursorMode：平台支持的光标模式

## 随机数

### Random类：与c#中的Random类不一样

- Random.Range(min,max)

	- int重载左闭右开

	- float重载左闭右闭

### System.Random：使用c#的随机数

## 委托

### C#的自带委托

- System.Action：无参无返回值

- System.Action<>:有参无返回值

- System.Func<T>:无参返回T

- System.Func<T,U>:参数为T,返回值为U

### Unity自带委托

- UnityAction：无参无返回值

- UnityAction<T>：有参无返回值

## 模型

### 模型格式：推荐fbx格式

### 构成

- 骨

	- 骨骼：非必需，有动作的模型需要

- 肉

	- 网格面片：必需，决定了模型的轮廓

- 皮

	- 贴图：必需，决定了模型的颜色效果

### 重点规则

- 模型面朝向朝模型坐标系的Z轴

- 缩放大小单位要注意

## SceneManager

### 得到当前所在场景的名字:GetActiveScene().name

## unity脚本基础

### 工程文件夹📂

- Assets:工程资源文件夹（美术资源，脚本等）

- Library:库文件夹（Unity自动生成管理）

- Logs：日志文件夹，记录特殊信息（Unity自动生成管理）

- obj：编译产生中间文件（Unity自动生成管理）

- Packages:包配置信息（Unity）自动生成管理

- ProjectSettings：工程设置信息（Unity自动生成管理）

### MonoBehavior

- 只有继承此类才能挂载到GameObject上

- 继承了MonoBehavior不能new只能挂

- 重要成员

	- 1.获取依附的GameObject

	- 2.获取依附的GameObject的Transform

	- 3.获取脚本是否激活

		- this.enabled=bool

- 重要方法

	- 1.得到依附对象上挂载的其他脚本：this.GetComponent<>()

	- 2.得到自己挂载的多个脚本：this.GEtComponents<>()

	- 3.得到子对象挂载的脚本(默认也会找自己身上是否挂载该脚本)：this.GetComponentInChildren<>(bool)默认为false，意思就是如果子对象失活，是不会在这个子对象上去找脚本的
this.GetComponentsInChildren<>(bool)

	- 4.得到父对象挂载的脚本(默认也会找自己身上是否挂载该脚本)：this.GetComponentInParent<>()
this.GetcomponentsInParent<>()

	- 5.尝试获取脚本：
this.TryGetComponent<>(out varName)

### 生命周期函数

- fps：frames per second

-  

- LateUpdate:一般用来处理摄像机位置更新相关的

### 引擎窗口

- Hierarchy:层级窗口

- Scene：场景窗口

	-  

- Game:游戏窗口

- Project：工程资源窗口

- Inspector：检查窗口

- Console：控制台窗口

### 特性

- 在Inspector窗口中隐藏:[HideInInspector]

- 让私有的和保护的也可以被显示：[SerializeField](强制序列化字段)

- 公共的不让显示：[HideInInspector]

- 字典怎么都不能被显示
自定义类被显示：[System.Serializable]

- 为成员分组:[Head(" ")]

- 悬停注释：[Tooltip(" ")]

- 间隔特性:[Space]

- 修饰数值的滑条范围：[Range( , )]

- 多行显示字符串，默认不写参数显示三行:[MultiLine( )]

- 滚动条显示字符串：[TextArea(min,max)]

- 为变量添加快捷方法：[ContextMenuItem("显示按钮名","方法名")]

- 为方法添加特性，能够在Inspector中执行：[ContextMenu(" ")]

## unity重要组件和API

### GameObject

- 成员变量

	- 名字：this.gameobject.name

	- 是否激活：this.gameobject.activeSelf

	- 是否是静态：this.gameobject.isStatic

	- 层级：this.gameobject.layer

	- 标签:this.gameobject.tag

	- 位置信息：this.gameobject.transform

- 静态方法

	- 创建自带几何体：.CreatePrimitive(PrimitiveType.type)

	- 查找对象

		- 查找单个对象

			- 通过对象名查找：.Find(" ")
效率低，在场景上所有的对象查找

			- 通过tag查找：.FindWithTag(" ")
|| .FindGameObjectWithTag(" ")

			- object.FindObjectOfTye<>():效率更低，可以找到场景中挂载的某一个脚本对象

		- 查找多个对象：只能通过tag

			- .FindGameObjectsWithTag(" "):只能找到激活对象

	- 实例化（克隆）对象

		- GameObject.Instantiate(obj)

	- 删除对象

		- GameObject.Destroy(obj,delayedTime)
一般情况下，会在下一帧时把这个对象移除并从内存中移除

		- GameObject.DestroyImmediate(obj):尽量不用，降低卡顿几率

	- 删除脚本

		- GameObject.Destroy(this)

	- 过场景不移除

		- GameObject.DontDestroyOnLoad(obj)

- 成员方法

	- 创建空物体

		- GameObject obj=new GameObject(name,typeof(脚本名));

	- 为对象添加脚本

		- 如果想要动态的添加继承了MonoBehavior的脚本在某一个对象上：
obj.AddComponent<>();
通过返回值可以得到脚本信息

	- 得到脚本

		- 和继承MonoBehavior的一样 

	- 标签比较

		- obj.CompareTag("")

	- 设置激活失活

		- obj.SetActive(bool)

	-  

### Time

- 时间缩放比例

	- 时间静止：Time.timeScale=0f;
Time.timeScale=1f;
2倍速：Time.timeScale=2f;

- 帧间隔时间：最近的一帧用了多长时间（秒），

	- 受scale影响：Time.deltaTime

	- 不受scale影响：Time.unscaledDeltaTime

- 游戏开始到现在的时间

	- 受scale影响：Time.time

	- 不受scale影响：Time.unscaledTime

- 物理帧间隔时间:FixedUpdate

	- 受scale影响：Time.fixedDeltaTime

	- 不受scale影响：Time.FixedUnscaledDeltaTime

- 帧数:从游戏开始到现在游戏跑了多少帧（多少次循环）

	- Time.frameCount

### Transform

- 位移：this.transform.Translate()

- 旋转：this.transform.Rotate()

	-  

	- 相对某一个点转

		- this.transform.RotateAround()

			-  

- 角度

	- 相对世界坐标系角度：
this.transform.eulerAngles

	- 相对父对象角度：
this.transform.localEulerAngles

	- 不能单独设置x,y,z,要一起设置

- 缩放

	- this.transform.lossyScale

	- this.transform.localScale

	-  

- 看向

	- 让一个对象的面朝向一直看向某一个点或某一个对象

	- this.trnsform.LookAt()

	-  

- 父子关系

	- 获取和设置父对象

		- this.transform.parent

		- this.transform.setParent

		-  

	- 抛妻弃子

		- this.transform.DetachChild()

	- 获取子对象

		- this.transform.Find("name "):
能找到失活对象

		- this.transform.childCount:
能找到失活对象，找不到孙子

		- this.transform.GetChild(index)

	- 儿子的操作

		- 判断自己的爸爸是谁:this.transform.IsChildOf()

		- 得到自己作为儿子的编号：
this.transform.GetSiblingIndex()

		- 把自己设置成第一个儿子：
this.transform.SetASFirstSibling()

		- 把自己设置成最后一个儿子：
this.transfom.SetAsLastSibling()

		- 指定位置：
this.transform.setSiblingIndex(Index)

		-  

- 坐标转换

	- 世界坐标转本地坐标

		-  

	- 本地坐标转世界坐标

		-  

### Input

- 输入相关内容肯定是写在update函数里面

- 鼠标在屏幕位置

	- Input.mousePosition

	- 屏幕坐标原点在左下角

- 检测鼠标输入

	- 鼠标按下一瞬间进入

		- Input.GetMouseButtonDown():
0左键，1右键，2中键

	- 鼠标抬起一瞬间进入

		- Input.GetMouseButtonUp()

	- 鼠标长按按下抬起都会进入

		- Input.GetMouseButton()

	- 中键滚动

		- Input.mouseScrollDelta

			- 返回Vector2，y值改变

				- -1往下，0没有，1往上

- 检测键盘输入

	- 按下

		- Input.GetKeyDown(KeyCode枚举)：
传入字符串的重载：只能传小写字符

	- 抬起

		- Input.GetKeyUp()

	- 长按

		- Input.GetKey()

- 检测默认轴输入

	- Input.GetAxis(string name)

		- 检测键盘

			- Vertical:w,s

			- Horizontal:a,d

		- 检测鼠标

			- Mouse X

			- Mouse Y

		- 返回值(float):[-1,1]

	- Input.GetAxisRaw()

		- 返回值:-1,0,1三个值

- 是否有任意键或鼠标长按

	- Input.anyKey

- 是否有任意键或鼠标按下

	- Input.anyKeyDown

- 这一帧的键盘输入

	- Input.inputString

- 手柄输入

	- 得到连接的手柄的所有按键名字：
string []strs=Input.GetJoystickNames()

	- 某一个按钮

		-  

- 移动设备触摸相关

	-  

	-  

### Screen

- 静态方法

	- 设置分辨率

		-  

- 静态属性

	- 屏幕的宽高(游戏窗口）

		- Screen.width

		- Screen.height

	- 当前屏幕分辨率（显示屏）

		- Screen.CurrentResolution：
.width    .height

	- 屏幕休眠模式

		- Screem.sleepTimeout=SleepTime.(类中常量)

	- 不常用

		-  

		-  

		-  

### Vector3

- Vector.Distance():计算两个三维向量之间的距离

- 位置

	- 相对世界坐标系：
this.gameobject.transform.position

	- 相对父对象：
this.transform.localPosition

	- 位置的赋值只能整体改，不能单独改x,y,z:
Vector3 pos=this.tranform.position;
pos.x=a0;
this.tranform.position=pos;
可通过这种方法单独更改

	- 对象当前的朝向

		- this.transform.forward
```````up,right

- 位移

	- this.transform.Translate():
默认相对于自己坐标系动

### Camera

-  

- 重要静态成员

	- 获取摄像机

		- Camera.main:
前提是tag为MainCamera

		- 获取摄像机数量：
Camera.allCamreasCount

		- 得到所有摄像机：
Camrea.allCameras

	- 渲染相关委托

		-  

- 重要成员

	- 界面上的参数都可以在Camera中获取

	- 世界坐标<=>屏幕坐标

		-  

		-  

## 核心系统

### 光源系统基础

- 光源组件

	- 面板参数

		-  

		- 游戏窗口看到耀斑要添加耀斑脚本

	- 代码控制

		- Light

- 光相关面板

	-  

	-  

### 物理系统

- 碰撞检测

	- 刚体

		- 碰撞产生的必要条件：
两个物体都有碰撞器，至少一个有刚体

		-  

		-  

		-  

	- 碰撞器

		- 3D碰撞器种类

			-  

		- 共同参数

			-  

		- 常用碰撞器

			-  

		- 异形物体使用多种碰撞器组合

			- 刚体对象的子对象碰撞器信息参与碰撞检测

		- 不常用碰撞器

			- 网格碰撞器：Mesh Collider

				-  

			- 环状碰撞器：Wheel Collider

				-  

				-  

			- 地形碰撞器：Terrain Colloder

	- 物理材质

		- 创建物理材质

		- 物理材质参数相关

			-  

	- 碰撞检测函数

		- 碰撞和触发响应函数属于特殊的生命周期函数，也是通过反射调用

			-  

		- 物理碰撞检测响应函数

			- OnCollisionEnter(Collision collision)

				-  

			- OnCollisionExit(Collision collision)

			- OnCollisionStay(Collision collision)

		- 触发器检测响应函数

			- OnTriggerEnter(Collider other)

			- OnTriggerExit(Collider other)

			- OnTriggerStay(ColLider other)

		-  

		-  

		-  

	- 刚体加力

		- 刚体自带添加力的方法

			-  

			-  

		- 力的几种模式

			-  

			-  

			-  

		- 力场脚本

			- Constant Force

		- 刚体的休眠

			-  

### 音效系统

- AudioSource(音频源脚本)

	- 音量大小:varName.volume

	- 静音：varName.mute

	- 开始播放：varName.Play()

- 音频文件导入

	- 常用格式

		-  

	-  

	-  

- 音频源和音频源监听脚本

	- 音频源脚本

		-  

		-  

	- 音频监听脚本

		- audio listener

- 代码控制音频源

	- 得到脚本：
AudioSource a=this.GetComponent<AudioSource>()

	- 控制播放停止

		- a.play()
a.stop()
a.pause()
a.unpause()
a.playDelayed(second)

	- 如何检测音乐播放完毕

		-  

	- 如何动态控制音效播放

		-  

- 麦克风输入相关

	- 获取设备麦克风信息

		-  

	- 开始结束录制

		-  

	- 获取音频数据用于传输和存储

		-  

## 1.用varName表示变量名
2.不加变量名的为静态函数

