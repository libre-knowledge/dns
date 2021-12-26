# 網域名稱系統 Domain Name System(DNS)

網域名稱系統(Domain Name System(DNS))是保存並提供第三方查詢之域名-IP 位址對應關係的分散式資料庫系統，讓使用者可以以好記的名稱而非 IP 地址訪問各種網路資源

![「檢查專案中的潛在問題」GitHub Actions 作業流程狀態標章](https://github.com/libre-knowledge/dns/actions/workflows/check-potential-problems.yml/badge.svg "本專案使用 GitHub Actions 自動化檢查專案中的潛在問題") [![pre-commit](https://img.shields.io/badge/pre--commit-enabled-brightgreen?logo=pre-commit&logoColor=white "本專案使用 pre-commit 檢查專案中的潛在問題")](https://github.com/pre-commit/pre-commit) [![REUSE 規範遵從狀態標章](https://api.reuse.software/badge/github.com/libre-knowledge/dns "本專案遵從 REUSE 規範降低軟體授權合規成本")](https://api.reuse.software/info/github.com/libre-knowledge/dns)

## 基本概念

### 網域名稱系統<br><small>Domain Name System (DNS)</small>

負責網際網路中主機名稱與 IP 地址對應的保存與查詢的階層式、非中心式的資料庫系統

### 域名空間<br><small>Name space

泛指以網域名稱系統中保存的樹狀結構域名資料

### 網域<br><small>Domain</small>

網域為域名空間樹狀結構中的一個節點，每個節點上各有一個標示著該網域名稱的名稱標籤(label)，如 `www`、`example`、`com` 分別代表一個網域

### 根網域<br><small>Root domain</small>

域名空間樹狀結構的根節點(root node)所代表的網域，以 `.` 表示

根網域位於 DNS 網域階層的第 0 層

### 域名<br><small>Domain name</small>

域名空間樹狀結構中節點的識別名稱，為將自網域節點至根網域的所有名稱標籤由左至右，以英式句點作為分隔串接在一起的名稱，如 `www.example.com.`

域名末尾的英式句點可省略

### 子網域<br><small>Subdomain</small>

指網域節點次一層的網域

以 www.example.com. 的域名為例，`example` 網域是 `com` 網域的子網域，`www` 網域是 `example` 網域的子網域

### 頂級網域<br><small>Top-level domain(TLD)</small>

域名空間樹狀結構的根節點(root node)的子節點(child node)

頂級網域位於 DNS 網域階層的第 1 層，又分為通用頂級網域(gTLD)以及國家及地區頂級域名(ccTLD)兩類別

### 通用頂級網域<br><small>Generic Top Level Domain(gTLD)</small>

最早就存在的網域類別，常見的頂級網域如 `com`、`org`、`gov` 等等

ICANN 目前允許第三方申請非典型的通用頂級網域作為註冊商標或特定興趣主題使用，如 `.cat`、`.apple`，為避免新委任(newly-delegated)的 gTLD 與內部網路管理者自己定義的 gTLD 衝突 ICANN 建議網路管理者使用已註冊的完整資格域名(FQDN)作為內部網路域名的名稱空間使用並將（如果有）自訂的 gTLD 使用移除避免造成 DNS 查詢洩漏與已註冊 gTLD 域名的訪問問題

### 國家和地區頂級網域<br><small>Country code top-level domain(ccTLD)</small>

由國家或地區專用的頂級網域類別，如 `tw`、`cn`、`jp` 等等

### 完整資格域名<br><small>Fully qualified domain name(FQDN)</small>

經過 ICANN 或其委任的域名註冊業者(registar)授權使用的域名

### DNS區域<br><small>Zone</small>

為方便管理，域名空間被劃分為多個 DNS 區域(zone)，DNS 區域涵蓋的範圍為：

* 自 DNS 區域所在網域節點到域名空間樹狀結構的葉節點(leaf node)
* 自 DNS 區域所在網域節點到下一個委任 DNS 區域的網域節點

### 名稱服務器<br><small>Name server</small>

保存 DNS 區域(zone)的資料並透過 DNS 協議回答關於該 DNS 區域的資料查詢的網路服務

### 解析器<br><small>Resolver</small>

用來查詢 DNS 資訊並將域名解析為 IP 地址的客戶端或軟體組件

### DNS 資源紀錄<br><small>Resource records(RR)</small>

與每個域名的相關聯的資料保存的形式，範例如下：

| 擁有者<br>Owner | 存活時間<br>Time To Live(TTL) | 資源紀錄類別<br>Class | 資源紀錄類型<br>Type | 資源紀錄資料<br>Data |
| :-: | :-: | :-: | :-: | :-- |
| `www.example.com.` | 86400 | IN | A | 1.2.3.4 |
| `example.com` | 86400 | IN | CNAME | `www.example.com` |

`IN` 資源紀錄類別代表「the Internet system」

`A` 資源紀錄類型代表「IPv4 協議的主機地址(host address)」

另外有下列常見的資源紀錄類型：

| DNS 資源紀錄類別 | DNS 資源紀錄類型 | 用途 | 資源紀錄資料範例 |
| :-: | :-: | :-: | :-- |
| IN | A | IPv4 協議的主機地址(host address) | `192.168.1.23` |
| IN | AAAA | 域名跟 IP 地址的對應(IPv6) | `2001:502:8cc::30` |
| IN | CNAME | 指定別名域名的正式域名 | `www.example.com` |
| IN | MX | 與郵件服務有關 | （待補） |
| IN | NS | 與名稱服務器間委任關係有關 | （待補） |
| IN | PTR | 用於域名反解 IP 地址 | （待補） |
| IN | SOA | 與權威服務器運作有關 | （待補） |
| IN | TXT | 保存任意純文字資料，可用於驗證域名的擁有權 | （待補） |

### DNS 資源紀錄集合<br><small>Resource record set(RRSet)</small>

有相同擁有者(owner)、DNS 資源紀錄類別與、DNS 資源紀錄類型的資源紀錄的集合稱為 DNS 資源紀錄集合

### DNS 區域<br><small>Zone</small>

一個單位擁有委任權限的 DNS 域名資料樹的範圍稱為 DNS 區域

### DNS 區域檔案<br><small>Zone file</small>

名稱服務器中保存 DNS 區域資料的檔案

### 權威名稱服務器<br><small>Authoritative Name Server</small>

擁有特定 DNS 區域(zone)完整資料的服務器，為了容忍服務或網路障礙 DNS 區域通常會有多個位於不同網路的權威名稱服務器

### 權威回應<br><small>Authoritative answer(AA)</small>

來自權威服務器的查詢回應稱為權威回應，其封包內的 authoritative answer 位元將被設定為 `1`

### 主要權威名稱服務器<br><small>Primary server</small>

保存並維護 DNS 區域資料的主要副本的權威名稱服務器

### 次要權威名稱服務器<br><small>Secondary server</small>

自其他權威名稱服務器接收 DNS 區域資料的權威名稱服務器

次要權威名稱服務器會定期向主要權威服務器送出重新整理查詢(refresh query)，透過判斷回應中 Start of Authority(SOA) 資源紀錄中的序號(SERIAL)欄位是否有異動來判斷 DNS 區域資料是否有被更新

一次要權威名稱服務器可同時擔任主要權威名稱服務器的角色，將區域資料傳遞給更次一級的次要權威名稱服務器

### 區域資料傳遞<br><small>Zone transfer</small>

傳送並複製 DNS 區域資料到其他權威名稱服務器的程序

### Stealth server

上層 DNS 區域的權威名稱服務器通常會有下層 DNS 區域權威服務器的 NS 資源紀錄，故意不列舉在 NS 資源紀錄中的下層權威服務器即為 stealth server，又稱為 hidden primary

### 遞迴查詢名稱服務器<br><small>Recursive name server</small>

能夠遞迴地跟授權服務器直接聯繫，為本地 DNS 客戶端進行完整的 DNS 域名解析程序的名稱服務器，由於通常會包含域名回應快取的功能又稱為快取名稱服務器(Caching name server)

### 快取名稱服務器<br><small>Caching name server</small>

遞迴查詢名稱服務器的別稱

### 域名查詢轉發<br><small>Forwarding</small>

將部份無法透過自身快取滿足的解析查詢請求轉發到其他快取名稱服務器（稱為轉發器(forwarder)）的動作

## 相關方案

### 服務實現

* ISC Berkeley Internet Name Domain(BIND) DNS 服務  
  傳統、功能強大的 DNS 服務
* dnsmasq  
  針對家庭區域網路等小型區域網路設計，資源佔用低且易於配置的 DNS/DHCP/TFTP 服務

### 輔助工具

* dig DNS 查詢工具  
  查詢 DNS 域名服務器並顯示查詢結果

## 參考資料

* [域名系統 - 維基百科，自由的百科全書](https://zh.wikipedia.org/zh-tw/%E5%9F%9F%E5%90%8D%E7%B3%BB%E7%BB%9F)
* [Domain Name System - Wikipedia](https://en.wikipedia.org/wiki/Domain_Name_System)
* [域名 - 維基百科，自由的百科全書](https://zh.wikipedia.org/wiki/%E5%9F%9F%E5%90%8D)
* [鳥哥的 Linux 私房菜 – DNS Server](http://linux.vbird.org/linux_server/0350dns.php)
* [Comparison of DNS server software - Wikipedia](https://en.wikipedia.org/wiki/Comparison_of_DNS_server_software)
* [General DNS Reference Information — BIND 9 documentation](https://bind9.readthedocs.io/en/latest/general.html#rfcs)
* [gTLD vs ccTLD 域名 有什麼不同? - Cloudmax 匯智部落格](https://blog.cloudmax.com.tw/gtld-vs-cctld/)
* [通用頂級域 - 維基百科](https://zh-yue.wikipedia.org/wiki/%E9%80%9A%E7%94%A8%E9%A0%82%E7%B4%9A%E5%9F%9F)
* [Country code top-level domain - Wikipedia](https://en.wikipedia.org/wiki/Country_code_top-level_domain)
* [存活時間 - 維基百科，自由的百科全書](https://zh.wikipedia.org/wiki/%E5%AD%98%E6%B4%BB%E6%99%82%E9%96%93)
* [Name Collision Resources & Information - ICANN](https://www.icann.org/resources/pages/name-collision-2013-12-06-en)
* [Guide to Name Collision Identification and Mitigation for IT Professionals - ICANN](https://www.icann.org/en/system/files/files/name-collision-mitigation-01aug14-en.pdf)
* [New gTLD Current Application Status](https://gtldresult.icann.org/applicationstatus/viewstatus)
* [List of Top-Level Domains - ICANN](https://www.icann.org/resources/pages/tlds-2012-02-25-en)
* [Recommended Naming Practices | Configure Host Names | Red Hat Enterprise Linux 7 | Red Hat Customer Portal](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/7/html/networking_guide/ch-Configure_Host_Names#sec-Recommended_Naming_Practices)
* [Root Server Technical Operations Association](https://root-servers.org/)
* [RFC 1034 - Domain names - concepts and facilities](https://tools.ietf.org/html/rfc1034)

---

本主題為[自由知識協作平台](https://libre-knowledge.github.io/)的一部分，除部份特別標註之經合理使用(fair use)原則使用的內容外允許公眾於授權範圍內自由使用

如有任何問題，歡迎於本主題的[議題追蹤系統](https://github.com/libre-knowledge/dns/issues)創建新議題反饋
