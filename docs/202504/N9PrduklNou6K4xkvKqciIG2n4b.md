# 【喂饭教程】手机一键采集小红书商品到飞书多维表格

> 来源：[https://d912sxp8dd.feishu.cn/docx/N9PrduklNou6K4xkvKqciIG2n4b](https://d912sxp8dd.feishu.cn/docx/N9PrduklNou6K4xkvKqciIG2n4b)

更新：获取小红书商品最新销量

更新：手机小红书笔记采集

更新：电脑采集笔记

更新：在小红书笔记工作流上添加采集视频

更新：常见问题-关于api执行工作流出现"code": 6039

更新：扣子更新了很多东西，如果碰到新问题可以在文档下面留言

# 前言

本文主要利用手机快捷指令类软件，通过扣子工作流采集，发送到飞书多维表格。文章写的比较详细，相信小白应该很容易操作。也写得比较赶，如果操作过程中遇到问题，可以直接问我。

小红书手机端浏览商品比较方便，分享复制链接通过快捷指令就可以一键发送到飞书多维表格，遇到想收集对标商品的也可以省点时间。

![](img/a9c293981c89d0aa21e9a2fd3262b341.png)

![](img/e15af93c728352d9fe7e852c0765fff8.png)

![](img/986b4d9f5a03d39619167dc7980af8a2.png)

![](img/556ffdcb0cd939f1712f0ee73ad1de9c.png)

简单流程图

# 飞书

*   注册登录

飞书：https://www.feishu.cn/

## 创建飞书多维表格

简单流程图

### 方法一（快捷）

#### 套用多维表格模板

打开链接，使用该模板，会保存到自己飞书里

![](img/90fe419d1566bfd2e23001a475486c17.png)

#### 修改多维表格分享权限

*   修改权限

![](img/a9fdae715f1c29c633844157dede201b.png)

#### 检查飞书多维表格的链接

*   飞书多维表格链接

![](img/5459f44acec452c4273c30e0c86404ca.png)

*   检查链接中的token是不是base类型

![](img/acefb83b0973c89b3d457f45f032d0f1.png)

*   是base类型的，跳过这步。如果不是base类型，请把多维表格移动到我的空间，或者云盘。

![](img/8553650c962f794a540494f6c0277dc2.png)

![](img/d388fd592ca6604ef001135205097dba.png)

*   说明

![](img/abdf4a0dc84a2a0ac7a492d9f58c303c.png)

#### 多维表格的token和table_id

红色字体的为飞书多维表格token，绿色字体为飞书多维表格table_id

![](img/2f69bfb209859de6c5aa3e2ea70b6757.png)

请记录下自己飞书多维表格的token和table_id，扣子工作流里飞书多维表格插件会用到

飞书多维表格app_token=A27xbnXHXaDpnrsLft9c7N6An4g

飞书多维表格table_id=tbljfQRh9edYZLp7

### 方法二（手动）

#### 手动创建多维表格

![](img/156e655bc16e54fca971daa0ec5f0bc0.png)

#### 删除行和列

![](img/e1ddc9f3f874cc34602ce3170e36a1ea.png)

#### 添加相应字段

![](img/9560bec020eb103fcec0ade592e456cb.png)

#### 修改【图片】字段

因为链接无法直接显示为图片，需要通过字段捷径【链接转附件】来显示图片

![](img/a538a6dd8f91fb0da72d307d9fa64229.png)

#### 修改【图片链接处理】字段

因为字段捷径【链接转附件】无法显示超过五张图片，还需要通过字段捷径【信息提取】去处理

![](img/b7fe77e0ca6b663dab71d8e6fdfbf8f4.png)

#### 修改多维表格链接的权限

![](img/8dd42eb5053683637b0d279c7417085b.png)

1.  多维表格的token和table_id

红色字体的为飞书多维表格token，绿色字体为飞书多维表格table_id

![](img/3402977c266b7b2f83e30506c95e9bc2.png)

请记录下自己飞书多维表格的token和table_id，扣子工作流里飞书多维表格插件会用到

飞书多维表格app_token=A27xbnXHXaDpnrsLft9c7N6An4g

飞书多维表格table_id=tbljfQRh9edYZLp7

# Coze扣子

## 注册登录

扣子官网：https://www.coze.cn/

![](img/40442ec207a8c2aaf0eecec751a86550.png)

## 工作流

### 小红书商品采集

*   工作流逻辑

![](img/5db7ec8e6a5be89ebeba253288914241.png)

#### 创建工作流

![](img/22d18c29442927d85e312860f4afd876.png)

*   工作流名称

![](img/7c958283e7128b3e3859eba6416464bb.png)

#### 节点-开始

修改变量名为”url”

![](img/50f178a9b02734e4f90654ce7714d6c3.png)

#### 节点-插件-小红书-xhs_goods_detail

添加节点插件

![](img/56bda7c8ea07f3000d81eb1acca0ea1a.png)

搜索小红书，添加小红书下的xhs_goods_detail插件

![](img/0b8e36a1c76c6ae629646c1f257657b3.png)

两节点相连的方法

![](img/de4f59ac1490fb43242dc0942a5348ae.png)

选择变量值

![](img/8c10381fa436697a64c30e6deba42522.png)

#### 节点-插件-链接读取-LinkReaderPlugin

添加节点插件

![](img/3a1ffcc4b6a4e01e2b95caa585c1e64e.png)

添加链接读取下的LinkReaderPlugin插件

![](img/bdab3f2e751327ff59b9c73aafd2ad46.png)

选择变量值

![](img/9521266204d52dc9fc89b72ee9d65002.png)

#### 节点-代码

添加节点代码

![](img/56b585a9febd67fd340ccc3e1aa55427.png)

选择变量值

![](img/9fb8871c57f84b4e82e6f39bf734017d.png)

写入代码

![](img/b2cf70a0190e3dee78823b5c647cd65c.png)

代码如下：

需复制请打开：

```
async function main({ params }: Args): Promise {
    const input = params.input || ''; 
    const regex = /已售\S+/; 
    const matchResult = input.match(regex);

    const ret = {
        "key0": matchResult ? matchResult[0] : "" 
    };
    return ret;
}
```

#### 节点-代码1

再添加一个节点代码

![](img/7a5025a459933c32730f7edacfca0151.png)

![](img/4ac0cd4566b753f6f1abb4540b0db780.png)

请添加变量，变量名请对照下图来修改

![](img/6688070dc14e699dce359b5b0f4c395c.png)

具体的变量值请对照下图来选择，xhs_goods_detail的变量值对应的变量名如下：

![](img/35db3e7bbb29aef56b04a7a7c1d96667.png)

![](img/b4f74785b1f2b45d9bbb5d93740483d2.png)

变量名sales对应的变量值

![](img/7a4b708151f03bcdb2cfc81df3535419.png)

变量名url对应的变量值

![](img/aef59d93bc557af569be2459667ae69c.png)

*   写入代码

![](img/325aa7860edebcd8604939bbd491df38.png)

代码如下：

需复制请打开：

代码里文字对应飞书多维表格字段标题，如需修改，请保持一致

```
async function main({ params }: Args): Promise {
    // 构建输出对象
    const list = [
        {
            "title": params.title,
            "name": params.name,
            "fans_amount": params.fans_amount,
            "seller_score": params.seller_score,
            "price": params.price,
            "deal_price": params.deal_price || '',
            "images": params.images,
            "sales": params.sales,
            "url": params.url
        }
    ];
    let records = [];
    for (let item of list) {
        let record = { "fields": "{}" };
        let fields = {};
        fields.商品名称 = item.title;
        fields.店铺名称 = item.name;
        fields.粉丝数 = item.fans_amount;
        fields.店铺评分 = item.seller_score;
        fields.销量 = item.sales;
        fields.售价 = String(item.price);
        fields.到手价 = String(item.deal_price);
        fields.图片链接 = item.images.join(','); 
        fields.商品链接 = item.url;
        record.fields = JSON.stringify(fields);
        records.push(record);
    }
    const ret = {
        info: records
    };
    return ret;
}
```

#### 节点-插件-飞书多维表格-add_records

*   添加插件

![](img/0c1098425c04e289398eb363b5c69c06.png)

*   搜索飞书多维表格，添加飞书多维表格下的add_records插件

![](img/6383416b311a727df585d896ac3006a2.png)

*   填入自己飞书多维表格的token和table_id

![](img/4cb3134372318f10d39e200832c9807a.png)

*   变量名records对应的变量值

![](img/58e81331e091f31f0c4f4d9f2dde589d.png)

#### 节点-结束

*   此工作流的结束节点用于结束流程，对于变量名和选择的变量值没作要求，我们的目的已在上一个节点完成了。

注意

新手请按照下图选择变量值，方便检查问题。

![](img/0f5b089cde3ab6580796f6bbc22c1304.png)

#### 测试工作流

*   试运行，粘贴商品链接测试（商品链接：小红书APP-分享-复制链接）

![](img/578855e25ebdad8c5f7d2ebc0ae4ac3a.png)

*   第一次运行，会提示运行失败，需要授权，请复制链接到浏览器打开授权

![](img/3d72ea58fded648480ff52aadc4cfe58.png)

![](img/b4095ac3781ada9e0a6ec465b9423fce.png)

*   运行成功后，正常情况多维表格就会更新数据。测试没问题后发布工作流

![](img/0d8b6b439dbcdaaf162f544d23ab9f53.png)

*   记录下工作流的workflow_id

![](img/72e8476347d30c192231ca6085843505.png)

红色标记的为workflow_id，请记录下来，后面要用

workflow_id=7492048120039358483

## 创建个人访问令牌

1.  添加新令牌，用于手机发送数据到扣子工作流

![](img/f753dd1bee98816909f6daaf48b23bee.png)

1.  时间不能超过30天，权限选择工作流，选择个人空间

![](img/8c5e0357afc9d3dac69f8626684eea98.png)

令牌仅显示一次，没保存好请重新添加新令牌

![](img/edf7f252bc5b6dbe0db60dc2c543dae2.png)

红色标记的为token，请保存好，后面要用

token=pat_iOgnznoTzJUJCUTSpmzWXjzGXRczmOacFuQBdE6uoEKSsiayVrpajpjWKKSSLSMT

## 测试扣子API执行工作流

1.  扣子API里选择执行工作流，测试token和workflow_id是否正常

![](img/7250e907fd5b11ed7847aca640f68f03.png)

1.  填入个人访问令牌token，工作流的workflow_id，还有parameters的参数

![](img/920db0870d36328ecc1c6ac7ed64f2eb.png)

Parameters的格式如下

*   其中的url为开始节点的变量名

```
{"url":"填入小红书商品链接"}
```

注意

以下情况为飞书未授权，请复制括号里的网址进行授权，如下图

![](img/a0c01c0daf5af8ecbc0c1e547cb1ba8f.png)

# 手机采集方法

## 苹果手机

苹果手机可以利用自带的快捷指令软件去实现一键采集

### 快捷指令

已编辑好指令，复制到浏览器里打开获取

https://www.icloud.com/shortcuts/c4ef07994b7649c1b97fe68bb209f7ac

1.  获取捷径，添加到快捷指令，修改设置

![](img/89076d55d21ac85226af859996f04ac6.png)

1.  修改小红书商品采集的设置

![](img/e2bb8aa5cfdadaf31d413174d0d3edd6.png)

1.  只需修改里面的Authorization和workflow_id

![](img/b674ab445b009ea3422dbfa8b9cf100f.png)

红色部分请替换为自己的tokent和workflow_id，注意格式

```
Authorization=Bearer pat_iOgnznoTzJUJCUTSpmzWXjzGXRczmOacFuQBdE6uoEKSsiayVrpajpjWKKSSLSMT

workflow_id=7492048120039358483
```

### 触发方式

1.  打开辅助触控

![](img/cec455a2689537eaf9f1ada4440b263e.png)

![](img/6c8f98c11aaaddcba9dc2c6693a52ed1.png)

![](img/a4110d4e188ed8996af50ca37ac4e0e7.png)

1.  选择自己喜欢的触发方式

![](img/36aa75446ee7e52c7d6485152af0c9c7.png)

1.  例如轻点两下

![](img/657f2b0b58a02ccd72cbd5aefee5c041.png)

1.  例如小圆点的顶层菜单

![](img/387b6d8281185e55946bbf1853457311.png)

1.  例如iPhone 8以上手机可以设置轻点背面

![](img/dcaec566cc117091af05d1d0eafe21a4.png)

![](img/4543ef4c0439723aaf2bb1b7e48262a5.png)

### 一键采集

在小红书商品页面，点击分享，复制链接，触发方式

![](img/d1fde8b286e167e95605184a772d4eb0.png)

![](img/1a06d36075bfb80fb61be999d79f83b3.png)

![](img/49fab793ee760b8210ce4d90d3491cc1.png)

## 安卓手机

安卓手机可以利用第三方自动化软件Macrodroid去实现一键采集

MacroDroid是一个任务自动化配置智能触发器，界面简约易用，直观的配置过程指引你进行相应的配置，列出宏，可直观查看到宏的数目，还能查看宏的详细信息并进行删除，复制，等编辑操作，添加宏中有已经列好的开关操作，可以选择来添加动作，创建新的宏。

*   安装Macrodroid软件

由于MacroDroid是通过宏来进行相关操作，所以我们需要去配置一个宏，下面会给出两个方法，一个是导入以配置好的宏，只需修改关键的参数；另一个是自己手动添加宏，一步一步的配置。

### 方法一（导入已配置的宏）

1.  导入宏

宏文件如下 ：

![](img/d54af03f21eb29bbf9f31b99eafe0674.png)

![](img/4e4be6788a6061b04aa74654b8b0b2f8.png)

1.  打开权限

运行过程中会出现要求启用显示上层的操作，请启用

![](img/6eb8bb563881c2fca8c7dc11edfe7d14.png)

1.  打开HTTP请求，选择配置

![](img/fb8cf409953c8ac2fdf567d28bc70f15.png)

![](img/5bfe50011638a47bd4e2792ce6f8f47e.png)

1.  修改内容正文

![](img/77da3c51fc1342173c837a31af70acd8.png)

内容正文代码如下：

```
{
  "parameters": {
    "url": "{v=商品链接}"
  },
  "workflow_id": "7492048120039358483"
}
```

1.  修改请求头参数

修改为自己的扣子的token

![](img/5d9339208d4ba2cdb744b7ea347f26cf.png)

Authorization的格式如下，请把红色的部分替换为自己扣子的token

```
参数名称：
Authorization
值（红色部分换成自己扣子的token）：
Bearer pat_iOgnznoTzJUJCUTSpmzWXjzGXRczmOacFuQBdE6uoEKSsiayVrpajpjWKKSSLSMT
```

修改完成后记得保存设置

1.  测试

![](img/ff39be9a9c9f36bb800b28c1adfae613.png)

![](img/64a21a5eef40a66a86348db6cd3935b2.png)

完结

### 方法二（手动添加宏）

*   简单流程图

#### 新建宏

![](img/201bfacf17137483a020e3cec0c89307.png)

#### 添加触发器

![](img/76eac6ac4838b3a97c1c68e41f86c869.png)

![](img/ba80b0b20600cfdd5b6f1da852196977.png)

![](img/bef469506ec313b9633b25b5cc3aadff.png)

![](img/45fe00dcac835e937182a56b744e24bc.png)

![](img/12d7831c6bd045797e918cd773900ad4.png)

添加动作

#### 添加动作-剪贴板刷新

![](img/d2f64fc0820d75495ebffd7a75667b09.png)

![](img/99bda913aca9d58311b1b69e9942bd8d.png)

#### 添加动作-设置变量

*   设置剪贴板文本为商品链接

![](img/3a0bc5b8b98d3050ef6d103bd24aa79a.png)

![](img/af5ead98654328546f49d6ee16d2f402.png)

![](img/df6b86675721d66731d1af87fecff844.png)

![](img/896d63e17ae90246f1349e9bcc34520c.png)

![](img/d5d010deef2a12d7c763c4e334b275b5.png)

![](img/231cb00ebb8ca276ed9a698e982f4d35.png)

#### 添加动作-如果

*   添加条件，剪贴板内容是否包含小红书商品链接

![](img/7a9831e1cb439cf472ae3024a09e68a5.png)

![](img/8778e250bc32d75d2a9fed982247f742.png)

![](img/41fddc81f909c978a1eeb050e2faeaf0.png)

![](img/9b6c1f15c39a7956ef650316551bc161.png)

![](img/636f769735c0e7b85434e3ffc0625d1b.png)

![](img/86cc514c56bc68b9591974b1f9c90bca.png)

![](img/62e4e51380a7709664441e0f0f15eb21.png)

![](img/a0b9cfba4eaf5341cc3ff5cebc8048b2.png)

![](img/467d121afb62a172ca20bd8bffd2f672.png)

#### 添加【如果】的子动作

*   添加HTTP请求，按照格式填入相关参数

![](img/a7104111decb9c1831d29e16e3824428.png)

![](img/f09edcbe5107de53d8a91bd850f32159.png)

![](img/6446e0945a215f8cf49a7c12aab7b167.png)

![](img/b3848640e657aa972af7d63c6166b544.png)

![](img/969ab6249bf3ac613abd15d40cd424da.png)

![](img/615c29810a06f717488abe115a7220aa.png)

![](img/ab4d6d1f0f985034e1b409b9afce6cc6.png)

![](img/d5e486099c2ca39eef5a0dfe9e77a0e0.png)

![](img/f607343fccf9235d91db3a32aadaf67e.png)

#### 添加【如果】的子动作

*   添加JSON解析，判断响应内容

![](img/e08a2b9807ca7a860923b78be0e87e98.png)

![](img/335d06ddedbf5a2b637d6fe3d701bd37.png)

![](img/c3ad2b40f5de71ed4b23f31ca6554c31.png)

![](img/1af1986ea4e5e4afe6f8b5e700368419.png)

![](img/1e4a86d6c82f98ca43c7da79b023e755.png)

![](img/6751a044839fc644d13adc9060884bc0.png)

#### 添加【如果】的子动作

*   再添加一个如果，判断扣子的响应内容

![](img/211836592a38266b7b80c4b978ec0252.png)

![](img/e96556d135354a290dede2d28ad48064.png)

![](img/a412f737f5e4826e4b4fdd53d0a48c70.png)

![](img/ea33e714aecb896d98f57bd64be24c3d.png)

![](img/0274c2dcd486a7c40e3140828da0f9d6.png)

![](img/330cc1220fd84c46387ef2d00779a608.png)

![](img/0d7acb58d4ca83daafa4106d2abe7505.png)

![](img/80cf02b089f66c4df49fca4ec4a14890.png)

![](img/4e84d00bc6bb6f153f5240884efab58e.png)

![](img/dc7eb241645f30e1bee6dd37b1e50bfb.png)

#### 添加【如果】-【如果】- 子动作

*   添加动作，条件成立后弹出保存成功消息提示

![](img/1f00db4fb8fb151c0c29a4a30480f483.png)

![](img/bdc3d3997b0a3e12677b60358a25ef79.png)

![](img/9792a63bcb2d11c218489b590b895eba.png)

![](img/dfd29813ce2a6f8ae23321bfe7cf72d2.png)

#### 添加【如果】-【如果】- 否则

*   添加“否则”子句

![](img/c71d9987431b76f896f472b1cdaeb931.png)

![](img/6be4aee658e29412a8e69386db1490b8.png)

#### 添加【如果】-【如果】- 否则 - 子动作

*   添加动作，条件成立后弹出保存失败消息提示

![](img/628bfc4a57cc2fe2b5af25029a739f32.png)

![](img/2ef04357f06b8af8492ea261bce1022f.png)

![](img/32fa1d0b40d2b06dcf7d0c99d85174be.png)

![](img/c42867e295c6ae37b845dacc427b9ee9.png)

#### 添加【如果】-【否则】

*   添加“否则”子句

![](img/f86d3c0f04988f48ba6c4f724289c63f.png)

![](img/518c4aa7052e192b5051f82ceae84989.png)

#### 添加【如果】-【否则】- 子动作

*   添加“否则”子动作，条件不成立弹出无效链接消息提示

![](img/2d31e58181033a40d15f4e684d55f4bf.png)

![](img/eaf0ea2ebee07d80cbecf40445105ad8.png)

![](img/f55f5761b05dd8b88c4eb815cc89407b.png)

![](img/0971c6f749b1ff6c19f029c71fc6167f.png)

![](img/5d72b3f51a7f7a4a7610292f1817cc8f.png)

# 更新

## 获取小红书商品最新销量

在之前采集商品信息的基础上，增加新增销量（由于第一次采集后商品的数据都是固定的，由此可以再添加一个字段，用于获取实时的销量），第一次采集商品时的销量，和每次字段捷径采集的销量相减，得出新增销量

采集商品信息后，如果还想用原来的多维表格去记录销量增长，可以通过创建智能体，发布成为飞书字段捷径，在多维表格里添加字段捷径，获取最新销量，通过两次不同时间内获取到的数据计算出新增量。（个别商品无法获取 到销量）

![](img/e1b84541b179dbb185436c89a89e6822.png)

### 创建字段捷径

#### 创建扣子智能体

*   打开扣子

![](img/12e5c553415f19604ba77d952812d682.png)

*   起名

![](img/8e0ed53f5d8ad888f808fdaf96c0f9e9.png)

#### 添加创建对话流

*   选择对话流模式

![](img/2986fb85f3d209ef0f8b14487e54533b.png)

*   添加对话流

![](img/47faff33d4bc70b88b07406dc8479e29.png)

*   创建对话流

![](img/da7a5e523cc68fcb9db5af2ab109aa7c.png)

#### 添加节点-链接读取-LinkReaderPlugin插件

*   添加节点插件

![](img/144584b07bcbe9f82c3b0b465fb4d924.png)

*   添加LinkReaderPlugin插件

![](img/f64db564255559ac90c59bd1907c6333.png)

*   选择变量值

![](img/ec2cf4988b1c9c293cf5c1ac5a859623.png)

#### 节点-代码

*   添加节点，选择代码

![](img/9200bb0683f52d226b8ed0305590d633.png)

*   选择变量值

![](img/506b62b5fdd30f3731fb1ca5300820ed.png)

*   粘贴代码

![](img/b8ab72d3802b78c6e7e6935ad0cadbf1.png)

代码如下：

需复制请打开：

```
async function main({ params }: Args): Promise {
    const input = params.input || ''; 
    const regex = /已售\S+/; 
    const matchResult = input.match(regex);

    const ret = {
        "key0": matchResult ? matchResult[0] : "" 
    };
    return ret;
}
```

#### 节点-结束

选择变量值

![](img/cfa7ae7736dfccc9fe7d9e9ca0d6675b.png)

#### 试运行

![](img/b5557430ae0e4cf96fc662e6350dec11.png)

*   输入商品链接测试

![](img/2262c587602463ac3e8ac4a3602e32f0.png)

#### 发布对话流

*   点击发布

![](img/f4313529d8efd81ed3532ea81a1aab4d.png)

*   添加到智能体

![](img/3d02ecb8033f350f757e7dd29a80c790.png)

#### 发布智能体

*   点击发布

![](img/9d8b97dbac65a63d79a62fc64cfe1aa2.png)

*   跳过开场

![](img/949087b1c082a22c07a45d99f7407c7c.png)

*   选择发布平台

![](img/9d65ecfb3d9e839121549af65b79664d.png)

*   授权配置多维表格

![](img/0f01ec8e7903cb0eaf9f44e2b77f32bd.png)

*   填写捷径信息

![](img/26cc3ec4260d5086ae9e217e710e5024.png)

*   提交审核

![](img/7ffbae3b37988b3a563da3c3456d8a0d.png)

*   点击发布

![](img/f36f27351d7738b16ea0c349ce903685.png)

![](img/0426444be6278b303a4171f3c347140a.png)

智能体审核需要一点时间

### 修改多维表格

#### 方法一（套用模板）

可以套用模板，但多维表格里的字段【最新销量】里的字段捷径需要修改为自己发布的智能体。（具体操作可以参照方法二 ）

![](img/b9b4d2e4f2c81b84cc661ec3d7ab3263.png)

#### 方法二（手动修改）

##### 添加字段-采集时间

*   获取第一次数据生成的时间

![](img/82b8e7413c475e5d946d38560e0049ba.png)

##### 添加字段-最后更新时间

*   获取最后更新的时间

![](img/7c943a4ccc9e160696afed41d53ea5aa.png)

##### 添加字段-最新销量

*   获取最新销量

![](img/625a6cd7072b51a8124e8e44ed558f36.png)

##### 添加字段-处理销量

*   提取销量的数字用于计算

![](img/5c33b8c8b64fa916fd191a4adec29cb7.png)

##### 添加字段-处理最新销量

*   提取最新销量的数字用于计算

![](img/ce6e002a97533837573933749bb54614.png)

##### 添加字段-增加的销量

*   计算新增销量

![](img/cc031a8818ade524d1e723c333aca952.png)

##### 调整位置和隐藏字段

*   为了美观，可以调整位置，和隐藏一些不用显示的字段

![](img/cb185644542cd6a09bc13b68f27b539a.png)

### 测试使用

*   使用原有的手机快捷指令去测试

## 小红书笔记采集

![](img/7440e79e64dd867381ecf2fe5094a860.png)

### 飞书多维表格

#### 创建多维表格

此处直接套用已做好的模板

打开链接，使用该模板，会保存到自己飞书里

![](img/dcaaa656f61f6c4216dd7d044967816f.png)

#### 修改多维表格分享权限

*   修改权限

![](img/c2074bfeb2561f80f2ab5576ed679f91.png)

#### 检查飞书多维表格的链接

*   飞书多维表格链接

![](img/032250911c23b9246a9c8cb50307685f.png)

*   检查链接中的token是不是base类型

![](img/7932bd7cd04cc919f7842789fcca574e.png)

*   是base类型的，跳过这步。如果不是base类型，请把多维表格移动到我的空间，或者云盘。

*   说明

![](img/4ad76de04bdd8191a9c00fa92e67bf4c.png)

#### 多维表格的token和table_id

红色字体的为飞书多维表格token，绿色字体为飞书多维表格table_id

![](img/80e622cce03ed1529483782392967536.png)

请记录下自己飞书多维表格的token和table_id，扣子工作流里飞书多维表格插件会用到

飞书多维表格app_token=L9eLbhW46aH1SRs0vLtcAPxJn2b

飞书多维表格table_id=tblyv2CsIXIl9CsG

### 扣子工作流

#### 创建工作流

![](img/0d68f12bb70b4cfa2aad9c4e8e15ea07.png)

*   工作流名称

![](img/32e28d2a1f21bdad7ace9a24039eff93.png)

#### 节点-开始

*   修改变量名为”url”

![](img/269dee006c6464c2c3be02d58cc54240.png)

#### 节点-插件-小红书分享链接提取-get_url

*   添加节点-插件

![](img/7042a345f6ab341d4657470cfd591bfa.png)

*   添加插件-get_url

![](img/788f97f0628fe7d2ace5b69a9985c28f.png)

*   选择变量值

![](img/f853e36cf459e7fdce975d2952b8ee20.png)

#### 节点-插件-小红书笔记信息提取器-get_note_detail

*   添加节点-插件

![](img/dda76b3a14fd295db333dafc5ca287d8.png)

*   添加插件-get_note_detail

![](img/15bd630b951bdc76d450499d9e1c90f9.png)

*   选择变量值

![](img/f668ba07fc7c30b998f673a6e6cc871a.png)

#### 节点-代码

*   添点节点-代码

![](img/7da3c434955e9c35f309154840a5fe37.png)

*   添加变量值

![](img/3f5dfb09c5caec2677c7300773ab70f5.png)

*   写入代码

![](img/dc10dc52af143de4317a907eaab00d68.png)

```
async function main({ params }: Args): Promise {
    // 构建输出对象
    const list = [
        {
            "title": params.title,
            "author": params.author,
            "content": params.content,
            "publish_time": params.publish_time,
            "location": params.location,
            "like_count": params.like_count,
            "collect_count": params.collect_count,
            "comment_count": params.comment_count,
            "share_count": params.share_count,
            "author_page": params.author_page,
            "url": params.url,
            "images": params.images
        }
    ];
    let records = [];
    for (let item of list) {
        let record = { "fields": "{}" };
        let fields = {};
        fields.笔记标题 = item.title;
        fields.博主 = item.author;
        fields.文案 = item.content;
        fields.发布时间 = item.publish_time;
        fields.地点 = item.location;
        fields.赞 = item.like_count;
        fields.收藏 = item.collect_count;
        fields.评论 = item.comment_count;
        fields.分享 = item.share_count;
        fields.博主主页 = item.author_page;
        fields.笔记链接 = item.url;
        fields.图片链接 = item.images.join(','); 
        record.fields = JSON.stringify(fields);
        records.push(record);
    }
    const ret = {
        key0: records
    };
    return ret;
}
```

#### 节点-插件-飞书多维表格-add_records

*   添加插件

![](img/f2376c222dbed2193be909558f1ba3b2.png)

*   搜索飞书多维表格，添加飞书多维表格下的add_records插件

![](img/31a168dbb795b42144dc8c56d6984839.png)

*   填入自己飞书多维表格的token和table_id，records选择代码中的key0

![](img/1192274c5f2620891ecd87fbed29b42b.png)

#### 节点-结束

工作流的最终节点，用于返回工作流运行后的结果信息，可以随意选择

![](img/9645ee9c77f9e7ab98c0983630286895.png)

#### 测试工作流

*   试运行，粘贴笔记链接测试（笔记链接：小红书APP-分享-复制链接）

![](img/6ed5d00316f97bb3cedd70418767449d.png)

*   运行成功后，正常情况多维表格就会更新数据。测试没问题后工作流需要发布

![](img/9dd3b7a2dfc901d93101fe080cb0e597.png)

#### 苹果和安卓手机已配置好的快捷指令

# 电脑上采集笔记

通过篡改猴插件去采集笔记，适用于 Chrome、Microsoft Edge、Safari、Opera Next 和 Firefox浏览器

有些人也会把篡改猴(Tampermonkey)称作油猴(Greasemonkey)，尽管后者只是一款仅适用于 Firefox 浏览器的浏览器扩展程序。

注意

先完成整个工作流的流程，测试扣子里API执行工作流是否正常，因为插件也是通过API执行工作流。

1.  浏览器安装Tampermonkey篡改猴插件

![](img/2e91331541a6842e05006d5c1a4f54b3.png)

![](img/d883327c97b6dd2f7f0278adcf987578.png)

1.  修改脚本

脚本如下：

脚本还需要修改，找到下面两项参数：

workflow_id修改为自己扣子工作流的ID

Authorization修改为自己扣子的token

```
workflow_id: '7499044907908628489'
'Authorization': 'Bearer pat_QhNwAtHQ1DC9m8o1MWDAp44t2JfV1ffmfBl6Bbz9Mi4Mn0goMYCAmThha01nS123'
```

1.  添加新脚本

复制粘贴脚本

![](img/41c5d19416ec2e3f0c418df451060f47.png)

![](img/87630c84b3f30e44d9d0d79ce8160584.png)

![](img/1ae0bc52f02dbcc809386c590fac3050.png)

1.  测试

![](img/186511691e70b23449393e379e031d36.png)

# 在小红书笔记工作流上添加采集视频

下图为小红书笔记采集的工作流，在这基础上添加个视频采集的插件

![](img/d934ff7e9f85603ec352501a953d9160.png)

1.  添加插件

![](img/f8e5a06041f900ff744482bc27878819.png)

1.  修改插件变量值

![](img/b3e7e9c862a6228605006ad1f280721c.png)

1.  代码节点

*   添加新变量，其值为视频链接地址

![](img/28fb892d1dfb47ac412dc0e8356af663.png)

![](img/4fe3d06988941c12bc9d1fd661208b91.png)

*   修改代码，把新变量添加上去

按照下图添加代码

![](img/2be54fde14f7ca7a9e2278a800d19370.png)

1.  发布工作流

![](img/94b26f76c0c2a1a29821107c1b1b750d.png)

1.  修改飞书多维表格

*   添加新字段-视频链接

用于放置采集到的视频链接

![](img/5a3740709e0231fec11904f20d9d7841.png)

*   添加新字段-视频

用于展示视频

![](img/3eb19df5427f7e8f287c3abf526d6be0.png)

*   测试

![](img/691145e7aeadb172ee5b3add750297f1.png)

# 常见问题

*   参数错误

![](img/0def0eda21a6bf87e3f26235bb8111d6.png)

*   变量类型错误

![](img/b6cc57cd48d5105d510682c35637df17.png)

*   需要授权（API执行工作流时出现）

![](img/69a2268a540df3e90350055f661d4a3e.png)

*   关于api执行工作流出现"code": 6039

![](img/3f80be2eadc9637be855c78047ca1c70.png)

解决方法

飞书开发文档（飞书插件出现问题时可以输入code代码查询）

https://open.feishu.cn/document/home/index