# 墨水屏相框 App 基准原型

当用户提出“墨水屏”“墨水屏相框”“相框 App”“送礼模式”“照片墙”“相册发送”“设备配网”等相关需求时，优先使用本基准原型作为修改起点。

## 基准文件

`assets/eink-frame-app-prototype.html`

该文件是 UGREEN 墨水屏相框 App 的三栏 LTT HTML 原型，包含左侧页面树、中间手机预览、右侧需求标注。后续需求修改应在该结构上定位相关页面、状态、数据对象和 annotation，而不是从空白模板重新生成。

## 使用规则

1. 先打开 `assets/eink-frame-app-prototype.html`，搜索 `menuTree`、`state`、`pages`、`annotations`、对应页面 id 或页面文案。
2. 修改时同时更新：
   - 左侧页面树节点。
   - 中间手机页面渲染。
   - 右侧需求标注。
   - 相关交互函数、状态对象和 mock 数据。
3. 保留三栏 LTT shell，不要替换为普通单屏 H5 或静态截图。
4. 对墨水屏设备特性保持一致表达：
   - 低频刷新、残影、休眠、唤醒。
   - BLE 辅助配网与 Wi-Fi 配置。
   - 相册、照片编辑、发送至相框、展示计划。
   - 礼品赠送、包装二维码、预配置祝福和照片。
   - 多相框、照片墙、设备日志等扩展能力。
5. 交互修改后必须验证目标页面可从左侧页面树进入，并且右侧 annotation 与页面行为一致。

## 文件放置

如果用户给的是桌面或下载目录中的新版原型，先复制到当前工作区或本 skill 仓库作为工作副本。不要直接覆盖用户桌面文件，除非用户明确要求。

对于后续需要沉淀进 skill 的稳定更新：

1. 更新 `assets/eink-frame-app-prototype.html`。
2. 如有新的规则或模块，更新本 reference。
3. 提交并推送 `prd-interactive-prototype-skill` 仓库。
4. 同步本机 `~/.codex/skills/prd-interactive-prototype` 中的 skill 文件，或提示用户重启 Codex 后使用新版 skill。
