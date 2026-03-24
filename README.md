# Web RTC 系统检测工具

基于火山引擎 Web RTC SDK 的系统兼容性检测工具，帮助开发者快速验证浏览器和设备对 WebRTC 的支持情况。

## 功能特性

### 浏览器兼容性检测
- 检测浏览器名称和版本
- 检查 `RTCPeerConnection` 支持
- 检查 `getUserMedia` 支持
- 检测 SDP、SRTP、UDP、TCP 协议支持

### 设备获取能力检测
- 枚举麦克风、扬声器和摄像头设备
- 显示设备详细信息
- 验证媒体设备权限获取

### 视频编码检测
- 检测 H264、H265、VP8 编码支持
- 通过火山引擎 SDK 或 SDP 分析检测

### 麦克风与扬声器检测
- 实时麦克风采集音量波形显示
- 录音并播放功能
- 实时扬声器播放音量波形显示

### 连通性检测
- 连接火山引擎 RTC 房间
- 本地视频预览
- 推流测试
- 视频分辨率支持检测（320x180 至 1920x1080）
- SDK 日志保存功能

## 项目结构

```
CheckBrowserConfiguration/
├── README.md           # 项目说明文档
├── index.html          # 主检测页面
├── rtc-check.js        # 核心检测逻辑
├── package.json        # 项目依赖配置
├── camera-test.html    # 摄像头测试页面
└── test-sdk.html       # SDK 测试页面
```

## 快速开始

### 前置要求
- Node.js 和 npm（使用 npm 服务时需要）
- Python 3（使用 Python 服务器时需要）

### 安装依赖

```bash
npm install
```

### 启动服务

#### 方法一：使用 Python 服务器（推荐）

```bash
npm run dev
```

#### 方法二：使用 npm serve

```bash
npm run serve
```

然后在浏览器中访问：http://localhost:8080

## 使用说明

### 基础检测流程

1. 打开页面后点击「开始检测」按钮
2. 允许浏览器访问摄像头和麦克风权限
3. 等待自动检测完成，查看各项检测结果
4. 底部日志区域显示详细的检测过程

### 麦克风与扬声器测试

1. 在「麦克风与扬声器检测」区域点击「开始采集」
2. 对着麦克风说话，观察音量波形
3. 点击「停止采集并播放」，验证扬声器功能

### 连通性测试

1. 填写 AppId、RoomId、UserId 和 Token
2. 点击「开始连通性测试」
3. 观察本地预览和推流状态
4. 测试完成后点击「停止测试」
5. 可点击「保存SDK日志」下载日志文件

## 协议检测方法说明

### SDP 协议（会话描述协议）
- **检测方法**：检查 `RTCPeerConnection.createOffer` 方法是否存在
- **原理**：createOffer 是生成 SDP 的核心方法，存在即表示支持 SDP 协议

### SRTP 协议（安全实时传输协议）
- **检测方法**：检查 `RTCPeerConnection.setConfiguration` 方法是否存在
- **原理**：setConfiguration 可以用来配置加密参数，支持该方法通常意味着浏览器支持 SRTP

### UDP 协议（用户数据报协议）
- **检测方法**：默认支持
- **说明**：WebRTC 通过 ICE 框架自动选择传输协议，现代浏览器都支持 UDP 作为首选传输协议

### TCP 协议（传输控制协议）
- **检测方法**：默认支持
- **说明**：WebRTC 也支持 TCP 作为备用传输协议（当 UDP 不可用时），现代浏览器都支持


## 注意事项

- 必须使用 HTTPS 或 localhost 访问，否则无法获取媒体设备权限
- 检测过程中请确保设备已正确连接
- 麦克风和扬声器测试会录制和播放音频，请确保环境合适
- 连通性测试需要有效的火山引擎 RTC 凭证（AppId、Token 等）
- 建议使用最新版本的 Chrome、Firefox、Safari 或 Edge 浏览器

## License

MIT
