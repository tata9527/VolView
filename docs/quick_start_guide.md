# 快速入门指南

VolView的欢迎屏幕注释如下图所示。有关欢迎屏幕组件的更多信息，请参阅["欢迎屏幕"](welcome_screen.html)文档。

![Welcome](./assets/01-volview-welcome-notes.jpg)

从欢迎屏幕开始，需要四个简单的构造来从DICOM数据生成令人惊叹和深刻的可视化。
1. 加载数据
2. Radiological controls 放射医学控制
3. 渲染控制
4. 保存/加载状态

## 1. 加载数据

VolView接受多种格式的DICOM数据:
* 文件夹:其中一个文件夹包含多个DICOM对象(文件)
* 文件选择:选择多个DICOM文件
* 压缩集合:包含一个文件夹或DICOM文件的选择

从Data选项卡(VolView启动时的默认选项卡)中，您可以拖放上述任何格式的DICOM数据，或者您可以单击打开文件浏览器并选择DICOM数据。您还可以选择列出的一个示例DICOM集合，它将从[https://data.kitware.com](https://data.kitware.com/#collection/586fef9f8d777f05f44a5c86/folder/634713cf11dab81428208e1e)下载到您的机器上。

[***观看视频!***](https://youtu.be/4PvZd7yTzf0)

VolView还可以加载许多其他图像数据格式。要了解更多信息，请参阅["Loading Data"](loading_data.html)的文档。

**注:** 当新数据已加载或切换选项卡时，在VolView显示新数据/选项卡之前可能会延迟长达10秒。在此期间请耐心等待。我们为这次延迟道歉，它将在VolView的未来版本中被消除。

## 2. Radiological controls 放射医学控制

三项主要的放射医学控制措施如下:

* 布局:这个工具栏按钮如下图所示。使用它可以在四个有用的窗口排列之间进行选择。在所有的事情，如果你有一个特定的布局，你想看到添加，请提出功能请求在我们的[问题跟踪器](https://github.com/Kitware/VolView/issues)。
  
  ![Layout](./assets/07-volview-layout-notes.jpg)
  

* 2D鼠标左键:窗口/水平、平移、缩放或准线:选择这些选项可以控制鼠标左键在2D窗口中的作用。
  ![Window-Level, Pan, Zoom, Crosshairs](./assets/10-volview-wl-pan-zoom-notes.jpg)

* 2D标注:绘制和标尺:当选择标尺工具时，使用鼠标左键放置和调整标尺末端标记。右键单击结束标记将显示一个弹出菜单，用于删除该标尺。切换到 `标注` 选项卡，查看当前加载数据的注释列表。选择所列标尺旁边的位置图标以跳转到其切片。选择要删除该标尺的垃圾桶。当选择绘画工具时，您可以在任何2D窗口中绘画。第二次点击绘画工具，调出颜色菜单，调整笔刷大小。
 ![Paint and Ruler](./assets/11-volview-paint-notes.jpg)

* 3D裁剪:选择此工具可调整3D渲染中显示的数据范围。在3D窗口中，您可以选择并移动角落，边缘和侧面标记来进行调整。在2D窗口中，抓取并移动覆盖在数据上的边界框的边缘。
 ![Crop](./assets/13-volview-crop.jpg)

[***观看视频!***](https://youtu.be/Bj4ijh_VLUQ)

有关工具栏的信息，请参阅["鼠标控制"](mouse_controls.html)和["工具栏控件"](toolbar.html)的文档。

## 3. 渲染控制

VolView读取数据的DICOM标签，以确定数据的电影体渲染的适当预设参数值，但通常您需要调整这些预设值以强调特定细节。我们建议按照以下顺序进行调整，以改善您的可视化效果。

1. 电影体绘制涉及两个“传递函数”:一个将记录的强度值(例如，CT霍斯菲尔德单位)映射到不透明度，另一个将记录的强度值映射到颜色。两者都可以使用render选项卡顶部的控件进行调整。顶部的图形显示了记录的强度值的直方图(浅灰色)和当前不透明度传递函数(黑色)的叠加曲线。在那张图中，黑色曲线下面是颜色传递函数的描述。 
   ![Cinematic](./assets/16-volview-rendering.jpg)
   
   1.  首先通过在顶部图形上向左/右按下拖动来调整不透明度传递函数。
    ![Opacity](./assets/17-volview-opacity-notes.jpg)
   2. 然后通过移动图形下方颜色栏上的蓝点来调整颜色传递函数。
   ![Color](./assets/17-volview-colormap-notes.jpg)
   
2. 您可能会认为颜色映射和/或传递函数不适合您的数据。单击“预设”栏展开并显示提供可选的不透明度和颜色传递功能的可用预设。
   ![Presets](./assets/18-volview-presets.jpg)
3. 接下来，可以控制灯光
    * 环境光是场景的一般亮度。
    * 漫射照明控制光线如何反射数据。它受光相对于数据局部表面方向的位置的影响。
    * 光线跟随相机可以启用/禁用以创建阴影，突出数据中的细节。启用后，灯将与相机对齐。当禁用时，即使相机移动，灯光的最后位置相对于数据保持固定。启用光线跟随相机后，以下是光线跟随相机时的视图: ![Default Lighting](./assets/20-volview-lightfollowcamera1.jpg)  通过将相机(以及光线)移动到数据的前面，然后禁用光线跟随相机，视图看起来应该是这样的:
    ![Light Setup](./assets/20-volview-lightfollowcamera2.jpg)  然后移回侧视图将显示强调深度和细节的阴影:
    ![Shadows](./assets/20-volview-lightfollowcamera3.jpg)

4. 高级，您还可以探索其他电影渲染方法。随后将提供详细的文档，描述这些方法并演示它们对各种类型的医疗数据的实用程序。
    *  标准
    *  混合
    *  环境闭塞

[***观看视频!***](https://youtu.be/eyrGd-meg6I)

## 4. 保存/加载状态

一旦您完成了度量并生成了您想要存储以便稍后调用或与他人共享的可视化，请使用工具栏顶部的图标来加载和保存状态文件。有关这些状态文件的json格式以及如何使用它们将VolView与工作流和其他服务集成的更多信息，请参阅[状态文件](state_files.html)。


