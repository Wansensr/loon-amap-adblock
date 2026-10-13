# loon-amap-adblock

Loon 插件：高德地图去广告（修复版）。

原始规则来自 kelee.one 的 `Amap_remove_ads` 插件（作者 @RuCu6 @kelv1n1n @可莉），
并参考社区维护的同类规则（blackmatrix7 / GeQ1an / deezertidal）。
原插件的开屏拦截针对的接口已经废弃，本仓库是 2026-10-13 按实测接口重写修复的版本。

## 订阅地址

主文件（Loon 3.5.1(978) 及以后，新版 Rewrite 语法）：

```
https://raw.githubusercontent.com/Wansensr/loon-amap-adblock/main/Amap-AdBlock.plugin
```

备用（经典 Rewrite 语法，老版本 Loon 用）：

```
https://raw.githubusercontent.com/Wansensr/loon-amap-adblock/main/Amap-AdBlock-classic.plugin
```

## 添加方法

Loon → 配置 → 插件 → 右上角 `+` → 从 URL 添加 → 粘贴上面的订阅地址。

如果之前装过 kelee 的「高德地图去广告」，先把它禁用或删除，避免两套规则同时生效。

## 更新方法

仓库文件更新后，进入 Loon → 配置 → 插件 → 点进本插件 → 右上角 ⟳ 重新下载即可。

## 2026-10-13 修了什么

- 原插件把开屏广告拦在 `amap-aos-info-nogw.amap.com/ws/aos/alimama/`，实测 GET/POST 都是 404，接口已废弃
- 高德开屏配置现在走 `m5.amap.com/ws/valueadded/alimama/splash_screen`（实测 200，服务端版本 3.2-2026-09-16）
- 改为拦 `*.amap.com` 任意子域的该路径，并补齐首页推荐、搜索热词、首页资源位、消息推送、订单弹窗等推广接口
- 拦截方式从「断开连接」改为返回 `200 + 空 JSON`，开屏不会卡在等超时
- 规则已逐条脚本校验：实测到的广告接口全部命中，`restapi/mapapi` 等正常接口不受影响

装好后建议先强制退出高德再清一次缓存，否则预加载的旧广告可能还会显示一次。
