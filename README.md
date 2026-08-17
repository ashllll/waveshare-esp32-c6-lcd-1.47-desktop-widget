# Waveshare ESP32-C6-LCD-1.47 桌面信息摆件

基于微雪 [ESP32-C6-LCD-1.47](https://www.waveshare.net/wiki/ESP32-C6-LCD-1.47) 开发板的桌面信息摆件固件:LVGL 界面显示时钟、天气、iKuai 路由器实时监控曲线,并支持 TF 卡日志记录。

## 硬件

- **主控**:ESP32-C6FH8(Wi-Fi 6 / BLE,8MB Flash)
- **屏幕**:ST7789,172×320,SPI 接口
- **板载外设**:WS2812 RGB 灯珠(GPIO8)、TF 卡槽(SPI 模式,与 LCD 共享 SPI2 总线)

## 功能

- **LVGL 桌面界面**:Wi-Fi 校时时钟 + Open-Meteo 天气 + 状态栏,背光上限 40%
- **iKuai 路由器监控**:HTTPS + Bearer token + 固定证书,1 秒轮询 CPU / 内存 / 在线数 / 实时上下行速率,ICMP ping 网关延迟,60 点滚动曲线
- **TF 卡记录**:低频发卡挂载,天气数据追加写入 `/sdcard/weather.log`;无卡/坏卡不阻塞启动
- **RGB 指示**:板载 WS2812 状态灯

## 构建

本项目使用 [PlatformIO](https://platformio.org/) + ESP-IDF 框架:

```bash
pio run            # 编译
pio run -t upload  # 烧录
pio device monitor # 串口监视
```

依赖(LVGL 等)由 `dependencies.lock` / PlatformIO 自动拉取,无需手动下载。

## 配置

首次编译前,从模板复制并填写自己的配置(这两个文件已被 `.gitignore` 排除,不会提交):

```bash
cp src/config.example.h src/config.h
cp src/ikuai_cert.example.h src/ikuai_cert.h
```

- `src/config.h`:Wi-Fi SSID/密码、iKuai 路由器地址与 token 等
- `src/ikuai_cert.h`:iKuai 路由器的 HTTPS 证书(PEM 格式)

## 目录结构

```
src/
├── main.c              # 入口
├── desktop_widget.c/h  # LVGL 桌面界面(时钟/天气/状态栏)
├── ikuai_monitor.c/h   # iKuai 路由器监控
├── lcd_driver.c/h      # ST7789 驱动
├── lv_port_disp.c/h    # LVGL 显示移植层
├── tf_card.c/h         # TF 卡挂载与日志
├── ws2812.c/h          # RGB 灯
└── fonts/              # 字体资源
```
