# loon-amap-adblock

Loon 插件：高德地图去广告（修复版）。

规则主体来自 kelee.one 的 `Amap_remove_ads`（作者 [@RuCu6](https://github.com/RuCu6)、[@kelv1n1n](https://github.com/kelv1n1n)、可莉🅥）。
原插件把「需要修改响应体」的那部分放在 `kelee.one` 域名下的 JS 上（开屏、搜索栏热词、首页资源位、我的页面、探索页等），
该域名失效后这些条目会**整块静默失效**。本项目把脚本收进本仓库自托管，插件里所有 URL 都指向本仓库或其 CDN 镜像。

## 订阅地址

主文件（Loon 3.5.1(998) 及以后，新版语法）：

```
https://raw.githubusercontent.com/Wansensr/loon-amap-adblock/main/Amap-AdBlock.plugin
```

备用（经典 Rewrite 语法，老版本 Loon 用）：

```
https://raw.githubusercontent.com/Wansensr/loon-amap-adblock/main/Amap-AdBlock-classic.plugin
```

`raw.githubusercontent.com` 连不上时用 jsDelivr 镜像（有缓存，可能滞后几小时）：

```
https://cdn.jsdelivr.net/gh/Wansensr/loon-amap-adblock@main/Amap-AdBlock.plugin
```

## 添加与更新

- 添加：Loon → 配置 → 插件 → 右上角 `+` → 从 URL 添加 → 粘贴订阅地址。
- 更新：进插件详情页点右上角 ⟳。**订阅地址不变，不用删除重加。**
- 判断更新有没有生效：看插件详情页「详细」里**描述那一行**，开头应该是当前版本号（现在应为 `v4 ·`）。
- 只保留这一个高德插件，不要和 kelee 的原插件同时开启。

## 版本记录

- **v4**（2026-10-13）：插件里的脚本与图标地址改用 jsDelivr（`cdn.jsdelivr.net`）。
  原因：`raw.githubusercontent.com` 在部分网络（尤其国内直连）取不到，而脚本一旦拉不到，
  「我的页面 / 首页 / 探索页 / 搜索栏热词」这些需要改响应体的条目会**整块静默失效**——
  现象就是开屏（纯规则，不需要脚本）修好了，但首页、我的、探索里的推广照旧。
  拦截项本身与 v3 **完全一致**，只是换了脚本的下载地址。
- **v3**（2026-10-13）：收敛为**与原插件逐条一致**。v2 期间我多加的 `optimus-ads.amap.com` 整域拦截已删除；
  开屏那条限定回原插件指向的 `m5.amap.com`。逐条对比结果：原插件 33 条（3 域名 + 16 改写 + 14 脚本），
  本插件 33 条（3 域名 + 17 改写 + 13 脚本），**唯一差别**是开屏从「脚本改响应体」换成「请求阶段返回空 JSON」
  —— 拦的是同一个接口，因为原插件那种写法实测已经拦不住开屏。
- **v2**（2026-10-13）：按原插件规则补齐搜索栏热词、首页资源位与运营位、我的页面、附近页、打车页、
  路线规划等推广；把原先托管在 `kelee.one` 的 `Amap_remove_ads.js` 收进本仓库自托管。
  （这一版我额外加了一条 `optimus-ads.amap.com` 整域拦截，超出原插件范围，v3 已移除。）
- **v1**（2026-10-13）：修复开屏广告。原插件拦截的
  `amap-aos-info-nogw.amap.com/ws/aos/alimama/` 接口已废弃（实测 GET/POST 均 404），
  高德开屏配置现在走 `m5.amap.com/ws/valueadded/alimama/splash_screen`（实测 200，服务端版本 3.2-2026-09-16），
  改为在请求阶段返回 `200 + 空 JSON`，开屏不会卡在等超时。

## 排查

- 描述行不是 `v4 ·` 开头 → 手机还没拉到新版：点插件详情页右上角 ⟳；仍旧不行就删掉这个插件重新从 URL 添加。
- 描述行已是 `v4 ·`、但首页/我的/探索里的推广还在 → 脚本没有执行。依次看：Loon 是否开了「脚本」、能否访问 `cdn.jsdelivr.net`。
- 别和 kelee 的原插件同时开：两个插件对同一个接口都有复写，会互相顶掉，脚本那条一旦被旧插件的死链接顶掉就等于没拦。

## 关于脚本

`Amap_remove_ads.js` 是 RuCu6 的 `amap.js` 镜像副本，逻辑未改动（只加了文件头说明）。
原始引用地址 `raw.githubusercontent.com/RuCu6/Loon/refs/heads/main/Scripts/amap.js` 已于 2026-10-13 核实为 404，
本副本取自 `Moli-X/Tool` 分支 `X` 的 `Loon/Plugin/Kelee/Script/Amap_remove_ads.js`（2026-03-09 版本）。

v4 起插件里的脚本与图标默认走 jsDelivr。如果你的网络**反而**是 `cdn.jsdelivr.net` 不通、
`raw.githubusercontent.com` 能通，把插件里所有
`https://cdn.jsdelivr.net/gh/Wansensr/loon-amap-adblock@main/` 换成
`https://raw.githubusercontent.com/Wansensr/loon-amap-adblock/main/` 即可。
