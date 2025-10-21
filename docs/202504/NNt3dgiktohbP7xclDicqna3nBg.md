# Cursor指导搭建云服务器攻略

> 来源：[https://vchedlrl7i.feishu.cn/docx/NNt3dgiktohbP7xclDicqna3nBg](https://vchedlrl7i.feishu.cn/docx/NNt3dgiktohbP7xclDicqna3nBg)

# 背景：云服务器前后配置有冲突

先前用cursor做web网站，照着claude指示安装了node 和pm2，给网站搭了一套环境；最近在ios航海，参照手册想配置宝塔面板，但配完nginx冲突。

我的想法是web和ios应用都想要开发，所以云服务器上希望能够配置一套兼容的环境，索性云服务器重装，借鉴手册、由cursor来指导完成云服务器部署。由于星球里关于配置云服务器的帖子比较少，分享此篇希望大家可以参考少踩坑。

本文适用于：计划为web/应用搭建服务器，但不知如何下手；先前配置过服务器，现在想重新再配一遍；准备好了服务器，想搭建api、配置web页面

# 零、重装系统服务器

![](img/97839ff5e635963c4a180ac61facd883.png)

操作系统选择Ubuntu（因为CentOS已停止维护，windows配置低的话用不了），填好登录密码

![](img/36a262d8b9e1e77a27a17475601f4940.png)

重装后打开终端Terminal

![](img/35f39f1ed52be7773b5858173841b9ef.png)

例如云服务器ip地址11.22.33.44，执行：

```
ssh root@11.22.33.44 -p 22
```

随后让你输入密码，就是刚设过的登录密码，输入后能连上云服务器，算是初步服务器ok

# 一、让cursor制定开发部署计划

## 发起prompt

```
我已经重装了服务器了，请结合当前ios应用的项目架构和需求，以及我还想做同一整套的web网站，你先帮我制定下开发部署计划吧，你可以提问我任何问题来确认方案细节
```

cursor回复：

### 核心需求确认

让我先确认几个关键点，以便制定更精确的计划：

1.  关于用户数据同步：您希望iOS用户和Web用户能共享同一个账户体系，实现数据跨平台同步，对吗？

1.  功能一致性要求：Web版是否需要实现iOS应用的全部功能，还是可以有所取舍？

1.  开发优先级：您希望先完善哪个平台？或者是同步开发？

1.  AI服务集成：您计划使用哪种AI服务（Claude、OpenAI等）来生成卡片内容？

1.  团队情况：是您个人开发还是有团队？这会影响开发策略和任务分配。

### 架构设计方案

基于目前了解的情况，我建议采用以下架构设计：

```
                  +----------------+
                  |   DNS服务     |
                  +-------+--------+
                          |
                          v
                  +----------------+
                  |   Nginx代理    |
                  +-------+--------+
                          |
           +-------------------------+
           |                         |
           v                         v
+---------------------+    +--------------------+
|   Web前端应用        |    |    API服务        |
| (React/Vue/Angular) |    | (Node.js+Express) |
+---------------------+    +--------+----------+
                                    |
                          +---------+---------+
                          |                   |
                          v                   v
                   +------------+     +---------------+
                   | 数据库      |     | AI服务集成     |
                   | (MongoDB/  |     | (Claude API/  |
                   |  MySQL)    |     |  OpenAI API)  |
                   +------------+     +---------------+
```

然后是为期数月的开发计划，忽略..

### 开发重点与挑战

1.  数据同步机制：确保iOS和Web用户数据实时同步

1.  一致的用户体验：保持两个平台的用户体验一致性

1.  AI服务可靠性：确保AI服务的稳定性和响应速度

1.  安全性考虑：保护用户数据和API安全

1.  性能优化：特别是在卡片生成和渲染方面

### 需要回答的问题

为了进一步完善计划，请回答以下问题：

1.  Web前端开发您偏好使用哪个框架？React、Vue.js还是其他？

1.  数据库选择上，您更倾向于使用关系型数据库(MySQL)还是文档型数据库(MongoDB)？

1.  AI服务集成方面，您已经有现成的API密钥或者有特定的服务商偏好吗？

1.  在用户认证方面，您是否需要支持第三方登录(如Google、Apple)？

1.  部署策略上，您希望采用持续集成/持续部署(CI/CD)还是手动部署？

1.  项目时间线有什么具体要求或限制吗？

根据您的回答，我可以进一步调整和细化这个计划。

## 一一回应，完善开发计划

web前端页面是找帖子用工具搭建的，什么框架并不清楚，直接问：

```
web前端我已经用工具做好网站页面了，如何确认它用的什么框架？
```

一番沟通确认是原生js没用框架;

数据库选择cursor判断选用mongodb:

![](img/ceab5af379ba9a83211ac10235b7a662.png)

3\. AI服务集成方面，我已经有现成的API密钥以及目标api站点

4\. 在用户认证方面，支持第三方登录好做吗？如果不复杂，可以添加苹果用户登录

5\. 部署策略上，您希望采用持续集成/持续部署(CI/CD)还是手动部署？这个我不太懂，你看着推荐下？

6\. 项目时间线有什么具体要求或限制吗？我要求越快越好

![](img/457fda440eca0284bf302564e59db7d7.png)

# 二、宝塔面板配置服务器

## 下载面板

打开终端，登录云服务器，根据系统版本执行不同的下载命令：

ubuntu:

```
wget -O install_panel.sh https://download.bt.cn/install/install_panel.sh && sudo bash install_panel.sh ed8484bec
```

或者linux通用安装脚本：

```
if [ -f /usr/bin/curl ];then curl -sSO https://download.bt.cn/install/install_panel.sh;else wget -O install_panel.sh https://download.bt.cn/install/install_panel.sh;fi;bash install_panel.sh ed8484bec
```

命令来源参考：https://www.bt.cn/new/download.html

安装完成后:

## 通过面板提供的URL、用户名和密码登录宝塔管理界面

![](img/ddce0c5c591ae444b2f44a19c54276b6.png)

复制面板地址浏览器打开，用给到的用户名密码登录

登录上去后，会推荐一键安装组合套装，航海手册中是选用的LNMP可以参考，我计划是根据cursor建议走，所以忽略一键安装，这里直接X掉

![](img/d162d2f9549b7dc7ade97ee516b1fc10.png)

![](img/6892cb06d5728e00e2db8b6ce8d02a58.png)

## 在软件商店中安装配置项

*   Nginx 1.18+ (推荐1.20) >> 选用了最新的1.24

*   Node.js 16+ (推荐16.14.0) >> 选用了较新的16.9.0

*   MongoDB 5+ >> 选用了7.0

*   PM2管理器 >> node.js管理器，内置 node.js + npm + nvm + pm2.! 将于2023年12月31日下架，如需使用请前往【网站->Node项目】

注：下载Node.js时，要先下个Node.js版本管理器，且安装node.js时会内置PM2，无需再下载PM2管理器了

![](img/d2dbc1b8f080754c7f4b28943ffca14c.png)

### 排查常见问题

Node.js版本不一致

如果您发现命令行显示的Node.js版本与面板设置的不一致:

1.在面板中检查Node.js路径(通常是/www/server/nodejs/bin/node)

2.在命令行中运行:

```
   # 查看系统中的node命令位置
   which node

   # 直接使用宝塔安装的Node.js
   /www/server/nodejs/v16.9.0/bin/node -v
```

更新系统路径优先级:

```
echo 'export PATH="/www/server/nodejs/v16.9.0/bin:$PATH"' >> ~/.bashrc

source ~/.bashrc
```

## 防火墙规则（云服务器设置安全组）

为何要配置安全组？顾名思义配置了更安全，可以简单理解为云服务器ip地址有很多端口，我们现在只允许其中某几个端口可以被访问。

像开始我们提到终端ssh 连接ip地址的命令里有个-p 22，就是用的22号端口，云服务器没有配置过管控、可以访问；以及安装宝塔面板后，提示请在安全组放行xxxxx端口，就是允许宝塔可以用 ip:33871端口来访问管理我们服务器。

我们配置安全组，就是设置哪些端口可以被如何访问：

操作步骤：去购置的云服务器界面找到安全组入口，直接新建：

![](img/e6b9a196b49270b316f5ba5fb186c68f.png)

![](img/faa84be4cb151490809611ea073ae7fc.png)

名称标签随意，给自己看的，名称可以写项目相关的名字，标签可以标明开放了哪些端口

建了安全组，点击配置规则，然后新建规则 ：

![](img/4ee04f4bc18d1d6395bbe14b2c3f80a9.png)

可以常用的协议和端口都有列，选择我们服务器所需要的端口配置上

![](img/ebbcff7aff88d65796eef5ec29945871.png)

现阶段，我们需要开放端口: 80(HTTP), 443(HTTPS), 22(SSH), 宝塔面板端口

配置完规则，再安全组中选到管理实例，新增关联，把安全组关联到我们的服务器，这样安全组就生效了

![](img/886d8912c700dceb17be456669993ef8.png)

# 三、配置web页面（ios忽略）

## 上传现有HTML页面

终端连接云服务器，创建网站目录结构:

```
mkdir -p /www/wwwroot/ainotecard/{api,public,logs,data,scripts}
chmod -R 755 /www/wwwroot/ainotecard
chown -R www:www /www/wwwroot/ainotecard
```

上传HTML文件:

1.1 使用宝塔面板的文件管理器上传文件到/www/wwwroot/ainotecard/public

![](img/bc726a1cd30a8f7fe7fe1524b1a87661.png)

1.2 上传index.html, generate.html和其他相关资源文件

可以拖拽文件上传

## 配置Nginx站点:

### 步骤1：创建必要的目录结构和文件

1.  在宝塔面板中打开文件管理器

1.  创建目录结构（如果尚未存在）

```
/www/wwwroot/ainotecard/api/
```

1.  在这目录下新建文件server.js，填入以下内容

```
// 基础Express服务器配置
const express = require('express');
const path = require('path');
const app = express();
const PORT = process.env.PORT || 3000;

// 中间件配置
app.use(express.json());
app.use(express.static(path.join(__dirname, '../public')));

// 测试路由
app.get('/api/test', (req, res) => {
  res.json({ message: '服务器运行正常' });
});

// 启动服务器
app.listen(PORT, () => {
  console.log(`服务器运行在端口: ${PORT}`);
});
```

1.  同样在/www/wwwroot/ainotecard/api/目录下，新建文件：package.json

```
{
  "name": "ainotecard-api",
  "version": "1.0.0",
  "description": "AINoteCard API服务",
  "main": "server.js",
  "scripts": {
    "start": "node server.js"
  },
  "dependencies": {
    "express": "^4.18.2"
  }
}
```

### 步骤2：安装基本依赖

终端ssh连接云服务器：

先检查node版本：如果版本低于 14.0.0，我们需要更新 Node.js到16

```
node -v

# 安装 nvm
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.1/install.sh | bash
source ~/.bashrc

# 安装 Node.js 16
nvm install 16
nvm use 16
```

```
cd /www/wwwroot/ainotecard/api
```

```
apt install npm
```

```
npm install
```

### 步骤3：再次添加Node项目

现在已经创建了基本的文件结构，添加Node项目：

1.  项目名称：ainotecard-api

1.  Node版本：v16.9.0

1.  启动文件：/www/wwwroot/ainotecard/api/server.js

1.  运行目录：/www/wwwroot/ainotecard/api

![](img/970e727dcadc45ef729373752342dc5f.png)

### 步骤4：测试基本功能

项目添加完成后，可以启动它测试基础功能：

1.  在Node项目管理页面，找到您刚创建的项目

1.  点击"启动"按钮

1.  等待状态变为"正在运行"

1.  打开浏览器访问：http://服务器IP:3000/api/test

1.  应该看到JSON响应：{"message":"服务器运行正常"}

![](img/9b265f42c39c2907ed3df83a91e7fc82.png)

注意：如果浏览器访问不到，原因是这里我们新增了3000端口作为测试，需要安全组里为3000打开

![](img/5d8d0377d06f288bc817ac7bd3146362.png)

添加完后，终端连接云服务器，查看防火墙设置：

```
# 查看UFW防火墙状态
sudo ufw status

# 如果3000端口未开放，可以添加规则
sudo ufw allow 3000/tcp
```

![](img/c32fc2fd70adb918a81ffff271dd8d65.png)

这样再浏览器继续打开 http://ip:3000/api/test 就正常了：

![](img/32f28ced565c896c07f427cb7c6a5f90.png)

1.  通过域名：http://域名:3000/api/test

1.  通过IP：http://ip:3000/api/test

两种方式都成功返回了预期的JSON响应：{"message":"服务器运行正常"}，这意味着Node.js服务正在正确运行并可以从外部访问。

### 步骤5：设置Nginx反向代理

1.  在宝塔面板界面中，选择"网站"-"PHP项目"-"添加站点"，弹出的表单中填写域名，php版本纯静态，点击确定

![](img/a479af1057ea5f4a67b77d3cf686c441.png)

1.  在网站列表中找到刚创建的站点，点击右侧的"设置"按钮，在弹出的设置页面中，找到左侧菜单栏中的"反向代理"选项（如果没有直接看到，可能需要点击"更多功能"或滚动查看）

![](img/2f72f3a3df749b05b58ecd7382a5a89a.png)

1.  点击"添加反向代理"按钮，打开高级功能，在表单中填写以下信息：

*   代理名称：api（用于标识这个代理配置）

*   目标URL：http://127.0.0.1:3000（您的Node.js服务地址）

*   发送域名：保持默认值$host

*   代理目录：/api（这表示所有访问/api的请求都会被转发到Node.js服务）

其他选项保持默认值，点击"提交"按钮保存配置

![](img/39c226b308898c3cac22631b9db4b85c.png)

这样配置后，所有访问http://您的域名/api/xxx的请求都会被转发到http://127.0.0.1:3000/api/xxx，也就是您的Node.js服务。注意这里，是访问域名的请求会被转发过去，http://ip/api/xxx 的按现在配置并不会，也不需要关注

浏览器访问 http://域名/api/test，说明反向代理配置成功；宝塔面板配置反向代理时默认只对域名生效，所以http://ip/api/test 并不会被反向代理到相应端口，这个坑我让ai排查很久都没定位到原因，求助到航海群2位圈友一眼看出问题来了。

![](img/35ae0dab67cbf5e5f93ce7b5d142fc9d.png)

# 四、服务端基础框架搭建

## 安装依赖包、创建项目目录结构

```
cd /www/wwwroot/ainotecard/api
npm install express mongoose cors dotenv body-parser jsonwebtoken bcrypt
mkdir -p models routes controllers middleware config
touch .env config/database.js server.js
```

## 创建并编辑 .env 文件：

```
cat > .env << EOF
PORT=3000
MONGODB_URI=mongodb://localhost:27017/ainotecard
JWT_SECRET=$(openssl rand -base64 32)
EOF
```

## 创建数据库连接配置文件：

```
cat > config/database.js << EOF
const mongoose = require('mongoose');
require('dotenv').config();

// 数据库连接选项
const options = {
  useNewUrlParser: true,
  useUnifiedTopology: true
};

// 连接到数据库
const connectDB = async () => {
  try {
    await mongoose.connect(process.env.MONGODB_URI, options);
    console.log('数据库连接成功');
  } catch (err) {
    console.error('数据库连接失败:', err.message);
    process.exit(1);
  }
};

module.exports = connectDB;
EOF
```

## 创建主服务器文件 server.js：

```
cat > server.js << EOF
// 导入必要的包
require('dotenv').config();
const express = require('express');
const cors = require('cors');
const bodyParser = require('body-parser');
const connectDB = require('./config/database');

// 初始化Express应用
const app = express();
const PORT = process.env.PORT || 3000;

// 连接数据库
connectDB();

// 中间件
app.use(cors());
app.use(bodyParser.json());

// 测试路由 - 保留现有功能
app.get('/api/test', (req, res) => {
  res.json({ message: '服务器运行正常' });
});

// 路由占位 - 将在后续步骤实现
// app.use('/api/auth', require('./routes/auth'));
// app.use('/api/cards', require('./routes/cards'));

// 错误处理中间件
app.use((err, req, res, next) => {
  console.error(err.stack);
  res.status(500).json({ message: '服务器错误', error: err.message });
});

// 启动服务器
app.listen(PORT, () => {
  console.log(\`服务器运行在端口: \${PORT}\`);
});
EOF
```

## 创建用户模型文件。请执行以下命令：

```
cat > models/User.js << EOF
const mongoose = require('mongoose');
const bcrypt = require('bcrypt');

// 用户模式定义
const userSchema = new mongoose.Schema({
  username: {
    type: String,
    required: true,
    unique: true,
    trim: true,
    minlength: 3
  },
  email: {
    type: String,
    required: true,
    unique: true,
    trim: true,
    lowercase: true
  },
  password: {
    type: String,
    required: true,
    minlength: 6
  },
  createdAt: {
    type: Date,
    default: Date.now
  }
});

// 保存前加密密码
userSchema.pre('save', async function(next) {
  // 只有当密码被修改时才加密
  if (!this.isModified('password')) return next();

  try {
    // 生成盐
    const salt = await bcrypt.genSalt(10);
    // 生成加密密码
    this.password = await bcrypt.hash(this.password, salt);
    next();
  } catch (error) {
    next(error);
  }
});

// 验证密码的方法
userSchema.methods.comparePassword = async function(candidatePassword) {
  return await bcrypt.compare(candidatePassword, this.password);
};

// 创建模型
const User = mongoose.model('User', userSchema);

module.exports = User;
EOF
```

## 创建认证中间件，用于验证 JWT 令牌：

```
cat > middleware/auth.js << EOF
const jwt = require('jsonwebtoken');
require('dotenv').config();

// 认证中间件：验证JWT令牌
const auth = (req, res, next) => {
  // 从请求头获取令牌
  const token = req.header('Authorization')?.replace('Bearer ', '');

  // 如果没有令牌，返回401未授权
  if (!token) {
    return res.status(401).json({ message: '无访问令牌，授权失败' });
  }

  try {
    // 验证令牌
    const decoded = jwt.verify(token, process.env.JWT_SECRET);

    // 将用户信息添加到请求对象
    req.user = decoded;
    next();
  } catch (error) {
    res.status(401).json({ message: '令牌无效', error: error.message });
  }
};

module.exports = auth;
EOF
```

## 创建认证路由：

```
cat > routes/auth.js << EOF
const express = require('express');
const jwt = require('jsonwebtoken');
const User = require('../models/User');
const router = express.Router();

// 注册新用户
router.post('/register', async (req, res) => {
  try {
    const { username, email, password } = req.body;

    // 检查用户是否已存在
    const userExists = await User.findOne({ 
      $or: [{ email }, { username }] 
    });

    if (userExists) {
      return res.status(400).json({ message: '用户已存在' });
    }

    // 创建新用户
    const user = new User({
      username,
      email,
      password
    });

    // 保存用户（密码会在save前被加密）
    await user.save();

    // 生成JWT令牌
    const token = jwt.sign(
      { id: user._id, username: user.username }, 
      process.env.JWT_SECRET,
      { expiresIn: '30d' }
    );

    // 返回成功消息和令牌
    res.status(201).json({
      message: '用户注册成功',
      token,
      user: {
        id: user._id,
        username: user.username,
        email: user.email
      }
    });
  } catch (error) {
    res.status(500).json({ message: '服务器错误', error: error.message });
  }
});

// 用户登录
router.post('/login', async (req, res) => {
  try {
    const { email, password } = req.body;

    // 查找用户
    const user = await User.findOne({ email });

    // 如果用户不存在
    if (!user) {
      return res.status(400).json({ message: '邮箱或密码不正确' });
    }

    // 验证密码
    const isMatch = await user.comparePassword(password);

    // 如果密码不匹配
    if (!isMatch) {
      return res.status(400).json({ message: '邮箱或密码不正确' });
    }

    // 生成JWT令牌
    const token = jwt.sign(
      { id: user._id, username: user.username }, 
      process.env.JWT_SECRET,
      { expiresIn: '30d' }
    );

    // 返回成功消息和令牌
    res.json({
      message: '登录成功',
      token,
      user: {
        id: user._id,
        username: user.username,
        email: user.email
      }
    });
  } catch (error) {
    res.status(500).json({ message: '服务器错误', error: error.message });
  }
});

module.exports = router;
EOF
```

## 更新 server.js 文件，添加认证路由：

```
nano server.js
```

找到"// app.use('/api/auth', require('./routes/auth'));" 删除前面的注释符“//”

```
app.use('/api/auth', require('./routes/auth'));
```

然后按 Ctrl+X 退出，按 Y 保存，然后按 Enter 确认。

## 创建卡片模型：

```
cat > models/Card.js << EOF
const mongoose = require('mongoose');

// 卡片模式定义
const cardSchema = new mongoose.Schema({
  user: {
    type: mongoose.Schema.Types.ObjectId,
    ref: 'User',
    required: true
  },
  title: {
    type: String,
    required: true,
    trim: true
  },
  content: {
    type: String,
    required: true
  },
  tags: [{
    type: String,
    trim: true
  }],
  category: {
    type: String,
    trim: true,
    default: '未分类'
  },
  isAIGenerated: {
    type: Boolean,
    default: false
  },
  createdAt: {
    type: Date,
    default: Date.now
  },
  updatedAt: {
    type: Date,
    default: Date.now
  }
});

// 更新前更新时间
cardSchema.pre('save', function(next) {
  if (this.isModified()) {
    this.updatedAt = Date.now();
  }
  next();
});

// 创建模型
const Card = mongoose.model('Card', cardSchema);

module.exports = Card;
EOF
```

## 创建卡片路由

```
cat > routes/cards.js << EOF
const express = require('express');
const router = express.Router();
const Card = require('../models/Card');
const auth = require('../middleware/auth');

// 获取当前用户的所有卡片
// GET /api/cards
router.get('/', auth, async (req, res) => {
  try {
    const cards = await Card.find({ user: req.user.id }).sort({ createdAt: -1 });
    res.json(cards);
  } catch (error) {
    res.status(500).json({ message: '服务器错误', error: error.message });
  }
});

// 获取单个卡片
// GET /api/cards/:id
router.get('/:id', auth, async (req, res) => {
  try {
    const card = await Card.findOne({ 
      _id: req.params.id, 
      user: req.user.id 
    });

    if (!card) {
      return res.status(404).json({ message: '卡片未找到' });
    }

    res.json(card);
  } catch (error) {
    res.status(500).json({ message: '服务器错误', error: error.message });
  }
});

// 创建新卡片
// POST /api/cards
router.post('/', auth, async (req, res) => {
  try {
    const { title, content, tags, category, isAIGenerated } = req.body;

    const newCard = new Card({
      user: req.user.id,
      title,
      content,
      tags: tags || [],
      category: category || '未分类',
      isAIGenerated: isAIGenerated || false
    });

    const card = await newCard.save();
    res.status(201).json(card);
  } catch (error) {
    res.status(500).json({ message: '服务器错误', error: error.message });
  }
});

// 更新卡片
// PUT /api/cards/:id
router.put('/:id', auth, async (req, res) => {
  try {
    const { title, content, tags, category } = req.body;

    // 构建更新对象
    const cardFields = {};
    if (title) cardFields.title = title;
    if (content) cardFields.content = content;
    if (tags) cardFields.tags = tags;
    if (category) cardFields.category = category;

    // 查找卡片并更新
    let card = await Card.findOne({ 
      _id: req.params.id, 
      user: req.user.id 
    });

    if (!card) {
      return res.status(404).json({ message: '卡片未找到' });
    }

    card = await Card.findByIdAndUpdate(
      req.params.id,
      { $set: cardFields },
      { new: true }
    );

    res.json(card);
  } catch (error) {
    res.status(500).json({ message: '服务器错误', error: error.message });
  }
});

// 删除卡片
// DELETE /api/cards/:id
router.delete('/:id', auth, async (req, res) => {
  try {
    const card = await Card.findOne({ 
      _id: req.params.id, 
      user: req.user.id 
    });

    if (!card) {
      return res.status(404).json({ message: '卡片未找到' });
    }

    await Card.findByIdAndRemove(req.params.id);

    res.json({ message: '卡片已删除' });
  } catch (error) {
    res.status(500).json({ message: '服务器错误', error: error.message });
  }
});

module.exports = router;
EOF
```

## 继续更新server.js

```
nano server.js
找到// app.use('/api/cards', require('./routes/cards'));
改为
app.use('/api/cards', require('./routes/cards'));
```

## 创建简单的AI服务模块

```
mkdir -p services
cat > services/ai.js << EOF
// AI服务 - 简单实现，未连接实际AI API
class AIService {
  /**
   * 生成笔记卡片
   * @param {string} prompt - 用户输入的提示
   * @param {string} template - 卡片模板类型
   * @returns {Promise} - 生成的卡片内容
   */
  static async generateCard(prompt, template = 'standard') {
    // 这里应该连接到真实的AI API
    // 目前使用简单的模拟实现

    // 模拟API延迟
    await new Promise(resolve => setTimeout(resolve, 1000));

    // 根据模板生成不同结构的内容
    let title, content;

    switch (template) {
      case 'question':
        title = \`关于: \${prompt.substring(0, 30)}\`;
        content = \`问题: \${prompt}\\n\\n答案: 这是对"\${prompt}"的回答。详细解释...\\n\\n扩展思考: 这里是一些延伸的相关知识点。\`;
        break;

      case 'summary':
        title = \`摘要: \${prompt.substring(0, 30)}\`;
        content = \`原文: \${prompt}\\n\\n摘要: 这是对上述内容的简明摘要。包含主要观点和关键信息。\\n\\n关键点:\\n- 第一个要点\\n- 第二个要点\\n- 第三个要点\`;
        break;

      default: // standard
        title = prompt.substring(0, 30) + '...';
        content = \`${prompt}\\n\\n这里是生成的笔记内容。包含了关键概念、解释和例子。\\n\\n关键词: 关键词1, 关键词2, 关键词3\`;
    }

    return {
      title,
      content,
      isAIGenerated: true,
      tags: ['AI生成', template],
      category: '自动生成'
    };
  }
}

module.exports = AIService;
EOF
```

## 创建AI生成卡片路由

```
cat > routes/ai.js << EOF
const express = require('express');
const router = express.Router();
const Card = require('../models/Card');
const auth = require('../middleware/auth');
const AIService = require('../services/ai');

// 生成AI卡片
// POST /api/ai/generate
router.post('/generate', auth, async (req, res) => {
  try {
    const { prompt, template } = req.body;

    if (!prompt) {
      return res.status(400).json({ message: '提示内容不能为空' });
    }

    // 调用AI服务生成卡片内容
    const cardData = await AIService.generateCard(prompt, template);

    // 创建新卡片
    const newCard = new Card({
      user: req.user.id,
      title: cardData.title,
      content: cardData.content,
      tags: cardData.tags,
      category: cardData.category,
      isAIGenerated: true
    });

    const card = await newCard.save();
    res.status(201).json(card);
  } catch (error) {
    res.status(500).json({ message: 'AI生成失败', error: error.message });
  }
});

module.exports = router;
EOF
```

## 更新 server.js 文件，添加AI路由：

```
nano server.js
在卡片路由后添加：
app.use('/api/ai', require('./routes/ai'));
```

## 测试api

```
测试基础路由：
curl http://www.ainotecard.com/api/test
{"message":"服务器运行正常"}

注册新用户：
curl -X POST http://www.ainotecard.com/api/auth/register -H "Content-Type: application/json" -d '{"username":"testuser","email":"test@example.com","password":"password123"}'
{"message":"用户注册成功","token":"eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpZCI6IjY3ZTJjZGQ2ZmI1ODYwY2RhOThhZGMyNiIsInVzZXJuYW1lIjoidGVzdHVzZXIiLCJpYXQiOjE3NDI5MTcwNzgsImV4cCI6MTc0NTUwOTA3OH0.S2NHeyIgbFMgVjTY0UquE6pYtZrMLmtjjOmxFMj1P14","user":{"id":"67e2cdd6fb5860cda98adc26","username":"testuser","email":"test@example.com"}}

尝试登录：
curl -X POST http://www.ainotecard.com/api/aun \logi 
>   -H "Content-Type: application/json" \
>   -d '{"email":"test@example.com","password":"password123"}'
{"message":"登录成功","token":"eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpZCI6IjY3ZTJjZGQ2ZmI1ODYwY2RhOThhZGMyNiIsInVzZXJuYW1lIjoidGVzdHVzZXIiLCJpYXQiOjE3NDI5MTcxMDIsImV4cCI6MTc0NTUwOTEwMn0.56xTLFmO6nz9E_j0kBuWlWfrogux_ZQRpsCbGBOiI4U","user":{"id":"67e2cdd6fb5860cda98adc26","username":"testuser","email":"test@example.com"}}

登录成功后，您将收到一个包含 token 的 JSON 响应。请保存这个 token，我们将在后续请求中使用它。

使用 token 创建一个卡片：
curl -X POST http://www.ainotecard.com/api/cards \
>   -H "Content-Type: application/json" \
>   -H "Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpZCI6IjY3ZTJjZGQ2ZmI1ODYwY2RhOThhZGMyNiIsInVzZXJuYW1lIjoidGVzdHVzZXIiLCJpYXQiOjE3NDI5MTcxMDIsImV4cCI6MTc0NTUwOTEwMn0.56xTLFmO6nz9E_j0kBuWlWfrogux_ZQRpsCbGBOiI4U" \
>   -d '{"title":"测试卡片","content":"这是一个测试卡片的内容","tags":["测试","示例"]}'
{"user":"67e2cdd6fb5860cda98adc26","title":"测试卡片","content":"这是一个测试卡片的内容","tags":["测试","示例"],"category":"未分类","isAIGenerated":false,"_id":"67e2cf29fb5860cda98adc29","createdAt":"2025-03-25T15:43:37.241Z","updatedAt":"2025-03-25T15:43:37.242Z","__v":0}

获取所有卡片：
curl -H "Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpZCI6IjY3ZTdGVzdHVzZXIiLCJpYXQiOjE3NDI5MTcxMDIsImV4cCI6MTc0NTUwOTEwMn0.56xTLFmO6nz9E_j0kBuWlWfrogux_ZQRpsCbGBOiI4U" \
>   http://www.ainotecard.com/api/cards
[{"_id":"67e2cf29fb5860cda98adc29","user":"67e2cdd6fb5860cda98adc26","title":"测试卡片","content":"这是一个测试卡片的内容","tags":["测试","示例"],"category":"未分类","isAIGenerated":false,"createdAt":"2025-03-25T15:43:37.241Z","updatedAt":"2025-03-25T15:43:37.242Z","__v":0}]

使用AI生成卡片的命令如下：
curl -X POST http://www.ainotecard.com/api/ai/generate \
>   -H "Content-Type: application/json" \
>   -H "Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpZCI6IjY3ZTJjZGQ2ZmI1ODYwY2RhOThhZGMyNiIsInVzZXJuYW1lIjoidGVzdHVzZXIiLCJpYXQiOjE3NDI5MTc5MDMsImV4cCI6MTc0NTUwOTkwM30.2GrrqC3Sl30ovU2f58ca4SyKQ0plRFrVUNWXu1tqdo8" \
>   -d '{"prompt":"人工智能的基础知识","template":"summary"}'
{"user":"67e2cdd6fb5860cda98adc26","title":"摘要: 人工智能的基础知识","content":"原文: 人工智能的基础知识\n\n摘要: 这是对上述内容的简明摘要。包含主要观点和关键信息。\n\n关键点:\n- 第一个要点\n- 第二个要点\n- 第三个要点","tags":["AI生成","summary"],"category":"自动生成","isAIGenerated":true,"_id":"67e2d12bfb5860cda98adc2d","createdAt":"2025-03-25T15:52:11.362Z","updatedAt":"2025-03-25T15:52:11.363Z","__v":0}
```

![](img/53f980fa9af2f89958493b578c7392ca.png)

## 汇总：当前API端点:

1.  GET /api/test - 测试服务器是否正常运行

1.  POST /api/auth/register - 注册新用户

1.  POST /api/auth/login - 用户登录

1.  GET /api/cards - 获取用户的所有卡片

1.  GET /api/cards/:id - 获取特定卡片

1.  POST /api/cards - 创建新卡片

1.  PUT /api/cards/:id - 更新卡片

1.  DELETE /api/cards/:id - 删除卡片

1.  POST /api/ai/generate - 使用AI生成卡片

# 五、配置SSL证书

调试api接口时发现：

```
curl http://域名/api/test
{"message":"服务器运行正常"}

但是curl https://域名/api/test
curl: (7) Failed to connect to 域名 port 443: Connection refused
```

HTTP服务已经正常工作了，现在需要配置HTTPS支持，那就需要配置SSL证书

宝塔面板-网站-找到目标网站站点-SSL证书未部署

![](img/454900b459e44a033367688531db35af.png)

点开后，Let's Encrypt-申请证书

![](img/4b3e3a9faffdd6484af9f9b8461c5a97.png)

选择文件验证-申请证书：

![](img/2d8eeab217bd99d5eae64796bc212af2.png)

选择强制HTTPS，添加到期提醒（证书有效期90天，到期前来这里续签），保存

![](img/78d4328a6e51ae317a23d1a566a139d2.png)

配置完SSL证书，再测试https端就OK了

```
curl https://域名/api/test
{"message":"服务器运行正常"}
```

# 六、总结

1、cursor除了写代码，指导配置环境、部署代码也是非常专业的，尤其是代码cursor写的，如何做相应的服务器配置对它来说那是轻松拿捏，你只管夸它、有问题甩给它，让它输出就完事了！

2、但有些问题，比如宝塔面板的默认设置，cursor是很难感知到的，这就会导致有些问题ai来来回回也没头绪，这时候要积极向专业经验人士求助。比如nginx反向代理的问题拉着ai排查2个小时没能搞定，求助到航海群里，2位圈友稍做了解就定位出根因了。

3、制定计划、分模块、分步骤执行，用文件记录存档，能让cursor用起来更加得心应手。