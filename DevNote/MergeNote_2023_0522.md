# Merge Note 2023.05.22

本次合并Xuan和Yao的Editor以及Player项目。由于github自动合并失败，由Yao完成手动合并

## Editor项目合并

### 简述

Xuan和Yao版本各自基于 ***Yao:DevNote_2023_0312.md*** 版本修改

#### Xuan版本

Xuan版本在旧版基础上增加两个组件：
1. 进度条组件
2. Anchor选中指示器

具体需求见文档： ***Xuan : DevReq_2023_0423.md***
组件调用见文档： ***Xuan : DevNote_2023_050607.md***

该版本在此需求基础上还完成了：
1. 项目中进度条的集成:在资源导入时，呼出进度条，通知用户导入进度
2. Anchor指示器的集成：进入锚点编辑模式时，被选中锚点会亮起绿色边框
    1. 尚待解决：文字类锚点的指示边框显示效果尚不理想

具体见文档：***Xuan***

#### Yao版本

Yao版本在旧版基础上增加部分双目渲染功能：
见需求文档 ***Yao : DevNote_2023_0519.md***
具体修改内容见下文 “合并情况描述”


### 合并情况描述

本次合并基于Xuan版本，集成Yao版本代码。所修改的内容如下

#### Prefab中

1. 对 Anchor 预制体的修改
    1. 去掉原本的Collider，改成BoxCollider

2. 对 Inspector.SceneEditCell 预制体的修改
    1. 在View下增加名称为**3D_Toggle**的Toggle组件
    2. 在View下增加名称为**Format_Dropdown**的Dropdown组件

#### Script中

1. 修改 PanoView 实体类：
    1. 增加 *is3D* 的bool字段
    2. 增加 *format3D* 的int字段
    3. 增加 *copyFrom(PanoView)* 方法
    4. 增加用于给 *format3D* 赋值的常量三个：
        1. FORMAT_360
        2. FORMAT_360_LR
        3. FORMAT_360_UD
    5. 修改 saveAsEntity 方法：
        ```{.java}
        //修改前
        public void saveAsEntity(int type, string name, string postFix)
        //修改后
        public void saveAsEntity(int type, string name, string postFix, bool is3D, int format3D)
        ```
2. PanoResourceLoader 类
    1. 修改**registerPanoViews**方法：由于修改了PanoView实体，此处进行相应修改。**共两处**，修改后代码如下：
        ```{.java}
        // 默认为2D 360°全景资源
        view.saveAsEntity(
            PanoView.VIEWTYPE_IMAGE,
            Path.GetFileNameWithoutExtension(imagePath),
            Path.GetExtension(imagePath),
            false,
            PanoView.FORMAT_360);
        viewList.Add(view);
        ```
3. DefaultPath 类：
    1. 修改 getResourceLoaderPath(PanoView) 方法:
        1. 修改后名为：getPanoViewPath（PanoView）
    2. 增加 getPanoViewVicePath(PanoView) 方法

4. View.Inspector.SceneEditorScript 类
    1. 增加方法：setPanoViewAs3D()
    2. 修改方法： setupEditor(SceneScript)
        1. 增加代码块以设置Toggle，如下：
            ```{.java}
            // set 3D toggle
            Toggle dToggle = transform.Find("View").Find("3D_Toggle").GetComponent<Toggle>();
            dToggle.onValueChanged.AddListener(delegate {
                setPanoViewAs3D(dToggle.isOn);
            });
            dToggle.isOn = scene.getPanoView().is3D;
            ```