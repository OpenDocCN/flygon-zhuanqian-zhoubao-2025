# 用coze搭建一个低配版的吐槽大会

> 来源：[https://gida8fb9mrg.feishu.cn/docx/BsPmdnUV6owzozx6d2Uc0aMXnSd](https://gida8fb9mrg.feishu.cn/docx/BsPmdnUV6owzozx6d2Uc0aMXnSd)

在精华帖看到了用AI工具从0-1的吐槽网站：https://t.zsxq.com/dBAYN

于是想到用coze实现一个，现在coze不止可以搭建智能体，还能搭建应用。

最终的低配版的吐槽大会长这样：

![](img/9542e7f94de35d76eb2c1b82a3a69a34.png)

coze体验地址：https://www.coze.cn/s/ifPYNLNw/

搭建步骤：

1.  访问coze地址：https://www.coze.cn/space/

1.  点击右上角的创建按钮

1.  创建应用

![](img/baf1c1ee3bb1bc647607bee7fff4837f.png)

1.  选择应用模板，我是使用了空白模板，大家可以根据自己的需求选择

![](img/aae21fb0f1dcc9850a8ee304aad154a8.png)

1.  填写应用信息

![](img/f4fc0af38837775a806217e2d7ba357c.png)

1.  创建工作流

![](img/317ef20e17215dbcff15b0dbfb7d827d.png)

1.  工作流其实只加了一个大模型和提示词

![](img/35405977838b99f333ffdd50eaec69f9.png)

配置开始节点

![](img/bd4d4ca80ee7fc2267ffeb515ecf3cba.png)

配置大模型节点

![](img/54c4c82d6d1d2395be5710da4c4d762f.png)

```
你是一个致力于创作反心灵鸡汤的灵魂段子手​  
#根据{{input}}创作对应的反心灵鸡汤​  
#采用具有强烈讽刺意味的表达​  
#风格应当毒舌、辛辣、讽刺​  
#内容应当深刻、直击灵魂​  
#内容应当精简，不超过50字​  
#当{{input}}为空时，吐槽用户这个行为​  
#当{{input}}涉及政治、党派、种族歧视等敏感内容时，拒绝创作，并吐槽用户的钓鱼行为​  
#请尽情挥洒你的创造力
```

配置结束节点

![](img/60f091b94295dd39c9837fd2a923e780.png)

1.  配置用户界面

![](img/4cb2e9074cba5c1bc05305eaf47b1bca.png)

选择模板，也可以不选择

![](img/e034ec8d4a4c5da4cb7a30589e0ad249.png)

1.  增加组件，这次用到输入、输出、按钮三个组件

![](img/e9721889c5f18d6c5abbba0c55021621.png)

1.  配置组件属性

配置输入组件

![](img/3beed29b30561f124696fa294178d7c5.png)

配置输出组件

![](img/87937869935ad40ceff19cd9b8513826.png)

配置按钮属性和事件

![](img/48efe4039b651094a8bf90c1cf31d8d9.png)

![](img/3d96ed21c8adcf97194e900378459c30.png)

1.  发布

根据需求可以发布为不同类型

![](img/cefe95c5f0dfc86b41dc2cbdef4e714b.png)

![](img/7604884e6ba68b16fddf99254bd56c18.png)

![](img/377611dd718cec004e14ff53c8809a92.png)

![](img/f89c2cdef18eff5d19a1262290ed36cb.png)