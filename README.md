# cf-free-deeplx-translate

- 一个简便的负载均衡的方式来使用翻译服务

## 部署方式

- 配置cloudflare的Work
- 把index.js的内容粘贴到cloudflare的work中
- 在cloudflare > work > 触发器,配置自定义域名就可以愉快的翻译了


## 参考deeplx使用方式或者沉浸式翻译

```Shell
curl --location 'https://freedeepl.aivvm.com/translate' \
--header 'Content-Type: application/json' \
--data '{
    "text": "hello world",
    "source_lang": "EN",
    "target_lang": "ZH"
}'
```

### 响应

```Body
{
    "alternatives": [
        "你好世界",
        "哈喽世界",
        "哈啰世界"
    ],
    "code": 200,
    "data": "哈罗世界",
    "id": 8345422279,
    "method": "Free",
    "source_lang": "EN",
    "target_lang": "ZH"
}```

我們可以從一些公開的免費的測繪空間搜索出來的資產就可以給我們帶來很多的方便的神奇用法，今天主題講講Deeplx + 測繪空間的妙用
新手閱讀理解篇
美國是最早啟動網絡空間測繪研究與應用的國家。早在2008年，為進一步加固關鍵基礎設施網絡組件，擴展主動的探測能力和快速響應、作戰能力，美國先後推出了3個重量級計劃：國土資源部（DHS）的SHINE計劃、國家安全局（NSA）的藏寶圖（TreasureMap）計劃、國防部先進研究項目局（DRAPA）的X計劃。

我國在網絡空間測繪方向也進行了相關部署和研究。公安部第一研究所設計研發的“網絡資產測繪分析系統”（簡稱網探D01），通過收集互聯網資產數據及指紋，實現網絡空間資產檢索、分析、監控，結合漏洞、廠商信息等威脅情報，開展漏洞統計分析工作，旨在為國家重點行業、部門提供全面的網絡資產安全態勢，使其更好地應對威脅關鍵信息基礎設施的網絡攻擊事件。另外，國內網絡空間測繪方面也有幾款新型的，可以識別網絡空間中包括路由器、交換機、網絡攝像頭、網絡打印機、移動設備在內的30餘種網絡終端設備。

網絡資產識別主要有設備組件識別、應用組件識別、業務類型推斷3個方面，常用的技術手段是資產指紋比對。網絡資產在協議實現、網絡應用等方面存在差異，如開放的端口/服務信息、banner信息、Web網頁數據等，對這些差異進行特徵提取可得到該資產的特徵指紋，網絡資產指紋庫積累了大量網絡資產指紋。資產指紋比對是將目標主機的特徵指紋和指紋庫進行匹配，從而實現資產屬性識別。

網絡設備組件識別首先獲取資產的網站響應頭部數據、網站文件類型、網站異常響應、服務端口、banner等數據，提取設備指紋，通過與網絡設備組件指紋庫進行指紋比對，識別目標主機的設備類型、設備廠商、設備品牌、設備型號等設備屬性。

網絡應用組件識別通過持續收集、解析目標網絡的應用組件信息，如論壇程序、博客程序等，獲取網站響應頭部數據、HTML頁面、特殊URL、開放的端口、banner等，生成應用指紋，通過比對網絡應用組件指紋庫來自動化識別目標主機的Web服務器軟件、Web腳本語言、服務類型及相應版本型號等應用屬性。

業務類型推斷是基於資產探測數據，深入融合DNS信息、漏洞庫、IP地理信息庫等資源，建立資產多層級關聯模型，推斷網絡資產的業務類型，實現網絡資產多維度畫像。業務類型推斷旨在識別重要行業的重要資產，是網絡空間深入態勢感知的核心環節。

測繪空間概念清晰了，那麼我們可以做什麼達到我們想要的服務呢？
舉例，我要搜索某個廠商的視頻監控的設備在互聯網上有多少，通過測繪空間搜索出來的資產設備可以統計IP，設備ID等等信息
而這個時候我正好發現了這個廠商的漏洞，那可以瞬間通過測繪收集到的所有設備IP進行妙用
小知識
每年網安為了搜集和堵住各種各樣的漏洞，國內已經有很完備的網絡測繪體系了，事態感知維護國內安全
美國每天都會搞很多大規模的攻擊都跟測繪空間收集資產有關，具體可以Google
測繪空間的領域得益於大數據的平台的出現而興起，因為收集大量的信息和分析需要大數據平台作為支撐，如果有興趣可以了解 ARL(Asset Reconnaissance Lighthouse)
國內外做的比較大的測繪平台
https://quake.360.net/ 89
https://fofa.info/ 67
https://Fofa.so 23
https://Wigle.net 14
https://Hunter.io 12
https://Shodan.io 10
https://Onyphe.io 7
https://Zoomeye.org 10
https://Ghostproject.fr 6
https://App.binaryedge.io 8
https://Viz.Greynoise.io/table 10
在這些網站我們可以進行搜索deeplx的端點來進行負載均衡已達到免費使用翻譯服務的目的
GitHub - OwO-Network/DeepLX: DeepL Free API (No TOKEN required) 31 我們先分析下這個github服務部署的返回的body message
{"code":200,"message":"DeepL Free API, Developed by sjlleo and missuo. Go to /translate with POST. http://github.com/OwO-Network/DeepLX"}
舉例，那麼我們打開 https://fofa.info/
 搜索以下字段【搜索body只是一種方式，其他的語法方式自己探索】
body='{"code":200,"message":"DeepL Free API, Developed by sjlleo and missuo. Go to /translate with POST. http://github.com/OwO-Network/DeepLX"}'
可以出來很多端點地址
拿到這些端點的URL地址就可以開始進行負載均衡部署一個服務，用來分攤請求deeplx的速率壓力避免429限速等

我們現在應該獲取了一些Deeplx的URL了，參考一些github的方案進行負載均衡部署一個服務來愉快的使用翻譯服務
參考部署【這個只是一個demo】：GitHub - CaoYunzhou/cf-free-deeplx: cf-free-deeplx 50
原理： 用戶請求 > 你自己部署的服務代理 > 請求互聯網公開的端點翻譯服務
分享下隨手收集的deeplx地址
https://dx.ift.lat
https://deepl.tr1ck.cn
https://translate.dftianyi.com
https://deepl.dlwlrma.xyz
https://deepl.d0zingcat.xyz
https://e.nxnow.top
https://deeplx.he-sb.top
https://deepl.aimoyu.tech
https://deepl.coloo.org
https://api.deeplx.org
https://deeplx.keyrotate.com
https://deeplx.spaceq.xyz
https://deeplx.ychinfo.com
https://deeplx.papercar.top
https://deepx.dumpit.top
https://deepl.degbug.top
https://dx-api.nosec.link
https://deepl.mukapp.top
https://deeplx.imward.dev
https://ghhosa.zzaning.com
https://deeplx.6696699.xyz
https://deeplx.zeabur.app
https://deepl.zhaosaipo.com
https://deeplx.vercel.app
https://dlx.bitjss.com
https://gpay.eu.org
https://deepl.yuwentian.com
總結：
這個只是一個拋磚引玉，網絡空間的測繪各種方法可以有各種妙用

例如我想組一個免費的chatgpt web的服務，我來收集和分析下某個開源的github公開的免費chatgpt，是不是理論可行？
假如我要搜索某個服務部署的全球站點數量
