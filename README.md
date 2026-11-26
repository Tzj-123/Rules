# Rules

自用 Quantumult X 规则与重写合集：全软件去广告大合集、番茄小说、红果短剧去广告。内容整理自公开仓库，合并去重，重复的只留一份，自用为主。

![GitHub last commit](https://img.shields.io/github/last-commit/Tzj-123/Rules) ![GitHub commit activity](https://img.shields.io/github/commit-activity/m/Tzj-123/Rules) ![GitHub repo size](https://img.shields.io/github/repo-size/Tzj-123/Rules)

## 📢 最近更新

- 2026-11-26 新增全软件去广告合集：zqzess AdBlock + deezertidal AntiAD/ADLite + xwxiewu AdvertisingTest 三家合并去重，原始 56 万条 → 376,288 条，拆成 AdBlock-All-1~4.list，另有 AdBlock_lite 精简版
- 2026-11-26 新增 276 个 App 的单独重写（QuantumultX/rewrite/apps/），哪个 App 要去广告就单独订阅哪个
- 2026-11-26 新增番茄小说、红果短剧去广告（分流 + 重写成套）

## ⚠️ 注意

**关于番茄小说广告**

```
QuantumultX 需要重写和分流配合，即 FanQieNovel.qxrewrite 和 FanQieNovel.list，只加一个没效果
该规则同样对番茄听书有效
如果添加了没有效果，请自行排查规则是否冲突，不是规则失效
```

**关于红果短剧广告**

```
先只用基础版分流 HongGuo.list，不需要证书
不够再加进阶重写 HongGuo.qxrewrite，需要 MITM
```

**关于去广告合集**

```
AdBlock-All-1~4.list 四份要一起订阅才完整，策略统一 reject
规则量大，手机发烫 / 圈X 变慢就改用 AdBlock_lite.list，二选一，不要同时开
所有重写都要开启 MITM 并信任证书才生效
其余服务分流里的策略名是原作者的策略组名，导入时用 force-policy 或自建同名策略组
```

## 🧭 导航

> [去广告大合集（分流）](https://github.com/Tzj-123/Rules/tree/main/QuantumultX/rules)

> [按 App 单独重写（276 个）](https://github.com/Tzj-123/Rules/tree/main/QuantumultX/rewrite/apps)

> [重写合集](https://github.com/Tzj-123/Rules/tree/main/QuantumultX/rewrite)

> [细分分流片段](https://github.com/Tzj-123/Rules/tree/main/QuantumultX/snippet)

## 🛡 去广告大合集（分流）

| 文件 | 说明 |
| --- | --- |
| AdBlock-All-1.list ~ AdBlock-All-4.list | 全网去广告大合集，三家来源合并去重后 376,288 条，4 份一起订阅 |
| AdBlock_lite.list | 精简版，性能优先时用，和 All 版二选一 |

```
[filter_remote]
https://raw.githubusercontent.com/Tzj-123/Rules/main/QuantumultX/rules/AdBlock-All-1.list, tag=去广告合集1, update-interval=86400, enabled=true
https://raw.githubusercontent.com/Tzj-123/Rules/main/QuantumultX/rules/AdBlock-All-2.list, tag=去广告合集2, update-interval=86400, enabled=true
https://raw.githubusercontent.com/Tzj-123/Rules/main/QuantumultX/rules/AdBlock-All-3.list, tag=去广告合集3, update-interval=86400, enabled=true
https://raw.githubusercontent.com/Tzj-123/Rules/main/QuantumultX/rules/AdBlock-All-4.list, tag=去广告合集4, update-interval=86400, enabled=true
```

## 📱 按 App 单独重写

共 276 个 App 的单独重写，在 `QuantumultX/rewrite/apps/` 里，哪个 App 要去广告就单独订阅哪个文件，例如哔哩哔哩是 `apps/biliad.conf`。

订阅格式：

```
[rewrite_remote]
https://raw.githubusercontent.com/Tzj-123/Rules/main/QuantumultX/rewrite/apps/文件名.conf, tag=备注, enabled=true
```

同一个 App 有两个来源的（比如哔哩哔哩、YouTube），只开一个，别同时开。番茄小说的重写在 `rewrite/FanQieNovel.qxrewrite`，apps 里那份重复的没放。

## 🍅 番茄小说去广告

分流 + 重写，必须配合使用。重写需要开启 MITM 并安装信任证书，开启后先清一次番茄小说缓存。

```
[filter_remote]
https://raw.githubusercontent.com/Tzj-123/Rules/main/QuantumultX/rules/FanQieNovel.list, tag=番茄小说, update-interval=86400, enabled=true

[rewrite_remote]
https://raw.githubusercontent.com/Tzj-123/Rules/main/QuantumultX/rewrite/FanQieNovel.qxrewrite, tag=番茄小说重写, update-interval=86400, enabled=true
```

## 🎬 红果短剧去广告

- 基础版分流 `HongGuo.list`：无需 MITM，先用这个
- 进阶版重写 `HongGuo.qxrewrite`：需要 MITM，会拦截 `*.snssdk.com`，若红果打不开 / 转圈，停用重写退回基础版
- 看广告得金币 / 解锁类入口异常时，删掉分流里“埋点/上报”那一段

```
[filter_remote]
https://raw.githubusercontent.com/Tzj-123/Rules/main/QuantumultX/rules/HongGuo.list, tag=红果短剧, update-interval=86400, enabled=true

[rewrite_remote]
https://raw.githubusercontent.com/Tzj-123/Rules/main/QuantumultX/rewrite/HongGuo.qxrewrite, tag=红果短剧重写, update-interval=86400, enabled=true
```

## 🌐 其他分流

在 `QuantumultX/rules/` 里，按需订阅，订阅格式同上：

| 文件 | 说明 |
| --- | --- |
| Apple.list | 苹果服务 |
| AppleIOSUpdate.list | iOS 更新相关 |
| SystemOTA.list | 屏蔽 iOS 系统更新 |
| CMedia.list | 国内媒体 |
| GMedia.list | 国外媒体 |
| Mainland.list | 中国大陆直连 |
| Outside.list | 境外流量 |
| Microsoft.list | 微软服务 |
| Netflix.list | Netflix |
| YouTube.list | YouTube |
| ReFix.list | 规则修正 |
| WhiteList.list | 白名单（direct） |

`QuantumultX/snippet/` 里是细分分流片段：QMusicAd（QQ 音乐开屏）、ad_uni、backiee（壁纸）、baiduApp（百度系）。

## ✏️ 重写合集

`QuantumultX/rewrite/` 根目录（zqzess 系）：MyRewrite.conf、MyRewrite_lite.conf、MyAdBlock.qxrewrite、MyJsRewrite.conf、MyJsRewrite_lite.qxrewrite、Mycookie.conf、Qsearch.qxrewrite、QsearchMac.qxrewrite、baiduAd.qxrewrite、bilibili.qxrewrite、bodianMusic.conf、googleRedirect.qxrewrite、kuwo.qxrewrite、youtube.qxrewrite

`QuantumultX/rewrite/collections/`（xwxiewu 系，2022 年整理）：Rewrite-xwxiewu.txt、Js-xwxiewu.conf，较老，和上面的合集重复较多，一般不用开。

### 参考鸣谢

- [@zqzess](https://github.com/zqzess/rule_for_quantumultX)：番茄小说、AdBlock 分流、服务分流、重写合集
- [@deezertidal](https://github.com/deezertidal)：AntiAD / ADLite 分流、276 个 App 单独重写
- [@xwxiewu](https://github.com/xwxiewu)：AdvertisingTest 分流与重写合集
- [@k6nfmm7dbr-commits](https://github.com/k6nfmm7dbr-commits/hongguo-lite)：红果短剧原版（原版只有 Egern / Surge / Loon 版，此处已转成圈X格式）

### Star History

[![Star History Chart](https://api.star-history.com/svg?repos=Tzj-123/Rules&type=Date)](https://star-history.com/#Tzj-123/Rules&Date)

## 免责声明

本仓库内容整理自公开仓库，仅供自用与学习交流，规则版权归原作者所有，如有侵权请联系删除。使用后出现 App 异常请先自行排查规则冲突。
