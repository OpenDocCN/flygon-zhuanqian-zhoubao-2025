# 图像API工作流3_OpenAI（全能4种）

> 来源：[https://aigcstudy.feishu.cn/docx/L2i3d2mFQo6CTuxSf30cXZZjnHc](https://aigcstudy.feishu.cn/docx/L2i3d2mFQo6CTuxSf30cXZZjnHc)

### ComfyUI 工作流使用 OpenAI 三种最新生图模型自动批量出图（保姆级教程+工作流下载）

# GPT-Image-1 工作流

OpenAI 在今天发布了 GPT-Image-1 API（与 ChatGPT 4o 图像模型相同的模型）。ComfyUI 现在支持通过原生的 API 节点（测试版）来使用 OpenAI 最新的图像生成模型，让你无需复杂的 API 密钥，直接在 ComfyUI 中访问最先进的功能。而且可以使用微信或者支付宝直接充值使用OpenAI GPT-Image-1，OpenAI DALL·E 3，OpenAI DALL·E 2三个不同的生成图片模型，无需CHATGPT账号。下面来来详细介绍ComfyUI 工作流中使用 OpenAI 三种生图模型 批量出图保姆级教程。

### 为啥用ComfyUI？核心是批量自动生成图片 且可以结合其他AI视频模型，AI音频模型，AI数字人模型，共同制作AI视频。

![](img/ae627f126b8b72ccf80593295f421d31.png)

### OpenAI GPT-Image-1 节点支持

*   文生图

*   图生图

*   多图生图

*   图像编辑功能（通过蒙版进行修复绘制）

## 文生图工作流

1.  文生图像工作流对应的工作流非常简单，你只需要加载 OpenAI GPT-Image-1 节点，在 prompt 节点中输入你想要生成的图像的描述，连接一个 保存图像（Save Image） 节点。工作流如图所示。提示词cat stickers（猫贴纸）

![](img/dc87c87d3b3a315ddae90fe8904f7d5c.png)

1.  运行工作流，生成结果

![](img/8d120e4c67fc3df20323515b0bedc624.png)

1.  参数详解

1.  积分消耗

## 图生图工作流

1.  图生图工作流中，我们使用 OpenAI GPT-Image-1 节点生成图像，并使用 加载图像（Load Image） 节点加载输入的图像，然后连接到 OpenAI GPT-Image-1 节点的 image 输入中，工作流如图所示。提示词turn this image into ghibli style（转换图片为吉卜力风格）

![](img/33c79c431c19aa03e47a0399eaf9ed4c.png)

你也可以这样，使用中文提示词帮我改成适合激光镭雕的黑白线稿等等

![](img/1fdc257166e8f001eec01b87c73429b1.png)

1.  我们将用下面的图片作为输入。

![](img/66a9a8b95d364e8d8cb9acf737cd77d3.png)

1.  运行工作流，生成结果

![](img/015c0326f18f55109a37c429416c26e6.png)

1.  积分消耗

## 多图生图工作流

1.  图生图工作流中，我们使用 OpenAI GPT-Image-1 节点生成图像，并使用 多个加载图像（Load Image） 节点加载输入的图像，然后使用图像组合批次把输入的两个图结合起来，最后然后连接到 OpenAI GPT-Image-1 节点的 image 输入中，工作流如图所示。提示词Put the hat on the cat's head and turn into ghibli style（给猫带上帽子并转换图片为吉卜力风格）

![](img/f3e530c6d2c5f7615f4c2a1c501a5c4c.png)

你也可以这样使用中文提示词，让猫带上帽子，让图1角色坐在夜间的路边咖啡馆喝咖啡，日本动漫风格，确保2个图片的原始特征保持一致不能改变。

![](img/9596174b95fd78797556bcd4e5dee630.png)

1.  运行工作流，生成结果

![](img/953d626675445503bf6607ac7040e88f.png)

![](img/97a44ca69832e69108d75913fc26f6ac.png)

1.  积分消耗

## 局部重绘工作流

1.  GPT-Image-1 节点也支持图像编辑功能，允许您使用蒙版指定要替换的区域，下面是一个简单的局部重绘工作流示例，其实你发现和图生图工作流一模一样。区别在于与图生图工作流相比，我们在Load Image中通过右键菜单使用 蒙版编辑器（MaskEditor） 并绘制蒙版，然后连接到 OpenAI GPT-Image-1 节点的 mask 输入中，来完成对应工作流。

### 注意事项

*   当输入大尺寸图片时，节点会自动将图像缩小到合适的尺寸

*   API 返回的 URL 是短期有效的，请确保及时保存需要的结果

![](img/4264311d4f9b24f02d721baa4b90bcf0.png)

1.  我们在输入图片右键，选择在遮罩编辑器中打开。

![](img/9aec2fa6ac1da3ef45e4d0938fae98fb.png)

1.  遮罩编辑中添加遮罩，点击保存。

![](img/765f71a34e69feb14c0e274c11ee2333.png)

1.  添加完遮罩后，对应工作流入图所示，提示词为Let the cat hold a big fish（让小猫举着一个大鱼）

![](img/690cd9ae41097c8694fa1ea73a7443a9.png)

1.  运行工作流，生成结果

![](img/0f1ff28d7ec9b592d0f51b2147d2e523.png)

1.  积分消耗

# DALL·E 2 工作流

![](img/f1cfbb3d8e846bd181ceab862131de75.png)

### 这个节点支持

*   文生图

*   图像编辑功能（通过蒙版进行修复绘制）

*   不支持图生图

*   不支持多图生图

## 文生图工作流

1.  你只需要在加载 OpenAI DALL·E 2 节点后，在 prompt 节点中输入你想要生成的图像的描述，并连接一个 保存图像（Save Image） 节点，然后运行工作流即可

![](img/e4ad1e7b25535442c09e46ea336f0068.png)

1.  运行工作流，生成图片

![](img/5a2ccb9f6742f62763c543d3240f2a34.png)

1.  参数详解

1.  积分消耗

## 局部重绘工作流

1.  DALL·E 2 支持图像编辑功能，允许您使用蒙版指定要替换的区域，下面是一个简单的局部重绘工作流示例，使用加载图像（Load Image）节点加载图像，在OpenAI DALL·E 2 节点 image 输入中连接加载的图像，编辑 prompt 节点的提示词，OpenAI DALL·E 2 节点 mask 输入中连接蒙版

注意事项

*   如果您想使用图像编辑功能，必须同时提供图像和蒙版（缺一不可）

*   蒙版和图像必须大小相同

*   当输入大尺寸图片时，节点会自动将图像缩小到合适的尺寸

*   API 返回的 URL 是短期有效的，请确保及时保存需要的结果

![](img/f712a75a89dc54ca0e6da16010b62e13.png)

1.  我们将使用下面的图片作为输入

![](img/878a6390729c13f26150aa550d211ae9.png)

1.  在加载图像节点中右键，选择 遮罩编辑器（MaskEditor）

![](img/1ea5b3d24e98bc840c5aa3ddfef0b749.png)

1.  在遮罩编辑器中，使用画笔绘制你想要重绘的区域

![](img/b989488e59389324f17d003ce68f7f8d.png)

1.  运行工作流，生成结果

![](img/e25997ee6ea6955298e9a8fcb89147f1.png)

积分消耗

# DALL·E 3 工作流

![](img/bb86024fe6614b51a317c848f62d68c2.png)

### 这个节点支持

*   文生图

*   不支持图生图

*   不支持多图生图

*   不支持图像编辑功能

## 文生图工作流

1.  文生图像工作流对应的工作流非常简单，你只需要加载 OpenAI DALL·E 3 节点，在 prompt 节点中输入你想要生成的图像的描述，连接一个 保存图像（Save Image） 节点。工作流如图所示。提示词A fox running in the snow, with snowflakes swirling around it. The background features coniferous forests and mountains, and there is the evening light.（一只狐狸在雪地里奔跑，雪花在它周围盘旋。背景是针叶林和山脉，还有傍晚的光线） 0.55

![](img/28e095e177961b9645904269f500cf04.png)

1.  运行工作流，生成结果

![](img/caa77a168d6f800027a4981477b97959.png)

1.  参数详解

1.  积分消耗

# 下载工作流

https://gitee.com/lailai666/comfyui_workflow/blob/master/API%20PIC/%E3%80%90API%E5%9B%BE%E5%83%8F%E3%80%91openai.json