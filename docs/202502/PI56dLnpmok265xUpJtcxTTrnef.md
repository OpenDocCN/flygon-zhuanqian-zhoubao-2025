# cursor开发自动化工具--闲鱼篇

> 来源：[https://yawxxwt3iq1.feishu.cn/docx/PI56dLnpmok265xUpJtcxTTrnef](https://yawxxwt3iq1.feishu.cn/docx/PI56dLnpmok265xUpJtcxTTrnef)

# 前言

前段时间收到了鱼丸的消息，询问是否还在关注AI编程相关的内容，正好近期通过cursor完成了闲鱼自动化工具的开发，借此机会分享一下我做工具的玩法，跟大家学习交流。

先放一张思维导图解释一下工具的大致功能：

![](img/17bc78d4e8d5c46a4841feb4ca52d782.png)

所有工具大概分为三个模块：

1.  前端：

1.  技术栈：vue + element-ui

1.  功能：主要负责更好的查看和维护数据库数据

1.  后端：

1.  技术栈：nodejs + mysql

1.  功能：主要用于存储和管理闲鱼的数据

1.  脚本：

1.  技术栈：python

1.  功能：主要用于采集数据+发布商品

接下来我将按照模块划分来详细描述一下我是如何通过cursor来完成这三个模块的具体开发的。进入正题！

# 一：脚本【重要】

## 功能展示

我们首先来看一下完整的脚本操作过程，我录制了两个视频，视频内容包含采集关键词、采集详情、上传等功能。由于上传是单独的脚本，所以关于上传请看第二个视频。

采集脚本演示：主要演示了自动采集状态为未采集的关键词，当关键词采集完成以后，自动采集未采集的商品详情。

主要演示脚本上传商品的功能：选择类目、上传图片、填写标题文案、设置sku等

## 详细功能

1.  采集脚本

1.  连接比特浏览器，API接口文档。

1.  脚本基础配置：

1.  数据库配置

1.  采集配置（并行采集数量、重试次数、等待时间等）

1.  过滤配置（过滤想要数）

1.  coze配置（密钥、bot_id）

1.  采集关键词商品列表

1.  商品列表需要保存的字段有：商品ID、商品标题、商品文案、商品主图、价格、库存、状态、所属关键词、采集时间、采集状态、想要数、卖家ID等。这些信息我们需要存储在数据表中，方便我们后续的查询。

1.  采集商品详情

1.  商品详情需要保存的字段有：商品所有图片、商品sku信息、浏览量等。

1.  标题文案脚本

1.  使用coze生成标题文案：cozeAPI文档。

1.  上传脚本

1.  使用webdriver打开浏览器进入指定页面

1.  判断是否需要登录

1.  进入发布页面

1.  选择设置好的类目和需要发布的闲鱼店铺

1.  上传图片、填写标题文案

1.  判断sku属性（单个sku、单组sku、双组sku），设置sku属性、sku库存、价格

1.  一些配置选项（是否发布、是否擦亮等），点击发布。

## 开发思路

由于脚本内容多，接下来关于脚本的样例我统一使用采集脚本来做演示，避免造成混乱。

如果是相对简单的脚本，那么无需使用chat，我认为composer足够完成简单脚本的开发。流程还是一样的，需要先明确需求、制定开发文档、完成代码编写。

![](img/2efd3c96aee6e93e5f44fb0567774ddd.png)

![](img/5530279813516bd20f82f6d027e2a7c5.png)

![](img/10d1d6dd1cb9918f3e6c7b951b5793e0.png)

![](img/f0532b5d1a8daaf0626a5c1292e7fe94.png)

![](img/56457b3bdab39640ac70084c2befa4d1.png)

![](img/15b8953ad7059f0146cc7ad539945af8.png)

![](img/27f32f191b08d4a2bb2193a095ac88ca.png)

![](img/a2d30c9594895b95ff67d1398cca6b9b.png)

![](img/90c760defaa2bf87abee8b0c70a880bc.png)

![](img/2b4ec2890735cdce76167599291c1c62.png)

![](img/0e882e9cbc182917e12bceced043b621.png)

![](img/f6418d5f0723657fe21dedf889a4bd2e.png)

# 二：后端【重要】

## 详细功能

我的开发习惯遵从模块化开发。

模块化开发是一种软件开发方法，旨在将复杂的软件系统拆分成多个独立、可重用的模块，以提高开发效率、代码重用性、可维护性和可扩展性。

定义和基本属性

模块化开发通过将软件系统自顶向下逐层划分成若干个简单的模块，每个模块都拥有清晰的功能和接口，可以独立开发、测试和维护。这些模块通过定义好的接口相互协作，共同实现整个系统的功能。每个模块通常具有以下几种基本属性：

*   接口：模块对外提供的服务或功能调用方式，是模块间相互通信的桥梁。

*   功能：模块实现的具体业务逻辑或任务，是模块的核心价值所在。

*   逻辑：模块内部的实现细节，包括算法、数据结构等，反映了模块的内部特性。

*   状态：模块在执行过程中可能处于的不同状态，以及状态之间的转换关系。

优势

1.  提高开发效率：通过将系统拆分为多个模块，可以并行开发，减少开发周期。开发人员可以专注于特定模块的实现，提高开发效率。

1.  提高代码重用性：模块是独立的、可重用的软件单元，通过封装通用功能和接口，可以在不同的项目中进行复用，减少重复劳动。

1.  提高可维护性：由于模块间通过接口进行通信，降低了模块间的耦合度，使得修改或更新某个模块时不会影响到其他模块。此外，模块化的结构也使得代码更加清晰、易于理解和维护。

1.  提高可扩展性：当系统需要增加新功能时，可以通过添加新的模块或修改现有模块的接口来实现，而无需对整个系统进行重构。

我们在开发之前首先需要明确我们需要哪些数据，需要基于哪些数据做一些什么样的操作。数据库应该存储一些什么信息，哪些信息是重要的，哪些信息是次要的。由上面得出后端需要具备内的功能点有哪些。如果想实现从采集 -> 上传完整的步骤，那么后端所必须具备的东西有如下图片所示。

![](img/0698be99f35ed80f731b89193138fc1f.png)

## 开发思路

当我们的需求明确之后，可以给cursor分配角色（ Chat ⌈产品经理⌋、Chat ⌈ 代码审查 ⌋、Composer ⌈ 程序员 ⌋）我们就可以通过 cursor 来创建我们的应用。

*   和 ⌈产品经理⌋ 商讨完整的开发流程、制定开发文档。

![](img/3ee5ffa03bd492d0cdabe1cdb6d5d0ac.png)

![](img/6ce6f5613a73a475c6544c01a16f0e56.png)

这是一份初始的开发文档。可以基于此文档继续进行完善。

![](img/304280b7c0b44ef2b9f4187a36ca2904.png)

![](img/e3118d57945dbfd8a392e0d7e0d033ea.png)

![](img/a140d42e7c0914d7fd333901c9f89837.png)

让cursor基于基础文档进行更新，我们可以在沟通的过程中，删除我们不需要的功能，比如一些过度的设计（库存预警、安全日志等）

![](img/d02caa27b90ef2eabf72822af5cdc4d8.png)

![](img/1c396564fd7053d6c45bd479964890e5.png)

这是一份进行了基础修改的文档，我们可以根据自己的需求来完善和修改。

*   和 ⌈程序员⌋ 详细沟通需求、进行代码实现。我们再次强调一下，我这里遵从模块化的开发，这样方便后续的开发和扩展。

![](img/02e97a3e8da475e78c326980813ab43d.png)

![](img/6a010dbb6c8f91d5462a50904db489c9.png)

![](img/542ca945692ab90592007785adaf8470.png)

*   让 ⌈代码审查⌋ 仔细审查代码，给出完善准确的代码修改方案。我们通过代码审查过一遍composer的代码，看一下代码审查给出的建议，筛选出我们认为有必要的修改告诉代码审查写成一份完整的代码审查报告。我们将审查报告发给composer让它依据报告进行修改。

![](img/1e54d2a930298474a689cc9d4e3e79c5.png)

![](img/05ee971d7f19799940e69ed8fbd0c9c9.png)

![](img/360f3b8ec8e9f7b631943319f5bedfd3.png)

![](img/fc2c3bd70684bb13a9c7d6f0bfcf17b5.png)

*   我们需要将数据库所有数据表的完整字段打印出来，以备后续脚本开发时使用。样例：

```
mysql> SHOW TABLES; 
+-------------------------+
| Tables_in_xianyu_manage |
+-------------------------+
| t_keyword               |
| t_log_operation         |
| t_prod_category         |
| t_prod_image            |
| t_prod_info             |
| t_prod_keyword          |
| t_prod_operation_log    |
| t_prod_shop             |
| t_seller_info           |
| t_shop_info             |
| t_shop_item             |
| t_stat_daily            |
| t_sys_config            |
| t_sys_user              |
| t_task_collection       |
| t_task_execution        |
| v_shop_collect_stats    |
+-------------------------+
19 rows in set (0.00 sec)

mysql> SHOW COLUMNS FROM t_collect_log;  
+------------+----------+------+-----+-------------------+-------------------+
| Field      | Type     | Null | Key | Default           | Extra             |
+------------+----------+------+-----+-------------------+-------------------+
| id         | bigint   | NO   | PRI | NULL              | auto_increment    |
| task_id    | bigint   | NO   | MUL | NULL              |                   |
| log_type   | tinyint  | NO   |     | NULL              |                   |
| content    | text     | NO   |     | NULL              |                   |
| created_at | datetime | NO   |     | CURRENT_TIMESTAMP | DEFAULT_GENERATED |
+------------+----------+------+-----+-------------------+-------------------+
5 rows in set (0.00 sec)

mysql> SHOW COLUMNS FROM t_keyword;     
+----------------+--------------+------+-----+-------------------+-----------------------------------------------+
| Field          | Type         | Null | Key | Default           | Extra                                         |
+----------------+--------------+------+-----+-------------------+-----------------------------------------------+
| id             | bigint       | NO   | PRI | NULL              | auto_increment                                |
| name           | varchar(100) | NO   | UNI | NULL              |                                               |
| collect_status | tinyint      | NO   | MUL | 0                 |                                               |
| collect_time   | datetime     | YES  | MUL | NULL              |                                               |
| created_at     | datetime     | NO   |     | CURRENT_TIMESTAMP | DEFAULT_GENERATED                             |
| updated_at     | datetime     | NO   |     | CURRENT_TIMESTAMP | DEFAULT_GENERATED on update CURRENT_TIMESTAMP |
+----------------+--------------+------+-----+-------------------+-----------------------------------------------+
6 rows in set (0.00 sec)

mysql> SHOW COLUMNS FROM t_prod_image;
+------------+--------------+------+-----+-------------------+-------------------+
| Field      | Type         | Null | Key | Default           | Extra             |
+------------+--------------+------+-----+-------------------+-------------------+
| id         | bigint       | NO   | PRI | NULL              | auto_increment    |
| product_id | bigint       | NO   | MUL | NULL              |                   |
| url        | varchar(500) | NO   |     | NULL              |                   |
| sort       | int          | NO   |     | 0                 |                   |
| is_main    | tinyint      | NO   |     | 0                 |                   |
| status     | tinyint      | NO   | MUL | 1                 |                   |
| file_size  | int          | YES  |     | NULL              |                   |
| dimensions | varchar(20)  | YES  |     | NULL              |                   |
| created_at | datetime     | NO   |     | CURRENT_TIMESTAMP | DEFAULT_GENERATED |
+------------+--------------+------+-----+-------------------+-------------------+
9 rows in set (0.00 sec)

mysql> SHOW COLUMNS FROM t_prod_info;  
+-------------------+---------------+------+-----+-------------------+-----------------------------------------------+
| Field             | Type          | Null | Key | Default           | Extra                                         |
+-------------------+---------------+------+-----+-------------------+-----------------------------------------------+
| id                | bigint        | NO   | PRI | NULL              | auto_increment                                |
| name              | varchar(255)  | NO   |     | NULL              |                                               |
| title             | varchar(255)  | NO   |     | NULL              |                                               |
| code              | varchar(50)   | NO   | MUL | NULL              |                                               |
| category_id       | bigint        | NO   | MUL | NULL              |                                               |
| price             | decimal(10,2) | NO   |     | 0.00              |                                               |
| stock             | int           | NO   |     | 0                 |                                               |
| sales             | int           | NO   |     | 0                 |                                               |
| status            | tinyint       | NO   | MUL | 0                 |                                               |
| source_url        | varchar(500)  | YES  |     | NULL              |                                               |
| description       | text          | YES  |     | NULL              |                                               |
| keywords          | varchar(500)  | YES  | MUL | NULL              |                                               |
| shop_id           | bigint        | NO   | MUL | NULL              |                                               |
| collect_time      | datetime      | YES  | MUL | NULL              |                                               |
| publish_time      | datetime      | YES  |     | NULL              |                                               |
| rewrite_status    | tinyint       | NO   | MUL | 0                 |                                               |
| publish_status    | tinyint       | NO   | MUL | 0                 |                                               |
| created_at        | datetime      | NO   |     | CURRENT_TIMESTAMP | DEFAULT_GENERATED                             |
| updated_at        | datetime      | NO   |     | CURRENT_TIMESTAMP | DEFAULT_GENERATED on update CURRENT_TIMESTAMP |
| deleted_at        | datetime      | YES  |     | NULL              |                                               |
| collect_status    | tinyint       | NO   | MUL | 0                 |                                               |
| collect_error     | varchar(500)  | YES  |     | NULL              |                                               |
| collect_count     | int           | NO   |     | 0                 |                                               |
| last_collect_time | datetime      | YES  |     | NULL              |                                               |
+-------------------+---------------+------+-----+-------------------+-----------------------------------------------+
24 rows in set (0.00 sec)

mysql> SHOW COLUMNS FROM t_seller_info; 
+------------------+--------------+------+-----+-------------------+-----------------------------------------------+
| Field            | Type         | Null | Key | Default           | Extra                                         |
+------------------+--------------+------+-----+-------------------+-----------------------------------------------+
| id               | bigint       | NO   | PRI | NULL              | auto_increment                                |
| shop_id          | varchar(255) | NO   |     | NULL              |                                               |
| seller_id        | varchar(50)  | NO   | UNI | NULL              |                                               |
| nickname         | varchar(100) | YES  |     | NULL              |                                               |
| rating           | decimal(3,1) | YES  | MUL | NULL              |                                               |
| total_items      | int          | NO   |     | 0                 |                                               |
| good_rating_rate | decimal(5,2) | YES  |     | NULL              |                                               |
| status           | tinyint      | NO   | MUL | 1                 |                                               |
| last_active_time | datetime     | YES  | MUL | NULL              |                                               |
| description      | text         | YES  |     | NULL              |                                               |
| location         | varchar(100) | YES  |     | NULL              |                                               |
| created_at       | datetime     | NO   |     | CURRENT_TIMESTAMP | DEFAULT_GENERATED                             |
| updated_at       | datetime     | NO   |     | CURRENT_TIMESTAMP | DEFAULT_GENERATED on update CURRENT_TIMESTAMP |
| deleted_at       | datetime     | YES  |     | NULL              |                                               |
+------------------+--------------+------+-----+-------------------+-----------------------------------------------+
14 rows in set (0.00 sec)

mysql> SHOW COLUMNS FROM t_shop_info; 
+--------------------+--------------+------+-----+-------------------+-----------------------------------------------+
| Field              | Type         | Null | Key | Default           | Extra                                         |
+--------------------+--------------+------+-----+-------------------+-----------------------------------------------+
| id                 | bigint       | NO   | PRI | NULL              | auto_increment                                |
| name               | varchar(100) | NO   |     | NULL              |                                               |
| platform           | varchar(50)  | NO   | MUL | NULL              |                                               |
| shop_url           | varchar(500) | YES  |     | NULL              |                                               |
| status             | tinyint      | NO   | MUL | 0                 |                                               |
| rating             | decimal(2,1) | YES  |     | 5.0               |                                               |
| created_at         | datetime     | NO   |     | CURRENT_TIMESTAMP | DEFAULT_GENERATED                             |
| updated_at         | datetime     | NO   |     | CURRENT_TIMESTAMP | DEFAULT_GENERATED on update CURRENT_TIMESTAMP |
| total_products     | int          | NO   |     | 0                 |                                               |
| collected_products | int          | NO   |     | 0                 |                                               |
| last_collect_time  | datetime     | YES  |     | NULL              |                                               |
| collect_status     | tinyint      | NO   | MUL | 0                 |                                               |
+--------------------+--------------+------+-----+-------------------+-----------------------------------------------+
12 rows in set (0.00 sec)

mysql> SHOW COLUMNS FROM t_sys_config;
+--------------+--------------+------+-----+-------------------+-----------------------------------------------+
| Field        | Type         | Null | Key | Default           | Extra                                         |
+--------------+--------------+------+-----+-------------------+-----------------------------------------------+
| id           | bigint       | NO   | PRI | NULL              | auto_increment                                |
| config_key   | varchar(50)  | NO   | UNI | NULL              |                                               |
| config_value | text         | YES  |     | NULL              |                                               |
| description  | varchar(200) | YES  |     | NULL              |                                               |
| created_at   | datetime     | NO   |     | CURRENT_TIMESTAMP | DEFAULT_GENERATED                             |
| updated_at   | datetime     | NO   |     | CURRENT_TIMESTAMP | DEFAULT_GENERATED on update CURRENT_TIMESTAMP |
+--------------+-------------

mysql> SHOW COLUMNS FROM t_shop_item;  
+-------------------+---------------+------+-----+-------------------+-----------------------------------------------+
| Field             | Type          | Null | Key | Default           | Extra                                         |
+-------------------+---------------+------+-----+-------------------+-----------------------------------------------+
| id                | bigint        | NO   | PRI | NULL              | auto_increment                                |
| seller_id         | bigint        | NO   | MUL | NULL              |                                               |
| item_id           | bigint        | NO   | MUL | NULL              |                                               |
| item_price        | decimal(10,2) | YES  |     | NULL              |                                               |
| item_image        | varchar(500)  | YES  |     | NULL              |                                               |
| collect_status    | tinyint       | NO   | MUL | 0                 |                                               |
| collect_count     | int           | NO   |     | 0                 |                                               |
| last_collect_time | datetime      | YES  |     | NULL              |                                               |
| created_at        | datetime      | NO   |     | CURRENT_TIMESTAMP | DEFAULT_GENERATED                             |
| updated_at        | datetime      | NO   |     | CURRENT_TIMESTAMP | DEFAULT_GENERATED on update CURRENT_TIMESTAMP |
+-------------------+---------------+------+-----+-------------------+-----------------------------------------------+
10 rows in set (0.00 sec)

mysql> SHOW COLUMNS FROM cookies;            
ERROR 2013 (HY000): Lost connection to MySQL server during query
No connection. Trying to reconnect...
Connection id:    117
Current database: xianyu_manage

+---------------+--------------+------+-----+-------------------+-----------------------------------------------+
| Field         | Type         | Null | Key | Default           | Extra                                         |
+---------------+--------------+------+-----+-------------------+-----------------------------------------------+
| id            | int          | NO   | PRI | NULL              | auto_increment                                |
| cookie        | text         | NO   |     | NULL              |                                               |
| token         | varchar(255) | NO   |     | NULL              |                                               |
| create_time   | datetime     | YES  |     | CURRENT_TIMESTAMP | DEFAULT_GENERATED                             |
| update_time   | datetime     | YES  |     | CURRENT_TIMESTAMP | DEFAULT_GENERATED on update CURRENT_TIMESTAMP |
| last_use      | datetime     | YES  |     | NULL              |                                               |
| is_valid      | tinyint(1)   | YES  |     | 1                 |                                               |
| fail_count    | int          | YES  |     | 0                 |                                               |
| success_count | int          | YES  |     | 0                 |                                               |
+---------------+--------------+------+-----+-------------------+-----------------------------------------------+
9 rows in set (0.01 sec)

mysql> SHOW COLUMNS FROM proxies; 
+---------------+--------------+------+-----+-------------------+-----------------------------------------------+
| Field         | Type         | Null | Key | Default           | Extra                                         |
+---------------+--------------+------+-----+-------------------+-----------------------------------------------+
| id            | int          | NO   | PRI | NULL              | auto_increment                                |
| ip            | varchar(255) | NO   |     | NULL              |                                               |
| port          | int          | NO   |     | NULL              |                                               |
| protocol      | varchar(10)  | YES  |     | http              |                                               |
| is_valid      | tinyint(1)   | YES  |     | 1                 |                                               |
| create_time   | datetime     | YES  |     | CURRENT_TIMESTAMP | DEFAULT_GENERATED                             |
| update_time   | datetime     | YES  |     | CURRENT_TIMESTAMP | DEFAULT_GENERATED on update CURRENT_TIMESTAMP |
| last_use      | datetime     | YES  |     | NULL              |                                               |
| fail_count    | int          | YES  |     | 0                 |                                               |
| success_count | int          | YES  |     | 0                 |                                               |
+---------------+--------------+------+-----+-------------------+-----------------------------------------------+
10 rows in set (0.00 sec)
```

# 三：前端【次要】

## 功能展示

![](img/63fb56436a88162c50c36aa7cce8233c.png)

![](img/df6c1479dbcd7d56054b74e6792cc369.png)

![](img/426f9250424bef4eaa22fa4f17355eac.png)

![](img/c3330914ee0e0ea8eb29d6306806d1b6.png)

![](img/0c834aeb9a3332e574f7f86ef20c1311.png)

## 完整步骤

1.  将需要采集的关键词添加到关键词列表中

![](img/dcc1131e2816a94e6854c16b8ada29f3.png)

点击批量新增

![](img/17a0d61aa6baf8888f22e0792e0682f7.png)

批量新增

![](img/709c6b273b26462b9ec310e514cf43ea.png)

新增成功

1.  启动采集脚本，脚本会提取数据库中未采集的关键词，将提取到的关键词的采集状态设置为采集中

1.  采集关键词商品列表数据、筛选过滤去重列表数据、存储列表数据，当关键词采集完成后，状态设置为采集完成

1.  当所有未采集的关键词全部采集完成后，会自动开始执行采集商品、提取状态为未采集的商品id开始采集商品详情

1.  采集商品详情完善基础商品数据表、将采集成功的商品的采集状态设置为成功，所有状态均在前端中有体现

1.  在前端中开始选品、将选好的品进行发布

1.  进入到发布管理，这时候我们需要处理两个地方：一个是商品图片，一个是标题文案。

1.  目前商品采用的是软件批处理、标题文案采用的是coze的API接口，coze处理完成后将标题文案存储到数据库中

1.  启动我们的发布脚本，进行发布。发布脚本需要处理的几个难点问题在于单个sku，单组sku和多组sku的问题，这里我们需要注意一下。发布脚本详情请看演示视频。

# 四：使用Cursor踩的坑

1.  精细要求代码输出不完整，cursor会“偷懒”

1.  大致要求代码输出冗余

1.  错误理解意思（我上面正在修改商品列表页，当我切换到新的页面时，会错误理解意思）

![](img/9376a86b488522afca37522ead844bf1.png)

这里在优化商品列表页

![](img/4634d63bd19070026e19601e3c2a92ef.png)

这里定位到发布列表页，修改出错了

1.  修改过程中会误删正确的代码逻辑

![](img/754bc917941a406222c515958cf2becd.png)

![](img/386f13c1a8d9dc23623aad703a4d17a3.png)

![](img/d78b60090b5e6f5e39ffbe024b819eef.png)

![](img/5deb0b73200cc4a6457966adb8f97465.png)

1.  当新增功能时，如果不人工要求，它会直接新增代码来完成你的需求，而不是检索当前模块时候具备此功能。需要人工介入。

1.  代码修改不完整，比如我们新增了新模块的使用方法，cursor会直接调用该模块的方法，但是并没有导入该模块，直接运行会导致代码报错。

1.  对话太多导致需要创建新的对话

![](img/eeed37efd9f45f3997acc6f0a48d21aa.png)

# 五：结语

cursor基础配置，请参考如下文档：

生财cursor航海对于cursor的配置和基础开发已经写的很完善了。cursor航海手册

生财圈友的文章：怎样通过Cursor编写复杂产品及AI协作编程

关于AI应用的文章生财里面有很多，都是优秀的分享，想了解更多关于cursor可看生财AI应用模块里面的分享。

如果有收获帮忙原文点个赞吧，感谢你的慷慨~