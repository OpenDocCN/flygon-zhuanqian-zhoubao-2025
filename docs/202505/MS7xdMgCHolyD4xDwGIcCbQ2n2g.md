# 每个月1美元，稳定解决Claude环境问题

> 来源：[https://oxpszlsgr00.feishu.cn/docx/MS7xdMgCHolyD4xDwGIcCbQ2n2g](https://oxpszlsgr00.feishu.cn/docx/MS7xdMgCHolyD4xDwGIcCbQ2n2g)

都知道Claude好用，但是对于新手和小白来说，如何低成本弄个稳定的环境不被封是个大问题。

甚至Google邮箱的注册都是个问题。

我把目前我使用的方案分享一下，希望能够对有需要的圈友有所帮助。方法其实很简单，指纹浏览器+静态IP，每个月1美元，就能解决这个问题。

以下操作全程需要魔法打开。

### 第一步，注册webshare

地址：https://www.webshare.io/?referral_code=q1hh2vmrtydn

![](img/faf568f111eaee0d3aa664519994d5d1.png)

QQ邮箱就能注册成功，注册完成后，会送10个免费的静态IP，我们可以使用免费的IP来注册Google邮箱。

![](img/bdf3f8e2e8ec3292aee5c5327038d8c6.png)

点击“Let's Get Started”进入免费的IP列表

![](img/542ffa4ed15f1313b30311bff8d05249.png)

把Proxy Address中的IP复制过去，挨个检测。检测结果如果合格，就可以拿这个IP先绑定上指纹浏览器，先注册几个Google邮箱。免费的羊毛不薅白不薅，当然直接付费买IP也行。

地址：https://ipjiance.com/

如何绑定指纹浏览器，请见第四步

![](img/67c63537a70ff95e2ff54272221b708d.png)

有圈友帖子说检测结果是优良再使用，我没有遇到过，合格就行了。

![](img/a7f07f2cab9460fb7d714f78d2951089.png)

如果不放心，可以使用https://scamalytics.com/这个IP检测工具再测试一下IP的风险

![](img/c832e7ec0f81e6c4a77eef78620ca21e.png)

这个免费的静态IP用来注册几个google邮箱足够了。下面我们再讲一下如何在webshare上购买静态IP。

### 第二步，办一个招商银行VISA信用卡。

![](img/0b297a3958ef2e8add83b0d3ee7e5472.png)

之前推荐的是野卡，但是野卡前段时间被封了

### 第三步，购买静态IP

点击点击【Subscription】下面的【Browse Plans】

![](img/658f38120c30188220afc306d5ddaa83.png)

代理的选择，我们选【Static Residential】静态住宅代理，然后下面选【Private】因为买一个的价格它和【Shared】是一样的，都是一美金，那肯定选更好的。

至于独享我觉得没必要，太贵了，而且待会有办法筛选IP，要是IP被污染了，我们换就行了。

「PROXY NUMBER」选择custom，

「Type Custom Proxy Number」填写1（大家想买几个就买几个），点击Save。我们只买一个就行了。

「Bandwidth」选择250GB/month

![](img/22b00a93f40d0087f8e76e23a30f0262.png)

选择代理所在地区（IP所在地），选择「United States」，并填“1”。

![](img/071eaa30632068fbf3c1fc7562f040dc.png)

选好后点击后面的「Continue」

![](img/2f2ce6452ca59ce40ca71b7d37e3640c.png)

这个框不用管，直接点「continue」

![](img/986cf6a2b71babf6105cc2afcf751d13.png)

付款页面，需要绑定你的visa信用卡，然后支付就行了。

![](img/467f71b1fab58d1f1bdf07ddf4047ec6.png)

由于我们买的不是完全独享的IP，所以每次在使用前，先用https://ipjiance.com/做个测试，没问题我们再用，有问题我们就换（如何换，请看第五步）。检测方法上面说过了，我就不再赘述了。

### 第四步，绑定指纹浏览器

我用的指纹浏览器上AdsPower，地址：https://share.adspower.net/6nwzVs

下载后点击左上角的新增浏览器

![](img/7eb599dc840abca70737fb15f831f9ad.png)

基础信息设置

名称Google、Claude随便填，自己能看到每个浏览器是干啥的就行。

浏览器在SunBrowser里选个Google最新版本

操作系统选个自己喜欢的

其他的都不用填

![](img/5f366190842a655e22f3e53afe1618c6.png)

代理信息设置

代理类型：Socket5

代理渠道：IP2Location

主机：端口：填写webshare上你找到的合格的IP地址，和对应的Port。（每个人的都不同，请按照实际的填写）

代理账号：IP的Username（每个人的都不同，请按照实际的填写）

代理密码：IP的Password（每个人的都不同，请按照实际的填写）

![](img/bea836f22dbbcb2eded8075217496d45.png)

点击检查代理，看是否连接测试成功。其他的内容全部默认就可以了

![](img/d1c3d5571ff8cd612c101f4a6f70ea8d.png)

最后一步，还需要设置用系统代理连接代理，确保我们能够访问外网

![](img/5dabbf7b040021872cdf753c4b986685.png)

点击“确定”，就会打开一个浏览器

![](img/49751f7f60143799a30a635f24375c8b.png)

到这，就可以直接注册Google邮箱和Claude了。

无论你的魔法是规则还是全局，在指纹浏览器中打开的网页IP检测的地址全部都是一致的。检测工具：https://ip111.cn/

![](img/0d94aa33f35ab4b2835e71bce14a4c22.png)

至于Google邮箱的注册和Claude的注册，大家一步步操作就行了，有个纯净的IP，注册起来就非常简单了。

### 第五步，如何更换IP

选择你要更换的IP，然后点击「Replace」

![](img/79ebf4559dcd55955584fc456be0c35c.png)

选择「Copy & paste proxies to replace」

![](img/f858663334e66d1dee6a99ea99d213cb.png)

选择Add a proxy from a Certain country

![](img/bda759c6a9adce06e5eaf1c25675818f.png)

点击Preview

后面再点「yes，Replace」就可以了