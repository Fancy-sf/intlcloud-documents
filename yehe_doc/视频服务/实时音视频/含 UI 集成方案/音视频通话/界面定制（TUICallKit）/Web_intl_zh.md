本文将介绍如何定制 TUICallKit 的用户界面，我们提供了两个方案供您选择：界面微调方案和自实现 UI 方案。

## 方案一：界面微调方案

通过直接修改我们提供的 UI 源代码，对 TUICallKit 的用户界面进行调整，TUICallKit 的界面源代码位于 [Github](https://github.com/tencentyun/TUICallKit) 中的 `Web/` 文件夹下面：

### 替换图标

您可以直接修改 `src/icons` 文件夹下的图标组件，以确保整个 app 中的图标色调风格保持一致，请在替换时保持图标文件的名字不变，图标预览可参考 `src/assets`。
![img](https://qcloudimg.tencent-cloud.cn/image/document/63512402ae3cee72786afcc919a988ce.png)

### 调整 UI 布局

您可以通过修改 src/components/ 文件下的不同页面来修改音视频通话界面

```bash
- components/
    - Calling-C2CVideo.vue          双人视频通话
    - Calling-Group.Vue             多人音频、视频通话
    - ControlPanel.vue              控制面板
    - ControlPanelItem.vue          控制面板子项
    - Dialing.vue                   拨打电话页面、来电页面、双人音频通话
    - MicrophoneIcon.vue            可显示音量变化的麦克风Icon
    - TUICallKit.vue                TUICallKit 总组件
```

### 修改样式

样式文件在 `src/style.css`，根据不同的 UI 样式，可以进行自行调整。

## 方案二：自实现 UI 方案

TUICallKit 的整个通话功能是基于 TUICallEngine 这个无 UI SDK 实现的，您可以完全基于 TUICallEngine 实现一套自己的 UI 界面。详情请参见 [API 接口地址](https://www.tencentcloud.com/document/product/647/51016)。