# loon-amap-adblock

Loon 插件：高德地图去广告（修复版）。

规则主体来自 kelee.one 的 `Amap_remove_ads`（作者 [@RuCu6](https://github.com/RuCu6)、[@kelv1n1n](https://github.com/kelv1n1n)、可莉🅥）。
原插件把「需要修改响应体」的那部分放在 `kelee.one` 域名下的 JS 上（开屏、搜索栏热词、首页资源位、我的页面等），
该域名失效后这些条目会**整块静默失效**——只靠域名不通是查不出来的。本项目把它改成**自托管**：
脚本收进本仓库，插件里所有 URL 都指向本仓库，不再依赖任何第三方域名。

## 订阅地址

主文件（Loon 3.5.1(998) 及以后，新版语法）：

```
https://raw.githubusercontent.com/Wansensr/loon-amap-adblock/main/Amap-AdBlock.plugin
```

备用（经典 Rewrite 语法，老版本 Loon 用）：

```
https://raw.githubusercontent.com/Wansensr/loon-amap-adblock/main/Amap-AdBlock-classic.plugin
```

GitHub 直连不通用 jsDelivr 镜像（有缓存，通常滞后几小时）：

```
https://cdn.jsdelivr.net/gh/Wansensr/loon-amap-adblock@main/Amap-AdBlock.plugin
```

## 添加与更新

- 添加：Loon → 配置 → 插件 → 右上角 `+` → 从 URL 添加 → 粘贴订阅地址。
- 更新：进插件详情页点右上角 ⟳。**订阅地址不变，不用删除重加。**
- 只保留这一个高德插件，不要和 kelee 的原插件同时开启。

## 版本记录

- **v1**（2026-10-13）：修复开屏广告。原插件拦截的
  `amap-aos-info-nogw.amap.com/ws/aos/alimama/` 接口已废弃（实测 GET/POST 均 404），
  高德开屏配置现在走 `m5.amap.com/ws/valueadded/alimama/splash_screen`（实测 200，服务端版本 3.2-2026-09-16），
  改为在请求阶段返回 `200 + 空 JSON`，开屏不会卡在等超时。
- **v2**（2026-10-13）：按原插件规则补齐搜索栏热词、首页资源位与运营位、我的页面、附近页、打车页、
  路线规划等推广；把原先托管在 `kelee.one` 的 `Amap_remove_ads.js` 收进本仓库自托管。

## 关于脚本

`Amap_remove_ads.js` 是 RuCu6 的 `amap.js` 镜像副本，逻辑未改动（只加了文件头说明）。
原始引用地址 `raw.githubusercontent.com/RuCu6/Loon/refs/heads/main/Scripts/amap.js` 已于 2026-10-13 核实为 404，
本副本取自 `Moli-X/Tool` 分支 `X` 的 `Loon/Plugin/Kelee/Script/Amap_remove_ads.js`（2026-03-09 版本）。

如果你的网络访问 `raw.githubusercontent.com` 不稳定，把插件里所有
`https://raw.githubusercontent.com/Wansensr/loon-amap-adblock/main/Amap_remove_ads.js`
替换成 `https://cdn.jsdelivr.net/gh/Wansensr/loon-amap-adblock@main/Amap_remove_ads.js` 即可。
