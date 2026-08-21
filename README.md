# 搬瓦工 KiwiVM 完全指南：面板功能怎么用？迁移机房、重装系统、API 调用全流程详解（附套餐对比与最新优惠码）

买搬瓦工的人，最终都会跟 KiwiVM 打上交道。

这不是一句废话。搬瓦工（BandwagonHost）的后台管理面板叫 KiwiVM，是他家自己开发的，全球 VPS 里基本找不到第二家。你的 VPS 开没开机、流量用了多少、要不要换机房——全在这个面板里操作。

**搬瓦工 KiwiVM 是 BandwagonHost 自主研发的 VPS 控制面板，每个 VPS 实例对应一个独立 KiwiVM 后台，提供开关机、重装系统、迁移机房、免费快照、自动备份、API 接口、在线 SSH 等管理功能。**

新手最容易卡的地方，不是不会用 VPS，而是不知道 KiwiVM 里那些英文按钮都是干什么的。这篇文章从头拆解，顺带把搬瓦工的套餐和购买流程也一起说清楚。

👉 [查看搬瓦工最新套餐与价格](https://bit.ly/bwhvps)

---

## 搬瓦工 KiwiVM 是什么？怎么登录？

KiwiVM（全称 KiwiVM Control Panel）是搬瓦工唯一的官方控制面板，外部工具用不了。你购买任何一款搬瓦工套餐之后，系统都会为那台 VPS 生成一个独立的 KiwiVM 入口，管理的是「这一台」，不是账号下所有机器的集中视图。

登录方法只有一条路：

1. 打开搬瓦工官网，右上角点 **Client Area**
2. 进入 **Services → My Services**
3. 找到你的 VPS 实例，点右边的 **Open KiwiVM** 按钮
4. 面板自动打开，无需单独输密码（从官网后台跳转的情况下）

如果你想直接用 KiwiVM 的登录地址打开，则需要设置独立的 KiwiVM 面板密码，这个密码和账号密码、VPS root 密码都是分开的三套不同密码——这个细节容易搞混。

---

## KiwiVM 三大功能模块拆解

KiwiVM 的左侧菜单分三个板块：**Admin functions**、**Migration**、**KiwiVM Extras**。逐一说。

### Admin Functions：日常管理的核心

这里是用得最多的地方，功能最杂。

**Main Controls（主控界面）**
面板首页。显示这台 VPS 的 IP 地址、SSH 端口、流量使用量、硬盘和内存占用，还有开机/关机/重启的按钮。买完 VPS 第一件事就是来这里拿 IP 和端口。

**Detailed Statistics（详细统计）**
可以查看带宽使用曲线、CPU 占用率历史、硬盘 I/O 记录。排查服务器跑慢的原因时很有用，日常不太需要盯着看。

**Root Shell（在线 SSH）**
分 Basic、Advanced、Interactive 三种。Basic 是最简单的在线命令行，Advanced 支持更多操作，Interactive 相当于网页版 VNC 终端。临时没有 SSH 客户端的时候可以救急用。

**Install New OS（重装系统）**
支持几十种 Linux 发行版，Ubuntu、Debian、CentOS 等主流版本都有。点进去选系统，确认之后几分钟完成。重装会清空数据，操作前建议先做快照。

**Two-Factor Authentication（两步验证）**
给 KiwiVM 面板本身加二次验证，需要配合 Google Authenticator 或 Authy 等 APP 使用。账号安全意识强的用户建议开。

**Root Password Modification（重置 root 密码）**
忘记 VPS 登录密码的时候，直接在这里重置生成新密码，然后用新密码 SSH 登录即可。

**Audit Log（审计日志）**
记录所有对这台 VPS 的操作：登录时间、开关机、API 调用记录等。发现账号有异常操作时，来这里查。

**API（接口密钥）**
显示这台 VPS 的 VEID（7位数字）和 API KEY。有了这两个值，可以用代码调用搬瓦工的 API 接口，实现自动重启、查看状态、批量创建快照等操作。不懂编程的话这个功能基本用不上，但别把 API KEY 泄露出去。

---

### Migration：迁移机房

这个模块只有一个功能——**Migrate to another DC（迁移到另一个机房）**。

搬瓦工最有特色的点之一就是多机房套餐。买了支持迁移的套餐（比如 CN2 GIA-E），就可以在十几个机房之间来回切换，不限次数，不用重新买。

操作步骤：
1. 进入 KiwiVM，左侧点 **Migrate to another DC**
2. 下拉菜单选择目标机房
3. 点 **Confirm on next step** 确认
4. 等待迁移完成（通常几分钟），IP 地址会变，记得更新 SSH 配置

注意：每次迁移会消耗一部分流量（双向传输数据），不是完全免费，但通常消耗量不大。

不同套餐可选的机房数量不同。KVM 套餐可迁到约 8 个机房，CN2 GIA-E 套餐可迁到 12 个以上机房，包括 DC6 CN2 GIA-E、DC9 CN2 GIA、日本大阪软银、荷兰联通 EUNL_9 等优质线路。

👉 [选购支持多机房迁移的搬瓦工套餐](https://bit.ly/bwhvps)

---

### KiwiVM Extras：附加功能

**Snapshots（快照）**
免费创建 VPS 快照，记录某一时刻的全量状态（系统、数据、配置）。日后可以从快照恢复。搬瓦工提供「永久快照（Sticky）」，不会过期。强烈建议在以下两个时间点做快照：装完环境之后、做重大变更之前。

**Backups（自动备份）**
系统会每隔一段周期自动全量备份你的 VPS，免费。备份可以导入到快照功能里进行恢复。这个是被动保护，不能替代主动备份策略。

**Private Network（私有网络）**
同一机房下的两台 VPS 可以组建内网，内网传输免流量计算。有多台 VPS 需要内部通信的场景会用到。

---

## KiwiVM API：适合开发者的进阶玩法

搬瓦工的 API 接口挂在 `api.64clouds.com/v1/` 下面。有了 VEID 和 API KEY，可以发 GET 或 POST 请求实现各种操作：查看 VPS 信息、开关机、重启、创建快照、迁移机房等。

调用示例（查看 VPS 信息）：


https://api.64clouds.com/v1/getServiceInfo?veid=你的VEID&api_key=你的API_KEY


PHP、Python、Shell 脚本都能调用，逻辑就是发一个 GET 请求拿回 JSON 结果。基于这个 API，一些用户开发了非官方的手机 APP 来管理搬瓦工 VPS，比如 Bandwagon 控制台、瓦工助手等。

注意：VEID 和 API KEY 权限很高，不要发给不信任的人，也不要写进公开的代码仓库。

---

## 搬瓦工全套餐对比表

搬瓦工官网的套餐分四个系列。下面是所有在售常规套餐的完整对比：

| 套餐系列 | 内存 | 硬盘 | 月流量 | 带宽 | 价格 | 可选机房 | 购买链接 |
| --- | --- | --- | --- | --- | --- | --- | --- |
| KVM 入门版 20G | 1GB | 20GB SSD | 1TB | 1Gbps | $49.99/年 | DC8 CN2 等约8个 | [购买此方案](https://bwh81.net/aff.php?aff=80104&pid=57) |
| KVM 入门版 40G | 2GB | 40GB SSD | 2TB | 1Gbps | $99.99/年 | DC8 CN2 等约8个 | [购买此方案](https://bwh81.net/aff.php?aff=80104&pid=58) |
| CN2 GIA-E 20G | 1GB | 20GB SSD | 1TB | 2.5Gbps | $169.99/年 / $49.99/季 | DC6/DC9/软银/EUNL_9 等12+个 | [购买此方案](https://bwh81.net/aff.php?aff=80104&pid=87) |
| CN2 GIA-E 40G | 2GB | 40GB SSD | 2TB | 2.5Gbps | $299.99/年 / $89.99/季 | DC6/DC9/软银/EUNL_9 等12+个 | [购买此方案](https://bwh81.net/aff.php?aff=80104&pid=88) |
| 香港 CN2 GIA 500G流量 | 1GB | 20GB SSD | 500GB | 1Gbps | $899.99/年 / $89.99/月 | 香港 HK85/HK | [购买此方案](https://bwh81.net/aff.php?aff=80104&pid=94) |
| 香港 CN2 GIA 1T流量 | 2GB | 40GB SSD | 1TB | 1Gbps | $1559.99/年 / $155.99/月 | 香港 HK85/HK | [购买此方案](https://bwh81.net/aff.php?aff=80104&pid=95) |

> 当前最新优惠码：**BWHCGLUKKB**，可减 6.77%，循环有效（续费同样有效）。购买时在结算页的 Promotional Code 栏填入即可。$49.99/年用完优惠码实付约 **$46.70**。

对大多数人来说，CN2 GIA-E 套餐是性价比最高的档位。根据多个中文社区的用户反馈，DC6 CN2 GIA-E 机房的三网延迟普遍在 150ms 以下，丢包率极低，建站和日常使用体验显著优于 KVM 入门套餐。

---

## 搬瓦工购买全流程

用支付宝就能付款，中国用户不用绑信用卡。

1. 打开搬瓦工官网，找到你想买的套餐，点 **Order Now**
2. 选择计费周期（年付最划算），选择机房（不确定就先选 DC6 CN2 GIA-E）
3. 点 **Add to Cart**
4. 在结算页找到 **Promotional Code** 填入优惠码 BWHCGLUKKB，点 Validate Code
5. 点 **Checkout**，注册或登录账户，填写账户信息（国家要填真实）
6. 支付方式选 **Alipay**（支付宝），扫码完成支付
7. 邮件会发来 VPS 信息，然后去 Services → My Services 打开 KiwiVM 面板

注意：填写账户信息时，国家一定要填真实，搬瓦工风控系统会比对 IP 归属地，信息差异大可能导致订单被取消。

👉 [立即前往搬瓦工选购最适合的套餐](https://bit.ly/bwhvps)

---

## 搬瓦工退款政策

搬瓦工支持新购账户 30 天内无理由全额退款，满足一定条件（包括未超额使用流量等）可以直接在账户后台发起申请，系统自动处理。这对于不确定 VPS 性能是否满足需求的新用户来说，相当于一个零风险的试用期。

根据搬瓦工官方知识库的说明，退款到账时间根据支付方式而有所不同。支付宝退款通常在申请通过后的几个工作日内处理完毕。

---

## FAQ：搬瓦工 KiwiVM 常见问题

**Q：KiwiVM 面板打不开，怎么办？**
A：最常见的原因是 kiwivm.64clouds.com 这个域名在部分网络环境下被干扰。建议换一个网络环境，或者关掉代理重试。实在访问不了，可以在搬瓦工账号后台通过 Client Area → My Services 跳转，这个路径不走 kiwivm.64clouds.com 的直接访问。

**Q：迁移机房之后 IP 变了，原来的 IP 还能用吗？**
A：不能。迁移机房后 IP 会重新分配，原 IP 作废。如果原 IP 被封，迁机房换 IP 是解决方案之一。

**Q：搬瓦工支持免费换 IP 吗？**
A：KiwiVM 里有换 IP 功能，但免费次数有限，超出后需要付费。如果 IP 被封，迁机房换 IP 是零成本的方式。

**Q：优惠码 BWHCGLUKKB 续费也有效吗？**
A：有效。搬瓦工的优惠码是循环有效的，用优惠码购买之后，每次续费都按折扣价计算，不只是首次。

**Q：KVM 套餐和 CN2 GIA-E 套餐的机房区别是什么？**
A：KVM 套餐走的是 CN2 GT 普通线路，可用机房约 8 个；CN2 GIA-E 套餐走 CN2 GIA 高端线路，可用机房 12 个以上，包括 DC6 CN2 GIA-E、DC9 CN2 GIA、日本大阪软银等速度更快的机房，到国内的延迟和丢包表现明显更好。

**Q：搬瓦工 KiwiVM 有中文版吗？**
A：没有。官方 KiwiVM 一直是纯英文界面，多年来没有推出中文版，需要自行对照翻译使用。本文表格中已列出主要功能的中文对照。

---

## 总结

搬瓦工 KiwiVM 的功能密度挺高，不过结构清晰，摸熟了之后操作很顺手。

新手最常用的三个操作：拿 IP 和 SSH 端口（Main Controls）、换机房（Migrate to another DC）、重装系统（Install New OS）。其余功能按需用就行，不必全部搞懂。

套餐上，有选择困难症的话直接选 CN2 GIA-E 季付 $49.99，用优惠码 BWHCGLUKKB 折下来约 $46.59/季。选完之后在 KiwiVM 里测一下各个机房，哪个延迟低就迁过去，这就是搬瓦工最有价值的用法。

👉 [前往搬瓦工获取最新套餐与折扣](https://bit.ly/bwhvps)
