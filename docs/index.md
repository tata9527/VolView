# VolView是什么?

VolView是为临床专业人员开发的开源放射查看器。使用VolView，您可以通过高质量的交互式可视化(包括电影体效果图)更深入地了解数据。由于VolView在你的浏览器中运行，你不需要安装软件，你的数据可以安全地保存在你的机器上。

![Welcome](./assets/VolView-Overview.jpg)

## 产品特点

VolView的主要功能包括:

1. **影片体绘制**: 只需点击几下即可创建漂亮的渲染图并获得对数据的新见解。VolView提供了三种电影体量渲染模式和直观的控制。我们还提供了简单的方法来控制照明和多个预设，让你开始。

2. **拖拽操作 DICOM 影像**: 将DICOM图像拖到VolView上，它们将被快速解析并显示为缩略图。点击缩略图，数据就会被快速加载，并以2D切片和3D电影体渲染的形式呈现。

3. **标注与测量**: 将DICOM图像拖放到VolView上，它们将被快速解析并呈现为缩略图。点击缩略图，数据将迅速加载，并以2D切片和3D电影级体素渲染的形式展示。 [问题跟踪](https://github.com/Kitware/VolView/issues).

4. **易用性、扩展性和安全性**: 只需访问一个网站安装VolView。一旦它开始运行，所有的数据处理、处理和可视化都在您的机器上进行。你载入VolView的数据永远不会离开你的机器。VolView可以在任何浏览器上运行:从你手机上的浏览器到你最强大的工作站上的浏览器。它将利用本地GPU资源来加速其渲染过程，但如果没有可用的，它仍然会生成相同的高质量渲染，尽管有点慢。

5. **面向未来**: VolView旨在为您未来的项目和产品奠定基础。它是开源的，免费供商业和学术使用。您可以自己修改它，或者Kitware可以帮助您自定义它，以支持客户机-服务器工作流，提供简化的接口和工具，并传播您的品牌。

VolView **不是FDA批准用于任何目的**，但Kitware可以与您合作创建自定义版本的VolView并提交FDA批准。更多信息请联系[kitware@kitware.com](mailto:kitware@kitware.com)。

## 历史

VolView 1.1版本于1999年9月21日发布，为临床专业人员提供业界领先的体绘制功能的直观界面。使用[VTK](https://vtk.org)构建，在当时是极具创新性的。它提供了交互式体效果图，不需要为知名医疗设备制造商购买专用系统。它支持Windows 95/98/NT、Sun、Silicon Graphics和Linux环境，并提供定制的细节级和复合渲染技术。这个版本的VolView蓬勃发展了十多年，最后一次发布是在2011年6月。2011年，开放源代码的放射观察器已经变得司空见惯(许多也使用VTK构建)，我们将注意力转向3D Slicer，一个开源的，跨平台的，功能丰富的，面向医疗图像的，切片器作为一个先进的，社区支持的，可扩展的研究和临床应用开发平台。

我们在2022年发布了VolView 4.0，再次推动放射图像可视化领域的发展。使用VTK的javascript版本(即[VTK .js](https://kitware.github.io/vtk-js/index.html))构建，VolView 4.0在web浏览器中运行，并提供仅在大牌医疗设备制造商销售的专用系统中广泛提供的电影体积渲染功能。我们期待继续使用VolView平台进行医学图像可视化创新，计划支持全息和AR/VR设备的WebXR，以及用于高级图像分析的配套库(例如，[it.wasm](https://github.com/InsightSoftwareConsortium/itk-wasm))和AI算法(例如，通过[MONAI](https://monai.io))。

## 路线图

我们路线图的细节和进展在Github上的VolView问题跟踪器中进行跟踪:https://github.com/Kitware/VolView/issues

我们的下一个主要版本计划于2023年3月发布，它将支持:
* DICOM网站
* DICOM SEG, RT, SR读写
* ITK用于图像处理
* 图像分析的深度学习推理

## 引用

如果你发现VolView对你的工作有用，请引用我们关于电影渲染的论文:

[Xu J, Thevenon G, Chabat T, McCormick M, Li F, Birdsong T, Martin K, Lee Y, and Aylward S, "Interactive, in-browser cinematic volume rendering of medical images", Computer Methods in Computer Methods in Biomechanics and Biomedical Engineering: Imaging & Visualization](https://www.tandfonline.com/doi/full/10.1080/21681163.2022.2145239)

要参考VolView的源代码，请提供https://github.com/Kitware/VolView的链接并引用[DOI:10.5281/zendo.7328066](https://zenodo.org/badge/latestdoi/248073292)。

## 致谢

This work was funded, in part, by the NIH via NIBIB and NIGMS R01EB021396, NIBIB R01EB014955, NCI R01CA220681, and NINDS R42NS086295.

## 相关工作

你可透过以下连结了解我们的相关工作:
* Glance:在web浏览器中的通用科学可视化
    * https://kitware.github.io/glance/index.html
* 3D Slicer: 桌面(c++和Python)，可扩展的放射查看器
    * https://slicer.org
* trame: 用于快速创建涉及服务器端渲染和计算的web应用程序的Python框架。
    * https://kitware.github.io/trame/index.html
* itk.wasm: 用于浏览器内图像分割和注册的ITK的Web-assembly版本，具有出色的DICOM支持。
    * https://github.com/InsightSoftwareConsortium/itk-wasm
* vtk.js: 一个纯javascript库，用于在web浏览器中进行高级，交互式，科学的可视化。
    * https://kitware.github.io/vtk-js/index.html
