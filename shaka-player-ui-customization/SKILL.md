---
name: "shaka-player-ui-customization"
description: "Customizes Shaka Player UI including controls, localization, and accessibility. Invoke when user needs to customize player appearance or add custom controls."
---

# Shaka Player UI Customization

This skill helps you customize the Shaka Player UI library, including controls, localization, accessibility features, and Chromecast integration.

## When to Use

Invoke this skill when:
- User needs to set up the UI library
- User wants to customize player controls
- User needs to enable Chromecast support
- User wants to enable VR playback
- User needs to localize the player UI

## Input Parameters

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `castReceiverAppId` | string | No | Chromecast receiver application ID |
| `config` | object | No | UI configuration object |
| `locale` | string | No | Language locale for UI |

## Setting Up UI Library

### HTML-based Setup (Declarative)

```html
<!DOCTYPE html>
<html>
  <head>
    <!-- Shaka Player UI compiled library -->
    <script src="dist/shaka-player.ui.js"></script>
    <!-- Shaka Player UI CSS -->
    <link rel="stylesheet" type="text/css" href="dist/controls.css">
    <!-- Chromecast SDK (optional) -->
    <script defer src="https://www.gstatic.com/cv/js/sender/v1/cast_sender.js"></script>
    <!-- Your application source -->
    <script src="myapp.js"></script>
  </head>
  <body>
    <!-- UI 容器 -->
    <div data-shaka-player-container style="max-width:40em"
         data-shaka-player-cast-receiver-id="07AEE832">
      <!-- 视频元素 -->
      <video autoplay data-shaka-player id="video" 
             style="width:100%;height:100%"></video>
    </div>
  </body>
</html>
```

### JavaScript Initialization

```javascript
// myapp.js

const manifestUri = 'https://storage.googleapis.com/shaka-demo-assets/angel-one/dash.mpd';

async function init() {
  // 使用 UI 时，player 由 UI 对象自动创建
  const video = document.getElementById('video');
  const ui = video['ui'];
  const controls = ui.getControls();
  const player = controls.getPlayer();
  
  // 附加到 window 以便控制台访问
  window.player = player;
  window.ui = ui;
  
  // 监听错误事件
  player.addEventListener('error', onPlayerErrorEvent);
  controls.addEventListener('error', onUIErrorEvent);
  
  // 加载清单
  try {
    await player.load(manifestUri);
    console.log('The video has now been loaded!');
  } catch (error) {
    onPlayerError(error);
  }
}

function onPlayerErrorEvent(errorEvent) {
  onPlayerError(errorEvent.detail);
}

function onPlayerError(error) {
  console.error('Error code', error.code, 'object', error);
}

function onUIErrorEvent(errorEvent) {
  onPlayerError(errorEvent.detail);
}

function initFailed(errorEvent) {
  console.error('Unable to load the UI library!');
}

// 监听 UI 加载事件
document.addEventListener('shaka-ui-loaded', init);
document.addEventListener('shaka-ui-load-failed', initFailed);
```

## Programmatic UI Setup

```javascript
// 编程式设置 UI
const localPlayer = new shaka.Player();
const videoContainerElement = document.getElementById('video-container');
const videoElement = document.getElementById('video');

// 创建 UI 覆盖层
const ui = new shaka.ui.Overlay(localPlayer, videoContainerElement, videoElement);

// 附加播放器到视频元素
await localPlayer.attach(videoElement);

// 获取控件和播放器
const controls = ui.getControls();
const player = controls.getPlayer();
const video = controls.getVideo();

// 配置 Chromecast
ui.configure({
  'castReceiverAppId': '07AEE832',
  'castAndroidReceiverCompatible': true
});
```

## Auto-loading Content

### Using src Attribute

```html
<div data-shaka-player-container style="max-width:40em"
     data-shaka-player-cast-receiver-id="07AEE832">
  <!-- src 属性中的清单 URL 将自动加载 -->
  <video autoplay data-shaka-player id="video" 
         style="width:100%;height:100%"
         src="https://storage.googleapis.com/shaka-demo-assets/angel-one/dash.mpd">
  </video>
</div>
```

### Using source Tags

```html
<div data-shaka-player-container style="max-width:40em"
     data-shaka-player-cast-receiver-id="07AEE832">
  <video autoplay data-shaka-player id="video" style="width:100%;height:100%">
    <!-- 首选清单 -->
    <source src="https://storage.googleapis.com/shaka-demo-assets/angel-one/dash.mpd"/>
    <!-- 备用清单 -->
    <source src="https://storage.googleapis.com/shaka-demo-assets/angel-one-hls-apple/master.m3u8"/>
  </video>
</div>
```

## Chromecast Integration

### Enable Chromecast

```html
<div data-shaka-player-container 
     data-shaka-player-cast-receiver-id="YOUR_APP_ID">
  <video data-shaka-player id="video"></video>
</div>
```

### Monitor Cast Status

```javascript
const controls = ui.getControls();

// 监听投屏状态变化
controls.addEventListener('caststatuschanged', (event) => {
  const newCastStatus = event['newStatus'];
  console.log('Cast status changed:', newCastStatus);
  
  if (newCastStatus) {
    showCastConnectedMessage();
  } else {
    showCastDisconnectedMessage();
  }
});
```

### Android Receiver Apps

```html
<div data-shaka-player-container 
     data-shaka-player-cast-receiver-id="07AEE832"
     data-shaka-player-cast-android-receiver-compatible="true">
  <video data-shaka-player id="video"></video>
</div>
```

## VR Playback

### Enable VR Mode

```javascript
// 方式 1：通过配置启用
ui.configure({
  'displayInVrMode': true
});
```

### Automatic VR Detection

VR is automatically enabled for content with:
- HLS or DASH manifest
- fMP4 segments
- Init segment contains `prji` and `hfov` boxes

### External VR Canvas

```html
<!-- 在外部 canvas 元素上渲染 VR -->
<canvas data-shaka-player-vr-canvas id="vr-canvas"></canvas>
<div data-shaka-player-container>
  <video data-shaka-player id="video"></video>
</div>
```

**Note**: VR is only supported for clear streams or HLS-AES streams. DRM prevents access to video pixels for transformation.

## Keyboard Shortcuts

| Shortcut | Action |
|----------|--------|
| `Spacebar` | Play/Pause (when seek bar is focused) |
| `←` / `→` | Seek backward/forward 5 seconds |
| `PageDown` / `PageUp` | Seek backward/forward 60 seconds |
| `Home` / `End` | Seek to beginning/end |
| `c` | Toggle closed captions |
| `f` | Toggle full screen |
| `m` | Mute/unmute |
| `p` | Toggle picture-in-picture |
| `>` | Increase playback rate |
| `<` | Decrease playback rate |

### Customize Keyboard Shortcuts

```javascript
ui.configure({
  'keyboardSeekDistance': 10,        // 箭头键跳转距离（秒）
  'keyboardLargeSeekDistance': 30    // PageUp/Down 跳转距离（秒）
});
```

## Stream Metadata for UI

### Display Title

Configure streams to display title in UI:

**ID3**: Use `TIT2` tag
**HLS**: Include `#EXT-X-SESSION-DATA` with ID `com.apple.hls.title`
**DASH**: Use `ProgramInformation` element with `Title` field

### Display Poster

Configure streams to display poster in UI:

**ID3**: Use `APIC` tag
**HLS**: Include `#EXT-X-SESSION-DATA` with ID `com.apple.hls.poster`

**Note**: This metadata is also used by the Media Session API.

## UI Configuration Options

```javascript
ui.configure({
  // 控件配置
  'controlPanelElements': [
    'play_pause',
    'mute',
    'volume',
    'time_and_duration',
    'fullscreen',
    'overflow_menu',
    'cast'
  ],
  
  // 溢出菜单项
  'overflowMenuButtons': [
    'captions',
    'quality',
    'language',
    'picture_in_picture',
    'cast'
  ],
  
  // 自定义跳转距离
  'keyboardSeekDistance': 5,
  'keyboardLargeSeekDistance': 60,
  
  // VR 模式
  'displayInVrMode': false,
  
  // Chromecast
  'castReceiverAppId': 'YOUR_APP_ID',
  'castAndroidReceiverCompatible': false
});
```

## Localization

Shaka Player UI supports localization with lazy-loaded translations.

```javascript
// UI 会根据浏览器语言自动选择本地化
// 也可以通过 URL 参数覆盖：?lang=zh-CN
```

## Accessibility

Shaka Player UI provides:
- Keyboard navigation
- Screen reader support
- High contrast mode support
- ARIA labels for all controls

## Custom Controls

### Add Custom Button

```javascript
// 创建自定义按钮
class MyCustomButton extends shaka.ui.Element {
  constructor(parent, controls) {
    super(parent, controls);
    
    this.button_ = document.createElement('button');
    this.button_.textContent = 'Custom';
    this.button_.addEventListener('click', () => {
      // 自定义操作
      console.log('Custom button clicked');
    });
    
    this.parent.appendChild(this.button_);
  }
}

// 注册自定义控件
shaka.ui.Controls.registerElement('custom_button', MyCustomButton);

// 在配置中使用
ui.configure({
  'controlPanelElements': ['play_pause', 'custom_button', 'mute']
});
```

## Best Practices

1. **Use declarative setup** when possible for simplicity
2. **Provide fallback sources** for robustness
3. **Test keyboard navigation** for accessibility
4. **Customize controls** to match your application's needs
5. **Handle cast status changes** for better user experience
6. **Use appropriate metadata** for title and poster display

## Common Issues

### 1. UI Not Loading

- Check if `shaka-player.ui.js` is loaded
- Verify `controls.css` is included
- Check browser console for errors

### 2. Cast Button Not Showing

- Verify Chromecast SDK is loaded
- Check `castReceiverAppId` is set
- Ensure device is on same network

### 3. VR Not Working

- Verify content meets VR requirements
- Check if stream is DRM-protected (not supported)
- Ensure canvas element is properly configured

## Related Skills

- `shaka-player-basic-usage`: Basic player setup
- `shaka-player-configuration`: Player configuration
- `shaka-player-accessibility`: Accessibility features
