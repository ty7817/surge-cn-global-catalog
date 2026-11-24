# Surge 国内外网站 / 软件分流清单

这是一个**域名与应用目录**，不是“全互联网完整清单”。数据来自公开的 Surge 规则集快照，供排查、检索和编写分流规则使用。

## 数据概览

| 文件 | 内容 | 数量 |
|---|---|---:|
| `data/domains-cn.txt` | 国内规则集域名（China_All 去重） | 3700 |
| `data/domains-global.txt` | 国外规则集域名（主要国外服务规则集并集） | 6013 |
| `data/domains-overlap.txt` | 同时出现在国内/国外规则集的域名 | 36 |
| `data/domains-cn-exclusive.txt` | 仅国内清单 | 3664 |
| `data/domains-global-exclusive.txt` | 仅国外清单 | 5977 |
| `rules/china-all.list` | 原始 China_All 规则 | 3763 行 |
| `rules/global-all.list` | 国外域名统一为 `DOMAIN-SUFFIX` 的规则 | 6013 行 |

> 数量按“唯一域名”统计；原始规则文件可能包含 `DOMAIN`、`DOMAIN-SUFFIX`、`DOMAIN-KEYWORD`。

## 使用方式

### 1. 作为 Surge 远程规则集（公开仓库 raw）

```ini
# 国内直连
RULE-SET,https://raw.githubusercontent.com/ty7817/surge-cn-global-catalog/main/rules/china-all.list,DIRECT,no-resolve
# 国外兜底：建议换成你的主节点或对应服务组，不要无脑全塞主节点
RULE-SET,https://raw.githubusercontent.com/ty7817/surge-cn-global-catalog/main/rules/global-all.list,主节点,no-resolve
```

`global-all.list` 是“国外规则集并集”，里面包含 Apple / Microsoft / Google / 流媒体 / 游戏 / AI 等不同服务。正式使用时，最好按服务拆到对应策略组，或者只用它做检索，不要直接当成一个整体策略。

### 2. 作为目录检索

- 查某个域名属于国内还是国外清单：在 `data/domains-cn.txt` / `data/domains-global.txt` 中搜索。
- 查重叠域名：`data/domains-overlap.txt`。这些通常是国际版服务、跨国厂商的中国入口，或者规则集本身的历史重叠，需要按实际产品判断。
- App 分类说明见 `docs/`。

## 重要说明

- **不是全量互联网清单**。规则集只覆盖公开维护的常见服务，长尾站点、私有 CDN、App 内嵌 IP 连接不一定收录。
- **不含 Surge 主配置、订阅链接或任何令牌**。这个仓库只放可公开的域名/应用目录。
- **域名会变**。上线、下线、换 CDN 都会导致规则过期；建议定期从 `SOURCES.md` 的上游仓库同步。
- **国内/国外不是按公司国籍判断**。例如 Apple、Microsoft、Google 有中国入口；B 站/爱奇艺有国际版。遇到重叠域名，按“用户实际访问的站点/区域”决定直连还是代理。
- 规则集版权归上游项目所有，使用时请遵守对应仓库许可证。

## 目录

```text
data/                 国内外域名清单与重叠清单
rules/                Surge 可用的域名规则
docs/                 常用网站/软件分类说明
SOURCES.md            上游规则集地址
```
