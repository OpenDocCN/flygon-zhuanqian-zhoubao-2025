# AI智能体-安卓手机也能玩转自动化：打造小红书文案提取+AI二创一条龙工作流教程

> 来源：[https://w63nbfedzw.feishu.cn/docx/JLxDdgB43ocSV2xpoadcuP9Yn4b](https://w63nbfedzw.feishu.cn/docx/JLxDdgB43ocSV2xpoadcuP9Yn4b)

# 为什么要做这个

苹果用户们早已开始用快捷指令+飞书多维表格实现一键获取视频文案，作为安卓用户的我们也不能落后！本文将介绍如何利用安卓平台的自动化工具，打造一个Android快捷指令的文案提取工作流，让创作效率翻倍。

# 你将收获

*   掌握安卓手机快捷指令（MacroDroid）的设置方法

*   学会搭建coze小红书文案提取智能体

*   了解如何在飞书多维表格调用工作流

*   掌握飞书机器人流程设计技巧

*   学会使用飞书多维表格AI插件

# 所需工具

1.  飞书PC端

*   下载地址：https://www.feishu.cn/download

1.  飞书机器人流程设计

*   飞书账号要求：

*   个人版账号即可（无需企业版）

1.  扣子（Coze平台账号）

*   官网地址地址：https://www.coze.cn

*   使用手机验证码登录

*   目前扣子智能体发布的飞书多维表格字段捷径插件每天200次，不知道专业版会不会多一些，因为没有超过200次，暂时不知道。可以使用我发布的扣子工作流调用字段捷径插件调用扣子工作流。

1.  MacroDroid（安卓自动化工具）

*   版本要求：

*   Android系统：7.0及以上

*   MacroDroid版本：5.5.24

*   下载安装：

*   Play商店：MacroDroid - Device Automation

*   APK直接下载：官网https://www.macrodroid.com/

*   权限配置：

*   悬浮窗权限（界面操作）

*   后台运行权限（保持活跃）

*   使用建议：

*   给予所有必要权限

1.  小红书App

*   账号要求：

*   正常登录状态

# 搭建流程

## coze小红书文案提取智能体搭建

构建智能化文案处理核心

### 智能体基础配置

1、登录扣子后，点击左上角的➕创建智能体，在弹出窗口点击创建智能体下面的【创建】：

![](img/9c9c95b0ab45d1a10f71120af3bd74df.png)

![](img/293c58d2ea5ee948748292424fc9ca81.png)

2、设置智能体内容：

![](img/196bfd571cbf9a53b9d88ff41e6c9198.png)

3、设置智能体为【单 Agent （对话流模式）】：

![](img/e799c20ec5bf05cb1eaa8010d3705f4c.png)

4、点击【点击添加对话流】开始添加工作流，然后点击【创建对话流】：

![](img/3e9ec2feb3d6865235ad8fa61cc18252.png)

![](img/983d751878a77c1df52d7d554f70801f.png)

### 智能体工作流设置

1、填写对话流信息：

对话流名称：rednote_extract

对话流描述：小红书笔记信息提取

![](img/cf48a6b6bb1fe372e38f642b263b0911.png)

![](img/efd15f1638931be36be72c52db2e09c0.png)

2、开始节点不用设置，鼠标移到开始节点右边中部，会出现个➕，点击➕添加一个插件节点：

![](img/7f4501a37557d03f4b0af83359840c6c.png)

![](img/56ea9b653d1f050e08e8659a85dbafd1.png)

3、搜索工具集合，点击>展开，然后选择【get_rednote_info】：

![](img/da33294eeb2c7ee30f3bf64c99b2f6b5.png)

![](img/4a64a924bb8f8fbc3e2ebed6fb225576.png)

4、设置【get_rednote_info】节点：

节点名称：get_rednote_info

输入设置：

content：引用【开始】节点的【USER_INPUT】

cookiestr：按需，可以不设置

![](img/0f30aea4dafeeed1d12d29803bb11cae.png)

5、添加选择器节点：

节点名称：选择器

条件分支设置：

如果设置：

条件1：设置【get_rednote_info】节点的flag等于1

条件2：设置【get_rednote_info】节点的type等于video

两个条件是且

否则如果设置：

条件1：设置【get_rednote_info】节点的flag等于1

条件2：设置【get_rednote_info】节点的type等于normal

两个条件是且

否则设置：

否则无需设置：

![](img/2e8d500a5adce71df001052b609eba81.png)

5,1、如果分支添加一个【字幕获取】插件节点：

![](img/c3eac1794f65989771e49d0d3e201ff2.png)

节点名称：generate_video_captions_sync

输入设置：

url：引用【get_rednote_info】节点的video/url

![](img/07db8b8231657762d28d89c6328edfb3.png)

5.2、否则如果分支添加一个代码节点：

节点名称：设置asr空内容

输入设置：

无需设置

输出设置：

asr：string类型

![](img/41f159dd4b19c4944c10d8d252b7a663.png)

代码(Python)：

```
async def main(args: Args) -> Output:
    params = args.params
    asr = ""
    # 构建输出对象
    ret: Output = {
        "asr": asr
    }
    return ret
```

可复制代码：

5.3、否则分支添加一个代码节点：

节点名称：设置空内容

输入设置：

无需设置

输出设置：

collectedCount、commentCount、likedCount、shareCount、urlDefault、notetype、desc、userId、avatar、nickname、video_url、title、ipLocation、lastUpdateTime、tag_text、asr：均为string类型

imageList：Array类型

![](img/035fe6a1ea99540c1569a5be9b4ead64.png)

代码(Python)：

```
async def main(args: Args) -> Output:
    params = args.params
    collectedCount = "无法获取"
    commentCount = "无法获取"
    likedCount = "无法获取"
    shareCount = "无法获取"
    urlDefault = "无法获取"
    notetype = "无法获取"
    desc = "无法获取"
    userId = "无法获取"
    avatar = "无法获取"
    nickname = "无法获取"
    video_url = "无法获取"
    title = "无法获取"
    ipLocation = "无法获取"
    lastUpdateTime = "无法获取"
    asr = ""
    imageList = []
    tag_text = "无法获取"
    # 构建输出对象
    ret: Output = {
        "collectedCount": collectedCount,
        "commentCount": commentCount,
        "likedCount": likedCount,
        "shareCount": shareCount,
        "urlDefault": urlDefault,
        "notetype": notetype,
        "desc": desc,
        "userId": userId,
        "avatar": avatar,
        "avatar": avatar,
        "nickname": nickname,
        "video_url": video_url,
        "title": title,
        "ipLocation": ipLocation,
        "lastUpdateTime": lastUpdateTime,
        "asr": asr,
        "imageList": imageList,
        "tag_text": tag_text,
    }
    return ret
```

可复制代码：

6、添加变量聚合节点，详细配置如下：

![](img/20c9ee45253e702d1d4991f4bc52b195.png)

![](img/b789b18e6d19f11430b9bec41f9b8f8a.png)

![](img/050a306cd369f6fabe9de064319e177d.png)

![](img/5002ed43f9541f6eb7ab2c07668cd52f.png)

7、配置结束节点，选择返回变量：

![](img/fc0e2859b1286947ecbad2dd07c816ee.png)

8、输入一篇笔记链接测试下工作流，点击【试运行】：

```
https://www.xiaohongshu.com/explore/67daa906000000001e007d6d?xsec_token=AB160KrsrDX4GWgUibp6cRQ7qjDlyWLEHJ94-TsJAS_yM=&xsec_source=pc_feed
```

![](img/ea66cead653097de98e019480685fe4a.png)

![](img/8adb1367c720602bd88c9f0715ed146e.png)

运行成功工作流没问题。

9、发布工作流，点击【发布】：

![](img/dc6cbcd0158c82bdf920acc356a7aa90.png)

![](img/c7d045c46cb35cc8e5c547b25f78248a.png)

### 开场白设置

开场白其实是否设置无关紧要，因为我们是要使用插件调用的工作流。

![](img/e5b872a480e81d81da200398ccf1e99a.png)

## 创建个人访问令牌

工作流配置好后就可以创建个人访问令牌了。

### 认证令牌获取

需要先在扣子平台获取令牌。

步骤说明：

1.  登录Coze控制台【https://www.coze.cn/】，点击左侧导航栏的【扣子API】：

![](img/fa2925a4a0fed14fcb451828d5c0446d.png)

1.  进入【授权 ➡️ 个人访问令牌】页面，点击【添加新令牌】按钮：

![](img/b6c446e35f2446cd1068dba803da9e97.png)

1.  输入令牌名称（建议命名与用途关联），设置令牌有效期、勾选【工作流】权限、选择要使用的工作流所在的空间，最后点击【确定】：

![](img/2d9f9e213b92fecb57865b8b03bd4da2.png)

1.  记录生成的API key(仅显示一次，需妥善保存)：

![](img/66b2120c9a8ceb06d79fdc3317dc91e0.png)

保存令牌信息到本地，后面飞书多维表格配置会用到。

注意事项：

*   令牌权限范围需包含工作流操作权限

*   泄露令牌可能导致数据安全风险

## 飞书多维表格设计

### 创建飞书多维表格

1、在飞书个人空间新建个飞书多维表格，删掉非必要字段，设置第一个字段位【笔记信息】，名称改为自己喜欢的：

![](img/21851e443c2d2a3abbcb3e4c8199ad9a.png)

2、添加一个字段，设置字段标题为【小红书信息获取】，搜索字段捷径插件【扣子工作流调用】：

![](img/9d923a94277323556052937a56538acd.png)

### 字段捷径插件设置

1、填写前面创建的扣子令牌到多维表格插件的认证令牌 ，工作流ID在我们编辑工作流时的链接里面有，workflow_id后面的值就是工作流ID，参数字段设置【笔记信息】列：

![](img/562b4ccac911950a2510a0834600f806.png)

2、其他信息配置：

参数名称：USER_INPUT

请求模板：

```
{
  "CONVERSATION_NAME": "Default",
  "USER_INPUT": "$$USER_INPUT$$"
}
```

$$USER_INPUT$$是替换关键词。

输出结果1：desc

输出结果2：asr

输出结果x的内容表示获取工作流的哪个变量的值，只能获取2个，其他的需要通过完整响应数据获取。我这里是想获取视频的语音文案，因为视频作品一般没有标题，所以我就没获取。

获取更多信息：全选

自动更新：启用

3、点击【确定】保存：

![](img/7f8d7ce3910153bae9934c4812fb4fff.png)

4、点击【仅保存配置】：

![](img/e187f430ac006cfec7f115ad0b91195d.png)

## 飞书机器人流程设计

设计个飞书机器人流程把内容插入多维表格。

1、电脑打开飞书，搜索【飞书机器人】：

![](img/4797d42276ae67c7f5e10f7b0dfbf951.png)

2、点击【新建应用】：

![](img/b240bdce809363ee4c4402d1dedb07fa.png)

3、设置应用名称、描述、图标，点击【确定】创建：

![](img/5eb714c4b5b0bfc704c9b4ab1094a8aa.png)

4、点击【创建流程】：

![](img/e850b5bbbdc817965f40719a1f6bc9d8.png)

5、选择触发器设置为【Webhook 触发】，记得保存好【Webhook 地址】，后面会用到：

参数设置为：

```
{
    "content":""
}
```

![](img/5050235e4b478b80fec9fe13c8b0b27a.png)

6、选择操作设置为【新增多维表格记录】，数据表选择我们创建的多维表格的数据表(不要通过多维表格名称去搜索，不能展开多维表格的数据表，不能操作知识库的，只能操作云空间多维表格)：

![](img/3aa28849469aa716ef07cec65fde49b6.png)

字段就选我们的【笔记信息】，值选择Webhook触发的content。

7、点击【启用】，设置名称为【小红书笔记转存】：

![](img/ff41ce34b59a516075ef420aa7d46f82.png)

![](img/cbfef30d6694a3b17fb0474baf60b5f6.png)

8、点击【发布】发布流程：

![](img/74ad7c73614076594b4012edfd318367.png)

![](img/a77795c12675641c1a81dddebc0ba2d1.png)

![](img/e4adc1c20d3456a65ccbaa0f7b989a1d.png)

![](img/51daae03584d8baf615dd7100fb34289.png)

个人版是直接免审的。

## MacroDroid流程设计

安装好 这个步骤就不说了，接下来讲配置流程。

### 创建宏

1、打开MacroDroid手机应用，添加宏：

![](img/76547dbb3e4c0327d192d49b696f5154.png)

### 设置触发器

1、设置宏名称，然后点击触发器右边的➕，选择用户输入的【浮动按钮】：

![](img/d3024bc2827565143b9257142172e552.png)

![](img/0d31d457c6ee7a0cbda2844d0df87efb.png)

![](img/707a9ce14e28241a5a9189d4656ed3c8.png)

2、启用显示在其他应用的上层的权限，然后点击左上角的箭头返回：

![](img/78580875f60c6f58e06e1cd83c338b87.png)

3、根据喜好设置浮动按钮：

![](img/8edf89eabe14edd7a3f3eaf599d42982.png)

### 设置动作

1、点击动作右边的➕，添加个【设置变量】动作，在【变量➡️设置变量】，选择【提取文本】，然后点击【确定】：

![](img/7eca9c7f88c8ff6317d2bcd89c9f9bc3.png)

![](img/981cecb4f0580f163bb0d0272787b6e5.png)

![](img/d970cc3538e31a4776d8cf24a61063db.png)

![](img/d6e488f8c7326ad649e3dbd74c712dbf.png)

![](img/3d2939795d62c8cac1db45ed09a2cd13.png)

2、添加如果动作，在【条件/循环】里面：

条件1：

```
https://www.xiaohongshu.com/explore/
```

条件2：

```
http://xhslink.com/a/
```

![](img/0ece3d061638c5a7b40a7abee7e88de7.png)

![](img/e6d48045e7b02afa450a028b8e984ac2.png)

![](img/3dbb23dc33726688c1e41d6f4828135f.png)

![](img/70b66a98cabc1db8f23eb5ba097e38b4.png)

3、点击如果，然后点击【添加“否则”子句】：

![](img/d5cde2e602e530402f07b84b30eab73f.png)

![](img/f8fbef42e1b6ac3bfa1c52d93eb25e2d.png)

4、点击如果，然后点击【添加子动作】，点击【网络互动➡️HTTP请求】，修改请求方法为POST，网址设为webhook的地址，勾选【完成后才能后续动作】，然后拉到下面，勾选上【将 HTTP 响应保存在字符串变量中】：

![](img/db3ebe60da23917e754b4dad987772af.png)

![](img/f035db4debd0e2935d7c63d6617518c7.png)

![](img/3a192518593bfe4e034617aa08fdba68.png)

![](img/86f26976658e3980ce6876bf17bfb6f0.png)

![](img/6d4b8482f759851abb6a8c766195abf3.png)

5、设置内容正文：

内容类型：application/json

内容正文选择文本，内容填写如下：

```
{
    "content":"{v=分享内容}"
}
```

![](img/f4469383867626681cdbb215c17ad003.png)

6、点击如果，然后点击【添加子动作】，点击【网络互动➡️JSON解析】：

![](img/a2b6aaeb8923b67f0c42d206a33c4801.png)

![](img/32ac98bdf07145f81ae90d3096130672.png)

![](img/c0091a1b2c1c80a3efe2863d0a4f5153.png)

7、点击如果，然后点击【添加子动作】，添加如果动作，在【条件/循环】里面，添加条件，选择【MacroDroid➡️MacroDroid变量】，手动定义填入【[msg]】：

![](img/66c9d6476f19f2ffa93a3fa0107127bc.png)

![](img/ffc84e4be2680db7169545cebbfc27c8.png)

![](img/ec36fa332559296f0df9d21008eb96cd.png)

![](img/f172a6ebf6543634005a067221b2cc59.png)

![](img/aed20b030f611dec5aec844e7329a344.png)

![](img/b5d5dc4e464cfddf18161ec4564fbe12.png)

![](img/cfe51385351749aa12572e4371918f75.png)

设置msginfo[msg]=success。

8、点击如果，然后点击【添加“否则”子句】，然后在如何和否则下面设置【弹出信息提示】：

![](img/8b4c05a62831dcb8650d94737986c301.png)

![](img/18212925d0c60d4a6c2274d329d85736.png)

![](img/da5651f2d7222f84c1bab073297493a1.png)

![](img/f169e3a8f4be1faeede2304367cd9ede.png)

![](img/b7afb77a91fd956aa020231fe239c71b.png)

9、在最下面的否则也设置一个【弹出消息提示】：

![](img/a8947a7777b9608e3406bc6f4f066eea.png)

![](img/30ee102d4df04f0401195a04d74aeb6e.png)

![](img/ae728d5fe3447064df3eae3bcd122031.png)

10、配置好后就可以测试了，记得一定要开启通知权限：

![](img/f9e3ce19d6fedcffea85c5c071231e99.png)

![](img/6d81665f261e8ea18b84bbd839e03f93.png)

![](img/882f41cec709f94e14028907eab8747c.png)

11、查看多维表格：

![](img/aa62725c54e4a376e947dd98458e5edd.png)

在MacroDroid点击浮动按钮

飞书多维表格是在最后一行写入的，哪怕前面是空的，建立表格的时候一定要删掉空行。

12、发现在MacroDroid点击浮动按钮才有效，在小红书的时候剪贴板内容是空的，需要增加个【剪贴板刷新】动作才能获取到剪贴板内容：

![](img/fa84f8c83118d18a1165e21f5739c5ab.png)

## 展示视频

## 信息提取

由于插件只能输出2个变量的值，如果需要获取响应内容中的其他值，可以使用【信息提取】字段捷径插件获取。

1、新建个字段【作品标题】，然后搜索【信息提取】字段，【选择需要提取的字段】选择扣子工作流调用插件输出的【完整响应数据】，提取信息写入“提取"title"的值”：

![](img/de0824b5713761fc42fd1ea29b9b0922.png)

2、新建个字段【作品封面】，然后搜索【信息提取】字段，【选择需要提取的字段】选择扣子工作流调用插件输出的【完整响应数据】，提取信息写入“提取"urlDefault"的值”：

![](img/12c8d49d63123247254afdc494d873a4.png)

![](img/97885c697f1d526600130d31f14cd255.png)

3、新建个字段【作品话题】，然后搜索【信息提取】字段，【选择需要提取的字段】选择扣子工作流调用插件输出的【完整响应数据】，提取信息写入“提取"tag_text"的值”：

![](img/87e9846204402eca0643b05843f178f6.png)

![](img/19fdd6167fee82a5258b814db05e524b.png)

4、新建个字段【作者】，然后搜索【信息提取】字段，【选择需要提取的字段】选择扣子工作流调用插件输出的【完整响应数据】，提取信息写入“提取"nickname"的值”：

![](img/45b6f325f23d27e2c419d153d935a6cd.png)

![](img/4076df7c432699144027754ae1ab1313.png)

5、新建个字段【视频地址】，然后搜索【信息提取】字段，【选择需要提取的字段】选择扣子工作流调用插件输出的【完整响应数据】，提取信息写入“提取"video_url"的值”：

![](img/95e68e6323a5c27a5a4c1ffd05dab907.png)

![](img/d399f9822127c67bdc2f2e11b6ac57aa.png)

信息提取比较简单，根据自己的需求提取需要的字段内容就可以啦。

## Deepseek AI二创

Deepseek AI二创不难，主要是看提示词好不好，容我做个标题党，大家自行发挥这一块哈~

# 思路扩展

除了小红书文案提取，我们还可以进行抖音、B站视频提取，或者更多，相信大家能够开发出更多创新的应用场景，到时候不要忘记了分享出来哦~

# 附录

## 小红书笔记转存宏脚本

把宏脚本分享给大家啦，只要在app里导入就可以啦。

![](img/af3c35badfcd60e27ee755b70d55e015.png)

![](img/02037046e67a5b4690ed1ba70054b2e2.png)

导入时会删除所有的宏，如果已经有宏了，记得备份一份，或者手动创建一个小红书笔记转存宏。