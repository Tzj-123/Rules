# Quantumult X 规则

仓库地址：https://github.com/Tzj-123/Rules

## 全软件去广告合集（2026-11-26 追加）

### 分流
- **AdBlock-All-1.list ~ AdBlock-All-4.list**（QuantumultX/rules/）：全网去广告大合集，已合并去重，重复的只留一份。
  来源：zqzess AdBlock + deezertidal AntiAD/ADLite + xwxiewu AdvertisingTest，原始 56 万条去重后 376,288 条，策略统一 reject。
  文件太大拆成了 4 份，4 份要一起订阅才完整。规则量大，手机发烫/圈X变慢就改用下面这个精简版。
- **AdBlock_lite.list**：精简版去广告分流，性能优先时用它（和 All 二选一，不要同时开）。
- 其余分流（zqzess 系，策略名是作者的策略组名，导入时用 force-policy 或自己建同名策略组）：
  Apple.list、AppleIOSUpdate.list、CMedia.list、GMedia.list、Mainland.list、Microsoft.list、Netflix.list、Outside.list、ReFix.list、YouTube.list、WhiteList.list（白名单 direct）、SystemOTA.list（屏蔽 iOS 更新）
- snippet/ 里是细分分流片段：QMusicAd（QQ音乐开屏）、ad_uni、backiee（壁纸）、baiduApp（百度系）

订阅示例：
```
[filter_remote]
https://raw.githubusercontent.com/Tzj-123/Rules/main/QuantumultX/rules/AdBlock-All-1.list, tag=去广告合集1, update-interval=86400, enabled=true
https://raw.githubusercontent.com/Tzj-123/Rules/main/QuantumultX/rules/AdBlock-All-2.list, tag=去广告合集2, update-interval=86400, enabled=true
https://raw.githubusercontent.com/Tzj-123/Rules/main/QuantumultX/rules/AdBlock-All-3.list, tag=去广告合集3, update-interval=86400, enabled=true
https://raw.githubusercontent.com/Tzj-123/Rules/main/QuantumultX/rules/AdBlock-All-4.list, tag=去广告合集4, update-interval=86400, enabled=true
```

### 重写（按 App 分开，在 QuantumultX/rewrite/apps/）
- 共 276 个 App 的单独重写（来源 deezertidal/QuantumultX-Rewrite，2026-11 还在更新），哪个 App 要去广告就单独订阅哪个文件，例如哔哩哔哩是 apps/biliad.conf、网易云没有单独文件可用下面的合集。
- 订阅格式：`https://raw.githubusercontent.com/Tzj-123/Rules/main/QuantumultX/rewrite/apps/文件名.conf, tag=备注, enabled=true`
- 同一个 App 有两个来源的（比如哔哩哔哩、YouTube），只开一个，别同时开。
- 番茄小说的重写已经在 rewrite/FanQieNovel.qxrewrite 里了，apps 里那份重复的没放。

### 重写合集（rewrite/ 根目录，zqzess 系）
MyRewrite.conf、MyRewrite_lite.conf、MyAdBlock.qxrewrite、MyJsRewrite.conf、MyJsRewrite_lite.qxrewrite、Mycookie.conf、Qsearch.qxrewrite、QsearchMac.qxrewrite、baiduAd.qxrewrite、bilibili.qxrewrite、bodianMusic.conf、googleRedirect.qxrewrite、kuwo.qxrewrite、youtube.qxrewrite
### 重写合集（rewrite/collections/，xwxiewu 系，2022 年整理）
Rewrite-xwxiewu.txt、Js-xwxiewu.conf（较老，和上面的合集重复较多，一般不用开）

重写都要开 MITM 并信任证书才生效。

## 番茄小说去广告（分流 + 重写，必须配合使用）
- 分流：QuantumultX/rules/FanQieNovel.list
- 重写：QuantumultX/rewrite/FanQieNovel.qxrewrite
- 来源：zqzess/rule_for_quantumultX

```
[filter_remote]
https://raw.githubusercontent.com/Tzj-123/Rules/main/QuantumultX/rules/FanQieNovel.list, tag=番茄小说, update-interval=86400, enabled=true

[rewrite_remote]
https://raw.githubusercontent.com/Tzj-123/Rules/main/QuantumultX/rewrite/FanQieNovel.qxrewrite, tag=番茄小说重写, update-interval=86400, enabled=true
```
重写需要开启 MITM 并安装信任证书，开启后先清一次番茄小说缓存。

## 红果短剧去广告
- 分流（基础版，无需 MITM）：QuantumultX/rules/HongGuo.list
- 重写（进阶版，需要 MITM）：QuantumultX/rewrite/HongGuo.qxrewrite
- 来源：k6nfmm7dbr-commits/hongguo-lite（MIT），原版只有 Egern/Surge/Loon 版，此处已转成圈X格式

```
[filter_remote]
https://raw.githubusercontent.com/Tzj-123/Rules/main/QuantumultX/rules/HongGuo.list, tag=红果短剧, update-interval=86400, enabled=true

[rewrite_remote]
https://raw.githubusercontent.com/Tzj-123/Rules/main/QuantumultX/rewrite/HongGuo.qxrewrite, tag=红果短剧重写, update-interval=86400, enabled=true
```
先只用基础版分流；不够再加进阶重写。
进阶重写会 MITM *.snssdk.com，若红果打不开/转圈，停用重写退回基础版。
看广告得金币/解锁类入口异常时，删掉分流里“埋点/上报”那一段。
