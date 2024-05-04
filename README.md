## 规则文件地址及使用方式

### 在线地址（URL）

> 如果无法访问域名 `raw.githubusercontent.com`，可以使用第二个地址（`cdn.jsdelivr.net`），但是内容更新会有 12 小时的延迟。以下地址填写在 Clash 配置文件里的 `rule-providers` 里的 `url` 配置项中。

- **直连域名列表 direct.txt**：
  - [https://raw.githubusercontent.com/Loyalsoldier/clash-rules/release/direct.txt](https://raw.githubusercontent.com/Loyalsoldier/clash-rules/release/direct.txt)
  - [https://cdn.jsdelivr.net/gh/Loyalsoldier/clash-rules@release/direct.txt](https://cdn.jsdelivr.net/gh/Loyalsoldier/clash-rules@release/direct.txt)
- **代理域名列表 proxy.txt**：
  - [https://raw.githubusercontent.com/Loyalsoldier/clash-rules/release/proxy.txt](https://raw.githubusercontent.com/Loyalsoldier/clash-rules/release/proxy.txt)
  - [https://cdn.jsdelivr.net/gh/Loyalsoldier/clash-rules@release/proxy.txt](https://cdn.jsdelivr.net/gh/Loyalsoldier/clash-rules@release/proxy.txt)
- **Telegram 使用的 IP 地址列表 telegramcidr.txt**：
  - [https://raw.githubusercontent.com/Loyalsoldier/clash-rules/release/telegramcidr.txt](https://raw.githubusercontent.com/Loyalsoldier/clash-rules/release/telegramcidr.txt)
  - [https://cdn.jsdelivr.net/gh/Loyalsoldier/clash-rules@release/telegramcidr.txt](https://cdn.jsdelivr.net/gh/Loyalsoldier/clash-rules@release/telegramcidr.txt)
- **局域网 IP 及保留 IP 地址列表 lancidr.txt**：
  - [https://raw.githubusercontent.com/Loyalsoldier/clash-rules/release/lancidr.txt](https://raw.githubusercontent.com/Loyalsoldier/clash-rules/release/lancidr.txt)
  - [https://cdn.jsdelivr.net/gh/Loyalsoldier/clash-rules@release/lancidr.txt](https://cdn.jsdelivr.net/gh/Loyalsoldier/clash-rules@release/lancidr.txt)
- **中国大陆 IP 地址列表 cncidr.txt**：
  - [https://raw.githubusercontent.com/Loyalsoldier/clash-rules/release/cncidr.txt](https://raw.githubusercontent.com/Loyalsoldier/clash-rules/release/cncidr.txt)
  - [https://cdn.jsdelivr.net/gh/Loyalsoldier/clash-rules@release/cncidr.txt](https://cdn.jsdelivr.net/gh/Loyalsoldier/clash-rules@release/cncidr.txt)


### 使用方式

关于 Clash Premium 使用方式，请查看[官方文档](https://github.com/Dreamacro/clash/wiki/Clash-Premium-Features) 或 [Lancellc's GitBook](https://lancellc.gitbook.io/clash/)。

要想使用本项目的规则集，只需要在 Clash 配置文件中添加如下 `rule-providers` 和 `rules`。

#### Rule Providers 配置方式

```yaml
  Myrejetct:
    type: http
    behavior: domain
    url: https://anti-ad.net/clash.yaml
    path: ./ruleset/Myrejetct.yaml
    interval: 259200
  cncidr:
    type: http
    behavior: ipcidr
    url: https://raw.githubusercontent.com/kurdsvv/rules/master/Clash-Rule/cncidr.yaml
    path: ./ruleset/cncidr.yaml
    interval: 259200
  allcnip:
    type: http
    behavior: ipcidr
    url: https://raw.githubusercontent.com/kurdsvv/rules/master/Clash-Rule/all_cn_cidr.txt
    path: ./ruleset/allcnip.yaml
    interval: 259200

  proxy:
    type: http
    behavior: domain
    url: https://raw.githubusercontent.com/kurdsvv/rules/master/Clash-Rule/proxy.txt
    path: ./ruleset/proxy.yaml
    interval: 259200
  direct:
    type: http
    behavior: domain
    url: https://raw.githubusercontent.com/kurdsvv/rules/master/Clash-Rule/direct.txt
    path: ./ruleset/direct.yaml
    interval: 259200
  cfdomain:
    type: http
    behavior: domain
    url: https://raw.githubusercontent.com/kurdsvv/rules/master/Clash-Rule/cf-domain.txt
    path: ./ruleset/cfdomain.yaml
    interval: 259200
    
  openai:
    type: http
    behavior: domain
    url: https://raw.githubusercontent.com/kurdsvv/rules/master/Clash-Rule/openai.txt
    path: ./ruleset/openai.yaml
    interval: 259200    

  lancidr:
    type: http
    behavior: ipcidr
    url: https://raw.githubusercontent.com/kurdsvv/rules/master/Clash-Rule/lancidr.txt
    path: ./ruleset/lancidr.yaml
    interval: 259200
  telegramcidr:
    type: http
    behavior: ipcidr
    url: https://raw.githubusercontent.com/kurdsvv/rules/master/Clash-Rule/telegramcidr.txt
    path: ./ruleset/telegramcidr.yaml
    interval: 259200
  private:
    type: http
    behavior: domain
    url: https://raw.githubusercontent.com/kurdsvv/rules/master/Clash-Rule/private.txt
    path: ./ruleset/private.yaml
    interval: 259200
  reject:
    type: http
    behavior: domain
    url: https://raw.githubusercontent.com/kurdsvv/rules/master/Clash-Rule/Reject.txt
    path: ./ruleset/reject.yaml
    interval: 259200
  Cloudflare:
    type: http
    behavior: ipcidr
    url: https://raw.githubusercontent.com/kurdsvv/rules/master/Clash-Rule/Cloudflare.txt
    path: ./ruleset/Cloudflare.yaml
    interval: 259200
  Google:
    type: http
    behavior: ipcidr
    url: https://raw.githubusercontent.com/kurdsvv/rules/master/Clash-Rule/Google.txt
    path: ./ruleset/Google.yaml
    interval: 259200
  applications:
    type: http
    behavior: classical
    url: https://raw.githubusercontent.com/kurdsvv/rules/master/Clash-Rule/applications.txt
    path: ./ruleset/applications.yaml
    interval: 259200


```

#### 黑名单模式 Rules 配置方式（推荐）

- 白名单模式，意为「**没有命中规则的网络流量，统统使用代理**」，适用于服务器线路网络质量稳定、快速，不缺服务器流量的用户。
- 以下配置中，除了 `DIRECT` 和 `REJECT` 是默认存在于 Clash 中的 policy（路由策略/流量处理策略），其余均为自定义 policy，对应配置文件中 `proxies` 或 `proxy-groups` 中的 `name`。如你直接使用下面的 `rules` 规则，则需要在 `proxies` 或 `proxy-groups` 中手动配置一个 `name` 为 `PROXY` 的 policy。
- 如你希望 Apple、iCloud 和 Google 列表中的域名使用代理，则把 policy 由 `DIRECT` 改为 `PROXY`，以此类推，举一反三。
- 如你不希望进行 DNS 解析，可在 `GEOIP` 规则的最后加上 `,no-resolve`，如 `GEOIP,CN,DIRECT,no-resolve`。

```yaml
rules:
  #- RULE-SET,Myrejetct,REJECT
  - RULE-SET,cfdomain,Cloudafare-conn
  - RULE-SET,proxy,🚀 节点选择
  #- RULE-SET,openai,ChatGPT
  - RULE-SET,telegramcidr,🌈 Telegram
  - RULE-SET,direct,DIRECT
  - RULE-SET,cncidr,DIRECT
  #- RULE-SET,allcnip,DIRECT
  - RULE-SET,Google,🚀 节点选择
  - RULE-SET,Cloudflare,Cloudafare-conn
  - RULE-SET,private,♻️ 自动选择
  - RULE-SET,lancidr,DIRECT
  - MATCH,MATCH

```


