# M HOTEL 官方网站

**建站 2026-09-11 ／ 桜華国際 ／ 对标 MIZUKA RESIDENCE 70万提案**

---

## 一、为什么品牌用「M HOTEL」而不是公司名

岳总要换掉「瑞禾」这个**公司名**，楼还是她的，只是换个法人名字。

**酒店品牌和公司名是两回事：**

| | |
|---|---|
| 公司名 | 瑞禾株式会社 → **待定新名** |
| 酒店品牌 | **M HOTEL** ← 不用改 |

M HOTEL 已经是**实物资产**：24 块门牌、丸に M 家紋，挂在楼上，是我们做的。
公司改名，门牌不用换，网站不用重做，OTA 上的名字不用改。

→ **网站现在就能做，不用等公司名定下来。**

## 二、公司名定了之后要改哪里

**只有两处**，`index.html` 里：

1. 页脚 `© 2026 M HOTEL` 那行下面，加一行「運営：〇〇株式会社」
2. JSON-LD 里加 `"parentOrganization":{"@type":"Organization","name":"〇〇株式会社"}`

改完 push 即上线。**其余一个字都不用动。**

---

## 三、对比 MIZUKA 那 70 万

| | MIZUKA 提案 | 本站 |
|---|---|---|
| 品牌归属 | **MIZUKA**（运营公司） | **M HOTEL**（岳总） |
| 域名 | 运营公司注册管理 | **注册在岳总名下** |
| 客人名单 | MIZUKA MEMBERS | **岳总自己的服务器**（民宿系统已在跑） |
| 多语言 | 5 语言 | **5 语言（日英简繁韩）已实装** |
| 直接预订 | 「对接的**设计**」 | **能用**：微信／LINE／WhatsApp／表单直通 |
| 会员 | 「扩展**设计**」 | 表单已通，数据库接民宿系统 |
| API 对接 | 「今后的**设计**」 | 静态站，无后端依赖 |
| SEO／AEO | 「SEO 基础」 | JSON-LD Hotel + ReserveAction + AI 爬虫 robots |
| 制作费 | ¥700,000 | — |
| 月费 | ¥16,000 | GitHub Pages **￥0**（域名年费另计） |

**关键差别不在价格，在第一行和第三行。**

---

## 四、技术

**纯静态**，无后端、无数据库、无构建步骤。跟 `ouka-reform` 一样 push 即部署（GitHub Pages）。

```
m-hotel/
├── index.html          单文件（HTML＋CSS＋JS＋i18n 全在内）
├── assets/
│   ├── hero.jpg        首屏（URO完成写真_01）
│   └── rooms/          room-01〜21.jpg
├── robots.txt          含 GPTBot / ClaudeBot / PerplexityBot 放行
├── sitemap.xml
└── README.md
```

### 多语言
`data-i` 属性 + JS 字典。5 语言 **56 个键，0 缺失**（已验）。
首次访问按浏览器语言自动选（zh-TW/HK→繁體，其余 zh→简体，ko→한국어，ja→日本語，其他→English），选过之后记在 localStorage。

### 直接预订
静态站没有后端，所以预订走**两条真实通道**：

1. **聊天软件直通** —— 微信／LINE／WhatsApp／邮件，四个按钮
2. **表单** —— 填完自动拼成邮件草稿（`mailto:`），主题和正文按当前语言生成

**这两条都是真的能用的**，不是「动线设计」。
以后要上真正的预订引擎（库存・支付），表单这块换掉即可，其余不动。

### 结构化数据（AEO）
`Hotel` 类型，含 `availableLanguage` 五语言、`amenityFeature`、`containsPlace`（9F）、
以及 **`potentialAction: ReserveAction`** 指向官网预订 —— 这是让 ChatGPT／Perplexity
在回答「大阪民宿推荐」时能直接给出**官网预订链接**而不是 OTA 链接的关键。

---

## 五、还没做的（需要岳总决定或提供）

| | 需要什么 |
|---|---|
| **域名** | `m-hotel.jp` 现为占位。**必须注册在岳总（新公司）名下**，不是在我这里 |
| **微信号** | 第 24 行 `ch.wechat.id` 现为占位文字，开通后填真实 ID |
| **LINE 官方账号** | 现指向 line.me 首页，开通后换成实际加友链接 |
| **邮箱** | `reservation@m-hotel.jp` 需随域名一起开通 |
| **堂ヶ芝・高津 照片** | 现用 URO 照片占位，两栋开业前要换实拍 |
| **价格** | 全站未写价格。要上会员价需先定价 |

## 六、本地预览

```bash
python3 -m http.server 8811 --directory "/Volumes/T7 Shield/OUKA-BRAIN/web/m-hotel"
```

---

**相关：** `瑞禾集团/09_民宿运营/Mizuka提案_20260911/`（对方提案书原件＋给岳总的分析）
