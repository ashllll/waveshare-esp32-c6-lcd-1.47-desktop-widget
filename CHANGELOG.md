# 更新日志

本项目所有重要变更记录于此文件。
格式参考 [Keep a Changelog](https://keepachangelog.com/zh-CN/1.1.0/),每次推送前必须更新本文件。

## 2026-08-17 · 文档更新

### 新增

- README 新增「实际显示画面」一节:`docs/ui-preview.svg` 界面效果图,依据 `ui_create()` 的布局坐标与配色 1:1 虚拟生成
- README 目录结构补充 `docs/`

### 修正

- README 功能描述与当前代码对齐:首页为 iKuai 网络监控面板(WAN 状态 / 上下行速率 / PING / 10 秒三色趋势曲线),移除已过时的「时钟 + Open-Meteo 天气」描述(代码中已无对应实现)
- 补充 RGB 状态灯颜色语义(Wi-Fi 断开红 / iKuai 无数据橙 / 正常绿)与 `APP_DEMO_MODE` 离线演示模式说明

## 2026-08-17 · 初始发布

### 新增

- LVGL 桌面信息摆件界面:Wi-Fi 校时时钟 + Open-Meteo 天气 + 状态栏,背光上限 40%
- iKuai 路由器实时监控:HTTPS + Bearer token + 固定证书,1s 轮询 CPU / 内存 / 在线数 / 实时上下行速率,ICMP ping 网关延迟,60 点滚动曲线
- TF 卡(microSD,SPI 模式,与 LCD 共享 SPI2 总线)天气日志:追加写入 `/sdcard/weather.log`,无卡/坏卡不阻塞启动
- ST7789 172×320 SPI LCD 驱动与 LVGL 显示移植层
- 板载 WS2812 RGB 状态灯(GPIO8)
- 敏感配置模板 `src/config.example.h` 与 `src/ikuai_cert.example.h`(真实配置经 `.gitignore` 排除)
- 8MB Flash 分区表(factory app 3MB)
- 中文 README:硬件 / 功能 / 构建 / 配置 / 目录结构
- 本更新日志
