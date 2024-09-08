# 本人读研期间编写的用于科研绘图的工具以及其他辅助工具

## 项目简介
所有代码均包含在[utils](/utils)文件夹中，所需的都是一些常用依赖包。[demo](/demo.ipynb)是我编写的简单的使用介绍，目前还在完善中。

## demo
### 矩阵可视化
需要用到函数 **mat2color**, 使用方法如下:

```Python
        from utils.misc import mat2color
        import numpy as np

        mat = np.arange(100).reshape(10,10)
        mat2color(
            mat=mat, #要可视化的二维矩阵
            colormap='rainbow', #颜色空间名称
            figure_size=4, #画布基本尺寸
            save_path='demo/00.png', #保存路径
            title=None, #标题
            norm='linear', #颜色条映射函数
            cbar_auto_log_tick=False, #以log间距显示颜色条坐标
            vmin=0, #颜色映射的最小值, 使用log norm时应大于0
            vmax=100, #颜色映射的最大值
            axis_visible=True, #是否显示主图的坐标轴
            has_colorbar=True, #是否显示颜色条
            cbar_width=0.03, #颜色条占画布的百分比
            cbar_ticks_rotation=None,#颜色条坐标旋转角度
            ax_fontsize=None,#主图坐标刻度字体大小，默认为None，使用自动大小
            cbar_fontsize=None,#颜色条标刻度字体大小，默认为None，使用自动大小
            show_in_jupyter=True,#是否在jupyter显示结果
            transparent=True,#图片是否透明
)
注意:上面并没有展示这个函数的所有参数，剩余的参数的解释正在完善中。
```
这个函数的运行结果如下:

![矩阵可视化](./demo/00.png "mat2color")

### 展示图片集
假设你有很多张图片，并且它们的分辨率相同，你想以n行m列的形式来展示，那么使用函数**imgsGridsPlot**就可以很方便做到:
```Python
        import cv2.cv2
        from utils.misc import imgsGridsPlot
        from utils.file import find_file
        import cv2

        img_folder = 'demo/coco'
        files = find_file(img_folder,
                        suffix='.jpg',#后缀名
                        mode='abs'#获取绝对地址
                        )

        img_list=[]
        for i, file in enumerate(files):
            img = cv2.imread(file, cv2.IMREAD_UNCHANGED)
            img = cv2.cvtColor(img,cv2.COLOR_BGR2RGB)
            img_resize = cv2.resize(img,dsize=(256,256),interpolation=cv2.INTER_NEAREST)
            img_list.append(img_resize)

        imgsGridsPlot(imgs_list=img_list, #图片列表，格式为[np.ndarray...]
                    nRows=10, #设置以多少行显示, 列数会自动计算
                    axis_visible=False, #和上述函数相同
                    save_path='demo/01.png', #和上述函数相同
                    transparent=True, #和上述函数相同
                    show_in_jupyter=True, #和上述函数相同
                    dpi=150 #保存图片的dpi
            )

上述代码先从文件夹'demo/coco'下获取到所有图片的路径，然后根据路径读取所有图片，最后以10行的方式显示它们。   
其中还用到了 find_file 函数，他能获取指定路径下的相同扩展名文件的文件名，包括子文件夹下的文件，文件名可以是绝对地址也可以仅是文件名。
```
这个函数的运行结果如下:

![图片集展示](./demo/01.png "图片集展示")

### 其他函数，持续更新中......


# 最近更新 2024.09.09
