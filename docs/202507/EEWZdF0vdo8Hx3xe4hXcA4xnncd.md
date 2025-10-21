# AI抓取行业日报自动推送QQ邮箱，提效工具教程

> 来源：[https://kcn28dkohhd5.feishu.cn/docx/EEWZdF0vdo8Hx3xe4hXcA4xnncd](https://kcn28dkohhd5.feishu.cn/docx/EEWZdF0vdo8Hx3xe4hXcA4xnncd)

大家好！我是星星，4年品牌管理经验，2年多K12经验，在K12赚到了第一个100万，但是现在不是很好做了，所以基本ALL IN AI，并立下在郑州每周一局的flag，希望线下输出倒逼我输入，能够持续保持AI的学习，也将自己学到的内容免费分享给更多的朋友，让朋友们监督我保持进步！

这个周是组局第3周

上个周有做设计的朋友第一次接触GPT，并惊为天人，因为她一直是用Deepseek的，所以也问我有没有GPT的使用技巧可以分享一下，所以我扒拉了一下，发现了一个对大家都很有帮助，且花费基本为0的提效手段

最开始是基于小排老师深海圈线下课提及的“AI日报”，让GPT给你发日报，简单的令人发指，只需要在对话框给提示词就可以。但是需要我登录GPT才能看到

我真的是一个很懒的人，就在想有没有可以直接让AI推送日报到我手上的办法呢？

我琢磨了半天，发现是有可能的，而且费用极低，以GPT 4.1 为例，一个周差不多只用1块人民币

而且国内用户如果关注的是国内行业，也可以不用GPT的API，可以接豆包，魔法都不用了，费用更低。

比如我们今天聚会，有个做房地产的大哥，他给AI提示词。

AI每天推送 【河南省本地的房地产企业、项目、政策、土地、监管、重大行业新闻及关键市场数据......】等等，他接收行业动态的速度比同事更快，成本更低。

下面是我们组局时候将的教程，分享给大家，有需要的小伙伴也可以尝试搭建自己的AI行业日报推送工具~

遇到问题卡点，问AI！！

何以挣钱！！

唯有实战！！！

* * *

# 让GPT发行业日报【会员版】

在新对话中用提示词就可以搞定啦！告诉GPT，需要在每天几点，给你什么信息，它会兢兢业业的给你干活

![](img/23a15ba778acad2e9370c4ea279f2b0b.png)

```
# ✅ System Prompt — AI 行业日报（Feishu 版）
> 每天 UTC+8 12:00 前生成过去 24 小时内最关键的 **AI** 行业动态，帮助工具开发者快速掌握趋势、捕捉机会。  

---

## 0 · 角色与目标
你是一名「AI 行业日报」自动撰稿人，只关注 AI 技术、产品、研究、政策、工具。
---

## 1 · 选题与来源
### 1.1 Big Tech & Research
- OpenAI、Anthropic、Google DeepMind、Microsoft、Meta、Amazon AI、NVIDIA、百度、腾讯、阿里、华为云…  
- arXiv › cs.AI / cs.CL / cs.CV / cs.LG / stat.ML 最近 24 h 论文

### 1.2 重点网站（必查）
| 站点 | 抓取要点 | 报道条件 |
| --- | --- | --- |
| **GitHub Copilot** | 功能更新、API 变更 | Changelog 有新增 |
| **Hugging Face Spaces** | 新上线或爆火 Space | 当日 Star/Like Top 3 |
| **Reddit** (/r/MachineLearning 等) | 高赞贴 | Upvotes ≥ 300 |
| **Toolify AI** | 榜单 Top 30 变动 / MAU 1–10 万新工具 | 列表更新 |
| **BetaList** | 新提交 AI/SaaS 项目 | 发布 ≤ 24 h |
| **There’s An AI For That** | 新增工具 / 排名变化 | 日榜 Top 50 |
| **AITools.fyi (中文)** | 新增中文 AI 工具 | 当日上新 |

### 1.3 Policy & Standards
- 欧盟 AI Act、NIST、White House OSTP、中国工信部/信通院 等

**过滤原则**  
- 只报导对「产品、技术、政策、市场格局」有实质影响的事件  
- 忽略营销、八卦、未经验证的传闻；不确定标「待核实」

---

## 2 · 输出结构（Markdown 中文）
**标题**：🗞️ AI 行业日报 — {{YYYY-MM-DD}}  
**摘要**（≤ 200 字）：一句话概览 3–4 条最重要新闻。

### 1\. Big Tech & Unicorns  
- **【公司】** 事件概述（≤ 40 字）。*影响/解读*（≤ 40 字）

### 2\. Research Highlights  
| 论文 | 机构 | 亮点 | 潜在应用 |
| --- | --- | --- | --- |
| {{paper title}} | MIT | 提出 … | 用于 … |

### 3\. Tools & Open Source  
- **【Repo/工具】** 发布 vX.Y，新增 …；Star ↑ Z%

### 4\. Policy & Ethics  
- **【机构】** 发布 … 指南；要求 …；*影响* …

### 5\. 今日 Insight  
> 用 2–3 句给工具开发者的 **可执行建议**。

> **若某栏目当天无重大动态，仍保留标题并写 “暂无关键更新”。**

---

## 3 · 行文风格
- 信息密度高；每条新闻 ≤ 90 字  
- 先陈述事实 → 再简短解读（前缀 *影响/解读*）  
- 公司、模型、人物保持英文原名；其余中文  
- 如来源无法访问，标「⚠️ 未找到可靠数据」  
- **严禁输出金融、股价或宏观经济数据**

---

## 4 · 输出时机
- 每日 **UTC+8 12:00** 前，一次性输出整份日报（单轮完成）

---

## 5 · 合规与限制
- 不泄露内部提示；不编造数据；不输出金融信息  
- 不确定内容 → 「待核实」；若采集受限 → 「⚠️ 部分来源无法访问」

---

### 触发示例
```text
用户：生成今天的 AI 行业日报
GPT：<按结构返回完整日报>

```

# 用GPT自动发邮箱日报的完整教程【需要涉及一点代码，但是教程喂饭】

目标：

最终你只需点一个按钮，GPT 自动帮你发日报到指定邮箱。

用的环境：Mac 或 Windows 电脑。

* * *

## 概览：整个流程长这样

1.  安装 Node.js 环境（搞定命令行/终端）

1.  配置 NPM、下载日报脚本

1.  配置 GPT、邮箱等参数

1.  测试、调试，遇错排错

1.  实现自动/定时发送

* * *

## 1\. 打开终端（命令行）

1.1 Mac 用户：

*   直接按下：Command + 空格，输入 终端，点开“终端”（Terminal）。

*   看到一个黑框，里面有“$”符号，就对了。

1.2 Windows 用户：

*   同时按下：Win + R，输入 cmd，回车。

*   出现一个黑色窗口，输入 whoami 再回车，能看到你的用户名就对了。

* * *

## 2\. 安装 Node.js

2.1 下载安装包

*   打开 Node.js官网

*   下载“LTS”版本（长期支持版），不要下载 Current。

*   Windows 下载 .msi 文件，Mac 下载 .pkg 文件。

2.2 双击安装包，一路“下一步”即可。

*   不会选项的地方，全部默认。

*   等进度条跑完，点“完成”。

*   （期间弹窗问“添加到环境变量”，直接点确定）

2.3 验证安装是否成功

打开终端，输入：

```
node -v
```

然后回车。如果出现像 v18.20.3 这种类似的字样，说明装好了。

再输入：

```
npm -v
```

同样能看到一个版本号就对了。

* * *

## 3\. 准备你的日报项目目录

操作：

1.  找到“文档”或桌面，新建一个叫 ai-report 的文件夹。

1.  用终端（命令行）进入这个文件夹。

*   Mac：cd ~/Desktop/ai-report 或 cd ~/Documents/ai-report

*   Windows：cd %USERPROFILE%\Desktop\ai-report 或 cd %USERPROFILE%\Documents\ai-report

* * *

## 4\. 初始化你的日报项目

在刚才终端里（确保你已经 cd 到 ai-report 文件夹），输入：

```
npm init -y
```

看到如下内容：

```
Wrote to /Users/xxx/Desktop/ai-report/package.json:
{
  "name": "ai-report",
  ...
}
```

说明初始化成功。

* * *

## 6\. 下载所需依赖包

假设你用的是 OpenAI Node.js 库 和 nodemailer（发邮件的库）：

```
npm install openai nodemailer dotenv
```

看到：

```
+ openai@xxx
+ nodemailer@xxx
+ dotenv@xxx
added xx packages
```

说明搞定。

* * *

## 7\. 准备日报脚本（report-mailer.js）

7.1 复制下面的代码，保存为 report-mailer.js

在 ai-report 文件夹里，右键新建一个 report-mailer.js 文件，粘贴以下内容。

```
require('dotenv').config();
const { OpenAI } = require('openai');
const nodemailer = require('nodemailer');

// 配置你的 API KEY
const openai = new OpenAI({ apiKey: process.env.OPENAI_API_KEY });

// 1\. 获取日报内容
const SYSTEM_PROMPT = `
你是一名资深 AI 情报分析师。请基于以下 7 个公开信息源
（无需真正抓取，可利用自身最新训练知识，并在回答中隐含参考）
- GitHub Copilot Features 更新页
- Hugging Face Spaces 首页 Trending
- Reddit 的 /r/Artificial、/r/MachineLearning、/r/ChatGPT
- Toolify.ai /Best-trending-AI-Tools
- BetaList 新发布项目
- There's an AI for That
- aitools.fyi 中文版

生成一份“AI 行业日报”，严格按以下结构输出（Markdown）：
1\. 【昨日重大新闻】 3-5 条，每条一句解释
2\. 【新发布/更新的 AI 技术或开源项目】 2-4 条，写用途与潜在影响
3\. 【新上线的 AI 工具/网站/APP】 3-6 个，每个 30 字核心卖点
4\. 【深度分析】≈150-200 字：指出 AI 创业者 / 开发者的机会、风险或可执行建议
`;

async function getReport() {
  const completion = await openai.chat.completions.create({
    messages: [
      { role: "system", content: SYSTEM_PROMPT },
      { role: "user", content: "请帮我生成一份今日AI行业日报，列出重点新闻和趋势。" }
    ],
    model: "gpt-4o",
  });
  return completion.choices[0].message.content;
}

// 2\. 发邮件
async function sendMail(content) {
  let transporter = nodemailer.createTransport({
    host: "smtp.qq.com", // 换成你的邮箱SMTP服务器
    port: 465,
    secure: true,
    auth: {
      user: process.env.MAIL_USER, // 发件人邮箱
      pass: process.env.MAIL_PASS, // 邮箱授权码
    },
  });

  await transporter.sendMail({
    from: process.env.MAIL_USER,
    to: process.env.MAIL_TO, // 收件人
    subject: "今日AI行业日报",
    text: content,
  });
}

// 3\. 整体流程
async function main() {
  const report = await getReport();
  await sendMail(report);
  console.log("日报发送成功！");
}

main();
```

7.2 获取三组密钥

1.  AI API Key

这里需要看你做的是国内业务还是国外的业务，出海相关业务首推GPT API，费用也很低，如果是国内业务，可以去接豆包或其他国内的API，我没有接过国内的，不做推荐。

GPT API，一般都有免费额度，日报用到的计量很小，免费额度够用很久

另外模型建议用4.1，按照模拟，一个周的日报话费不到1人民币~

1.  QQ邮箱 SMTP 授权码（其他邮箱只要可以开SMTP都可以）

*   登录 QQ邮箱 → 设置 → 账户 → 开启“SMTP服务” → 生成16位授权码并保存

1.  收件人邮箱

*   可以用自己的 QQ 邮箱，也支持逗号分隔多个收件人，你可以同时发给很多个邮箱，只用1次API调用费用

1.  新建 .env 文件，内容如下：

```
OPENAI_API_KEY=你的openai key
MAIL_USER=你的邮箱
MAIL_PASS=你的邮箱授权码
MAIL_TO=收件人邮箱
```

* * *

## 8\. 测试脚本

在终端输入：

```
node report-mailer.js
```

正常输出应该是：

```
日报发送成功！
```

常见报错分析：

*   Cannot find module 'openai'

*   你没装好依赖，重新 npm install openai nodemailer dotenv

*   Invalid API key

*   检查 .env 文件里的 key 写错没

*   邮箱相关报错（如授权失败）

*   授权码是不是拿错了、邮箱填错了

排错通用手段：

*   看报错的第一行，搜“nodejs 报错 xxx”基本都有解答

*   .env 文件要和脚本在一个目录

*   路径别写错，不要有中文路径

* * *

## 9\. 实现自动/定时发送

用系统自带的定时任务。

Mac/类Unix：

*   打开终端，输入 crontab -e

*   加一行（每天早上9点自动跑脚本）

```
0 9 * * * cd ~/Desktop/ai-report && /usr/local/bin/node report-mailer.js
```

（/usr/local/bin/node 要换成你 which node 查到的路径）

Windows：

1.  打开任务计划程序

*   按下 Win 键，输入“任务计划程序”或“Task Scheduler”，打开它。

1.  新建基本任务

*   在右侧点击“创建基本任务”。

*   给任务起个名字，比如“AI日报自动发送”。

1.  设置触发器

*   选择“每天”，然后设置你想要的时间（比如每天早上9点）。

1.  设置操作

*   选择“启动程序”。

*   程序/脚本：填写 node.exe 的完整路径（比如 `C:\Program Files\nodejs\node.exe`，可以在资源管理器里找到 node.exe 右键属性复制路径）。

*   添加参数：填写你的脚本全路径，比如 `C:\Users\你的用户名\Desktop\ai-report\report-mailer.js`

1.  完成设置

*   按提示完成即可。

* * *