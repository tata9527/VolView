# 工具栏

## 布局

使用布局按钮在窗口安排之间进行选择。在所有的事情，如果你想添加特定的布局，请提出功能请求[问题跟踪器](https://github.com/Kitware/VolView/issues)。

![布局](./assets/07-volview-layout-notes.jpg)

## 2D视图鼠标左键

窗口/等级、平移、缩放或十字准线:选择这些选项可以控制鼠标左键在2D窗口中的功能。

![Window-Level, Pan, Zoom, Crosshairs](./assets/10-volview-wl-pan-zoom-notes.jpg)

## 2D 标注

“标注”选项卡列出了绘制的、基于矢量的注释工具。列表中的每个工具都有一个“滚动到切片”和删除按钮。

### 绘画

当选择绘画工具时，您可以在任何2D窗口中绘画。第二次点击绘画工具，调出颜色菜单，调整笔刷大小。
### 矩形

当选择矩形工具时，使用鼠标左键可以放置和调整矩形控制点。
右键单击矩形控制点以删除该矩形。
“标注”选项卡列出了所有矩形，并提供跳转到和删除控件。

可以用标签标记矩形注释。使用左上角的调色板或 `q` 或 `w`键来选择活动标签。

### 多边形

选择多边形工具:

- 放置点:鼠标左键。
- 删除最后放置点:鼠标右键。
- 删除所有点: `Esc` 键。 
- 放置3个点后关闭多边形:点击第一个点，按`Enter`键或双击鼠标左键。

闭合多边形后:

- 移动点:用鼠标左键拖动点。
- 添加点:鼠标左键在多边形线上。
- 删除点:右键单击点，选择删除点。
- 删除多边形:右键单击点或线，选择删除多边形。

多边形注释可以用标签标记。使用左上角的调色板或 `q `或 `w` 键来选择活动标签。

### 直尺

当选择直尺工具时，使用鼠标左键放置和调整标尺末端标记。右键单击结束标记将显示一个弹出菜单，用于删除该直尺。切换到 `标注` 选项卡，查看当前加载数据的注释列表。选择所列标尺旁边的位置图标以跳转到其切片。选择要删除该标尺的垃圾桶。

标尺注释可以用标签标记。使用左上角的调色板或 `q` 或 `w` 键来选择活动标签。

![2D 标注](./assets/11-volview-paint-notes.jpg)

### 标签的配置

如果VolView加载一个JSON文件匹配下面的模式，标签被添加到2D标注工具。
示例配置JSON:

```json
{
  "labels": {
    "rulerLabels": {
      "big": { "color": "#ff0000" },
      "small": { "color": "white" }
    },
    "rectangleLabels": {
      "innocuous": { "color": "white", "fillColor": "#00ff0030" },
      "lesion": { "color": "#ff0000", "fillColor": "transparent" },
      "tumor": { "color": "green", "fillColor": "transparent" }
    }
  }
}
```

标签部分可以为空，以禁用工具的标签。

```json
{
  "labels": {
    "rulerLabels": null,
    "rectangleLabels": {
      "innocuous": {
        "color": "white",
        "fillColor": "#00ff0030"
      },
      "lesion": {
        "color": "#ff0000",
        "fillColor": "transparent"
      }
    }
  }
}
```

Tools will fallback to `defaultLabels` section if the tool has no specific labels property,
ie `rectangleLabels` or `rulerLabels`.

如果工具没有特定的标签属性，工具将回退到 `defaultLabels` 部分。
即 `rectangleLabels` 或 `rulerLabels`。

```json
{
  "labels": {
    "defaultLabels": {
      "artifact": { "color": "gray" },
      "needs-review": { "color": "#FFBF00" }
    }
  }
}
```

## 3D 剪裁

选择此工具可调整3D渲染中显示的数据范围。在3D窗口中，您可以选择并移动角落，边缘和侧面标记来进行调整。在2D窗口中，抓取并移动覆盖在数据上的边界框的边缘。

![剪裁](./assets/13-volview-crop.jpg)

[**_Watch the video!_**](https://youtu.be/Bj4ijh_VLUQ)
