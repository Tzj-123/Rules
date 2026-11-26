# Quantumult X 规则

仓库地址：https://github.com/Tzj-123/Rules

## 番茄小说去广告（分流 + 重写，必须配合使用）
- 分流：QuantumultX/rules/FanQieNovel.list
- 重写：QuantumultX/rewrite/FanQieNovel.qxrewrite
- 来源：zqzess/rule_for_quantumultX

圈X 配置里加：
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

圈X 配置里加：
```
[filter_remote]
https://raw.githubusercontent.com/Tzj-123/Rules/main/QuantumultX/rules/HongGuo.list, tag=红果短剧, update-interval=86400, enabled=true

[rewrite_remote]
https://raw.githubusercontent.com/Tzj-123/Rules/main/QuantumultX/rewrite/HongGuo.qxrewrite, tag=红果短剧重写, update-interval=86400, enabled=true
```
先只用基础版分流；不够再加进阶重写。
进阶重写会 MITM *.snssdk.com，若红果打不开/转圈，停用重写退回基础版。
分流规则要排在 snssdk.com / zijieapi.com 宽泛直连规则之前。
看广告得金币/解锁类入口异常时，删掉分流里“埋点/上报”那一段。
