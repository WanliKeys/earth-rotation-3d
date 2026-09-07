# 地球自转 3D 交互式演示

基于 Three.js 的地球自转知识点交互演示应用：自转方向、自转周期、自转速度、昼夜更替、地方时/时区/区时、地转偏向力六大知识点，含 14 道针对性练习题。

## 运行方式

项目需通过 HTTP 服务器访问（`fetch` 加载 GeoJSON 受浏览器跨域限制，直接双击打开 `index.html` 无效）：

```bash
cd earth-rotation-3d
python3 -m http.server 8899
# 浏览器打开 http://localhost:8899/
```

也可使用任意静态文件服务器（`npx serve .`、VS Code Live Server 等）。项目无远程资源依赖，可完全离线运行。

## 功能

- **六大知识点演示**：自转方向 / 周期 / 速度、昼夜更替、地方时与区时、地转偏向力
- **多视角**：侧视图、北极俯视图、南极俯视图、球面展开图、对比视角窗口
- **可视化图层**：卫星影像图、分层设色地形图、政区图、空白底图；经纬线、时区、日界线、地方时、回归线、极圈、地轴、北极星、云层、内部透明等开关
- **交互**：日期滑块（二分二至预设）、速度控制、参照点（预设城市 + 自定义）、手势控制、语音控制
- **实时数据**：UTC 时间、太阳直射经纬度、晨昏圈 P 点纬度、偏转方向
- **针对性练习**：14 道选择题，附题目附图放大

## 目录结构

```
earth-rotation-3d/
├── index.html            页面入口
├── main.js               核心逻辑（已去混淆、资源已本地化）
├── quiz.js / quiz-data.js   针对性练习
├── gesture-control.js    手势控制
├── voice-control.js      语音控制
├── cosmic-starfield.js   星空背景
├── style.css             样式
├── libs/                 Three.js 运行时（three.min.js、OrbitControls.js）
├── textures/             地球贴图与矢量数据
│   ├── earth-atmos/bump/lights/clouds …  贴图（threejs 官方示例素材）
│   ├── earth-day.jpg / earth-pretty.jpg   地球影像
│   ├── ne_50m_admin_0_countries.geojson   政区矢量数据（Natural Earth）
│   └── ne_10m_admin_0_label_points.geojson 国家标注数据（Natural Earth）
├── images/               星空背景图、favicon
└── _shared/              响应式外壳
```

## 改造说明

本项目由公开教学演示《地球自转 3D 交互式演示》复刻而来，做如下改造：

1. **去除作者品牌信息**：移除版权弹窗（公众号/小程序二维码）、页面底部版权署名、页面保护脚本（`pageProtect.js`）
2. **去混淆**：`main.js` 原为混淆代码，已还原为可读形式（解码 6869 处字符串调用）
3. **资源本地化**：原项目依赖 threejs.org、jsdelivr 等 CDN 的贴图与矢量数据，已全部下载到 `textures/` 并改为相对路径，离线可用
4. **修复原站资源缺陷**：原站 `textures/earth-pretty.jpg`（默认分层设色贴图）与 `earth-clouds.png`（云层贴图）在源站即 404（页面依赖远程回退）；本地已补齐可用贴图

> 版权提示：原始应用版权归「地理广角镜 / 地理时空」所有，贴图素材来自 Three.js 官方示例与 Natural Earth（均为可自由使用素材）。本复刻仅建议用于个人学习与教学场景；如需公开或商业发布，请保留原始出处或获得授权。
