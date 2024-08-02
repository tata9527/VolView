# 电影体渲染

VolView读取数据的DICOM标签，以确定数据的电影体渲染的适当预设参数值，但通常您需要调整这些预设值以强调特定细节。我们建议按照以下顺序进行调整，以改善您的可视化效果。

1. 电影体渲染涉及两个“传递函数”:一个将记录的强度值(例如，CT霍斯菲尔德单位)映射到不透明度，另一个将记录的强度值映射到颜色。两者都可以使用render选项卡顶部的控件进行调整。顶部的图形显示了记录的强度值的直方图(浅灰色)和当前不透明度传递函数(黑色)的叠加曲线。在图中，黑色曲线下面是颜色传递函数的描述。 ![Cinematic](./assets/16-volview-rendering.jpg)

   1. 首先通过在顶部图形上向左/右按下拖动来调整不透明度传递函数。 ![Opacity](./assets/17-volview-opacity-notes.jpg)
   2. 然后通过移动图形下方颜色栏上的蓝点来调整颜色传递函数。 ![Color](./assets/17-volview-colormap-notes.jpg)

2. 您可能会认为颜色映射和/或传递函数不适合您的数据。单击 “预设” 栏展开并显示提供可选的不透明度和颜色传递功能的可用预设。 ![Presets](./assets/18-volview-presets.jpg)
   [**_Watch the video!_**](https://youtu.be/eyrGd-meg6I)

3. 接下来，可以控制灯光。

   1. 环境光是场景的一般亮度。
   2. 漫射照明控制光线如何反射数据。它受光线相对于数据局部表面方向的位置影响。
   3. 光线跟随相机可以启用/禁用以创建阴影，突出数据中的细节。启用后，灯将与相机对齐。当禁用时，即使相机移动，灯光的最后位置相对于数据保持固定。启用光线跟随相机后，以下是光线跟随相机时的视图: ![Default Lighting](./assets/20-volview-lightfollowcamera1.jpg)。通过将相机(以及光线)移动到数据的前面，然后禁用光线跟随相机，视图看起来应该是这样的: ![Light Setup](./assets/20-volview-lightfollowcamera2.jpg). 然后移回侧视图将显示强调深度和细节的阴影: ![Shadows](./assets/20-volview-lightfollowcamera3.jpg).

4. 高级，您还可以探索其他电影渲染方法。
   1. 标准
   2. 混合
   3. 遮蔽环境光
