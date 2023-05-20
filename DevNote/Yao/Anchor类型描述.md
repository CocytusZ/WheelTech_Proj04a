# Anchor 类型描述
Anchor的类型由Type和Resource两个属性描述


## Anchor Resource 描述
各类型Anchor资源读写不同，通过type和rscUri两个字段存储信息，其格式如下：
    1. SWITCH类型：
        1. type = AnchorType.SWITCH
        2. rscUri：存储的是需要跳转的sceneId.toString()，通过Int32.Parse方法转换回int格式
    2. DISPLAY类型
        1. type = AnchorType.DISPLAY
        2. rscUri：存储的是PanoView的toJson()方法，通过静态方法PanoView.FromJson转换回Panoview
    3. TEXT类型
        1. type = AnchorType.TEXT
        2. rscUri:存储的是string形式的文本。rscWidth存文本框大小，rscHeight存字体的大小