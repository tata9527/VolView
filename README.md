# VolView

![A screenshot of a sample VolView session](./docs/assets/VolView-Overview.jpg)

## 试用

在线试用volview: https://volview.kitware.app/

## 介绍

VolView是为临床专业人员开发的开源放射查看器。使用VolView，您可以通过交互式电影体渲染对数据有更深入的视觉理解，并轻松地将DICOM数据可视化为3D。由于VolView在你的浏览器中运行，你不需要安装软件，你的数据可以安全地保存在你的机器上。

Major features of VolView include:
VolView的主要功能包括:

1. 拖放操作：将DICOM图像拖放到VolView上，它们将被快速解析并显示为缩略图。点击缩略图，数据就会被快速加载，并以2D切片和3D电影体渲染的形式呈现。

2. 电影体渲染:创建美丽的渲染，并获得新的见解，您的数据，只需点击几下。VolView提供了三种电影体量渲染模式和直观的控制。我们还提供了简单的方法来控制照明和多个预设，让你开始。

3. 注释和测量量:我们已经提供了一小组用于绘制、度量和裁剪的工具，并且该工具集将迅速扩展。如果您有关于新工具或改进VolView的建议，请在我们的[问题跟踪器](https://github.com/Kitware/VolView/issues)留下反馈。

4. 简单，可扩展和安全:只需访问一个网站安装VolView。一旦它开始运行，所有的数据处理、处理和可视化都在您的机器上进行。你载入VolView的数据永远不会离开你的机器。VolView可以在任何浏览器上运行:从你手机上的浏览器到你最强大的工作站上的浏览器。它将利用本地GPU资源来加速其渲染过程，但如果没有可用的，它仍然会生成相同的高质量渲染，尽管有点慢。
5. 未来的基础：VolView旨在为您未来的项目和产品提供基础。它是开源的，免费供商业和学术使用。您可以自己修改它，或者Kitware可以帮助您自定义它，以支持客户机-服务器工作流，提供简化的接口和工具，并传播您的品牌。

## 文档

访问: https://kitware.github.io/VolView 阅读文档。

# 引用

如果你发现VolView对你的工作有用，请引用我们关于电影渲染的论文:

[Jiayi Xu, Gaspard Thevenon, Timothee Chabat, Matthew McCormick, Forrest Li,Tom Birdsong,Ken Martin, Yueh Lee, and Stephen Aylward, "在浏览器中对医学图像进行交互式，电影质量的体积渲染", MICCAI 2022 AE-CAI Workshop, Singapore, Sept 19, 2022, Journal version accepted for publication in Computer Methods in Computer Methods in Biomechanics and Biomedical Engineering](docs/Paper48_IICVR_camera_ready_paper.pdf): 

要包含对VolView 4.0源代码的引用，请使用以下DOI: [![DOI](src\assets\logo.svg)](https://github.com/Kitware/VolView?tab=readme-ov-file)

# 定制VolView

请参阅 [Contributing.md](Contributing.md) 文档。

# 致谢

This work was funded, in part, by the NIH via NIBIB and NIGMS R01EB021396, NIBIB R01EB014955, NCI R01CA220681, and NINDS R42NS086295.
