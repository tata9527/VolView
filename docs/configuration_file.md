# 配置 JSON 文件

通过加载一个JSON文件，你可以设置VolView的配置:

- 起始视图布局(仅轴向，3D主视图等)。
- 工具标签
- 示例数据部分的可见性
- 键盘快捷键

## 起始视图布局

`activeLayout` 键在`config.ts` 文件中定义了选项(Axial Only, 3D Primary,等)。
```json
{
  "layout": {
    "activeLayout": "Axial Only"
  }
}
```

## 工具标签

每种工具类型(矩形，多边形等)都可以有工具特定的标签。共享标签跨工具，定义 `defaultLabels` 键，不要为应该使用默认标签的工具提供标签。

```json
{
  "labels": {
    "defaultLabels": {
      "lesion": { "color": "#ff0000" },
      "tumor": { "color": "green", "strokeWidth": 3 }
    }
  }
}
```

## 段组文件格式

`segmentGroupSaveFormat` 键指定VolView将包含在VolView.zip文件中的段组图像的文件扩展名。


```json
{
  "io": {
    "segmentGroupSaveFormat": "nii"
  }
}
```

工作段组文件的扩展名可以是以下格式:

hdf5, iwi.cbor, mha, nii, nii.gz, nrrd, vtk

## 按文件名自动组段

加载文件时，VolView可以自动将图像转换为段组，如果他们遵循命名约定。例如，名称为 `foo.segmentation.bar` 将被转换为名为 `foo.baz` 的基本图像的段组。

`segmentation` 扩展是由 `io.segmentGroupExtension` 键定义的。它接受一个字符串。

默认值为`''`，将禁用该功能。

这里定义 `myFile.seg.nrrd` 作为 `myFile.nii` 基础文件的段组。

```json
{
  "io": {
    "segmentGroupExtension": "seg"
  }
}
```

## 快捷键

配置键以激活工具、更改所选标签等。
所有 [快捷操作](..\src\constants.ts#L24) 都在 `ACTIONS` 变量下。

要为操作配置一个键，请在 `shortcuts` 部分下添加其操作名称和键。对于组合键，使用`+` ，就像 `Ctrl+f` 一样。

```json
{
  "shortcuts": {
    "polygon": "Ctrl+p",
    "showKeyboardShortcuts": "t"
  }
}
```

## 示例数据可见性

隐藏示例样本数据可以简化浏览器界面。

```json
{
  "dataBrowser": {
    "hideSampleData": false
  }
}
```

## 示例 JSON:

```json
{
  "labels": {
    "defaultLabels": {
      "lesion": { "color": "#ff0000" },
      "tumor": { "color": "green", "strokeWidth": 3 }
    }
  },
  "layout": {
    "activeLayout": "Axial Only"
  }
}
```

## 全部选项:

```json
{
  "labels": {
    "defaultLabels": {
      "lesion": { "color": "#ff0000" },
      "tumor": { "color": "green", "strokeWidth": 3 },
      "innocuous": { "color": "white" }
    },
    "rulerLabels": {
      "big": { "color": "#ff0000" },
      "small": { "color": "white" }
    },
    "rectangleLabels": {
      "red": { "color": "#ff0000", "fillColor": "transparent" },
      "green": { "color": "green", "fillColor": "transparent" },
      "white-yellow-fill": {
        "color": "white",
        "fillColor": "#00ff0030"
      }
    },
    "polygonLabels": {
      "poly1": { "color": "#ff0000" },
      "poly2Label": { "color": "green" }
    }
  },
  "layout": {
    "activeLayout": "Axial Only"
  },
  "dataBrowser": {
    "hideSampleData": false
  },
  "shortcuts": {
    "polygon": "Ctrl+p",
    "showKeyboardShortcuts": "t"
  },
  "io": {
    "segmentGroupSaveFormat": "nrrd"
  }
}
```
