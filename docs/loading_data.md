# 加载数据

将文件加载到VolView中最直接的方法是在查看“数据”选项卡时将它们拖放到中央窗口。您也可以在中央窗口内单击打开文件浏览器，并通过右上方工具栏上的“打开”按钮选择文件或文件夹。为了补充不同的用例，还有一些其他的打开文件的方法。

## File formats

VolView支持加载多个DICOM文件、包含多个DICOM文件的文件夹或包含多个DICOM文件的压缩文件。由于ITK和ITK的广泛I/O功能，它还支持加载Nifti、NRRD、MHA和20多种其他文件格式。但是在加载非dicom数据时必须小心，因为不能保证这些文件中数据的方向。

## 样本数据

VolView包含各种示例数据的链接。点击这些缩略图在数据选项卡将下载数据从Kitware data.kitware.com网站到您的本地机器。

## DICOMWeb

VolView列出并下载DICOMWeb服务提供的DICOM文件。DICOMWeb服务的主机地址可以通过以下方式配置:

- VolView 设置菜单
- `dicomweb` URL参数。例如:`https://volview.kitware.app/?dicomweb=https://dicomweb-server.com`
- 在VolView构建时使用 `VITE_DICOM_WEB_URL` 环境变量。

DICOMWeb地址可以指向研究中的特定系列，VolView将自动加载整个系列。示例URL:

```
https://volview.kitware.app/?dicomweb=https://dicomweb-server.com/studies/unique-study-id-here/series/unique-series-id-here
```

## 通过url加载远程数据

VolView支持在应用程序启动时通过URL参数加载远程数据集。这个集成的例子可以在这里查看: [VolView 样本数据](https://volview.kitware.app/?names=[prostate-mri.zip,neck.mha]&urls=[https://data.kitware.com/api/v1/item/63527c7311dab8142820a338/download,https://data.kitware.com/api/v1/item/620db4b84acac99f42e75420/download])

URL由两部分组成，如下所示。必需的参数是 `urls`参数，它指定要下载的url列表。可选的 `names` 参数指定文件的文件名。如果VolView无法推断文件类型，则使用文件名的扩展名作为回退。加载多个url是通过用逗号分隔它们来实现的。
```
https://volview.kitware.app/?names=[prostate-mri.zip,neck.mha]&urls=[https://data.kitware.com/api/v1/item/63527c7311dab8142820a338/download,https://data.kitware.com/api/v1/item/620db4b84acac99f42e75420/download]
```

### 谷歌云存储桶和AWS S3支持

VolView supports both Google Cloud Storage links of the form
`gs://<bucket>/<object>` and Amazon AWS S3 buckets of the form
`s3://<bucket>/<object>`. VolView can either download a single object, or
download everything underneath a given object prefix/folder. As an example,
VolView will download and load every file that exists in the
`gs://my-public-bucket/my-patient-folder/` folder.

VolView支持形式为 `gs://<bucket>/<object>` 的谷歌云存储链接和形式为 `s3://<bucket>/<object>` 的Amazon AWS S3桶。VolView既可以下载单个对象，也可以下载给定对象前缀/文件夹下的所有内容。例如，VolView将下载并加载  `gs://my-public-bucket/my-patient-folder/` 文件夹中的每个文件。

需要注意的是，没有检查总下载的大小。因此，在指定桶级前缀时要小心!
该特性目前只支持匿名访问的公共桶。将来可能会添加经过身份验证的支持。如果你有
它的强大用例，请通过我们的问题请求页(https://github.com/Kitware/VolView/issues) !

### CORS

为了使VolView下载和显示您的远程数据集，您的服务器必须配置正确的[CORS](https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS)配置。CORS是一种浏览器安全机制，它限制了web应用程序访问远程资源的方式。如果没有正确的CORS配置，VolView将无法下载和显示您的数据集。使用CORS配置您的web服务器超出了本文档的范围;请参考您的服务器的文档。

## 层图像

要在2D视图中覆盖图像，在图像缩略图上有一个图层按钮。PET图像可以叠加在CT图像上。使用图像的空间元数据将分层图像重新采样到基础图像。如果空间元数据没有将图像放置在同一坐标系中，则层对齐将是不正确的。

图层图像:
1. 加载基本映像。
2. 在“数据”页签中，单击上层数据集上的“添加图层”按钮。
3. 在渲染选项卡下，一个不透明度滑块可以改变上层的透明度。

![添加图层](./assets/add-layer.jpg)
