---
title: about
date: 2022-12-07 08:06:39
---



> Hi，我是谢冬博，欢迎来到我的个人博客网站，网站从12月7号开始运营，源站部署在`Github Pages`中，使用了`CloudFlare`作为DNS域名映射，希望坚持下去!!!

> ！！目前正在找上海的工作，有兴趣的公司可以[邮箱]sfreebobo@163.com联系！

### 我所涉及到领域: 

- Python
  - Django
  - DRF
- Database
  - MySQL
  - Redis
  - MongoDB
- MQ
  - MQTT
- Container
  - Docker、Docker-Compose
  - singularity

### 我所做过的项目：

#### ***设备一体化管理小程序**：*

一个用于管理公司旗下所有设备的微信小程序，具备设备状态展示与管理、设备数据统计、定时 任务、输入输出设备管理、文本投屏等多样功能。在一个应用中集结了对多种硬件设备的基本管理控制， 方便用户对设备进行操控。 

#### 主要职责： 

- 参与前后端技术选型（Django + DRF + MySQL + MongoDB + Redis + MQTT +Celery + UniAPP）， 参与项目目录模块划分、文件命名设计与整体架构。 
- 对软件整体性能进行持续优化，对项目服务器进行日常维护。 
- 对接相应API接口，开发 Python 版本 SDK 给予设备进行快速调用通信。 

#### 技术要点： 

- 基于 Agent 架构对设备模块进行业务调整，将设备对应为多智能体，便于后期的需求的扩展以及维护。 
- 转换原有存储在 MySQL 数据库中的设备信息转存到 MongoDB 数据库中，优化相关查询业务速度，增 加系统在面临大量数据写入写出时候的吞吐允许量。 
- 通过 Celery 定义相关定时任务，在固定时间段统计相关设备信息，替换原有的实时查询的统计业务，以 此提高服务性能表现。 
- 采用分包下载、骨架屏、图片懒加载等技术对小程序的加载速度与体验进行优化。 

#### ***虚拟舞蹈应用**：*

一款基于元宇宙概念所开发的虚拟艺术应用，用户在通过手机相机来创建个人虚拟形象后，基于此虚 拟形象来生成多样且独特的舞蹈进行舞蹈 PK 并获得不同经验值来解锁其余功能。 

#### 主要职责： 

- 深入研究最前沿的编舞相关论文，对比不同的神经网络结构、舞蹈数据集、自动编舞技术的改进，在论 文数据集或最新的舞蹈数据集上测试文中使用的 2D 或 3D 舞蹈数据集，验证其结果正确性，并研究其 网络结构的泛化能力。 
- 探究由视频中提取 2D 人体姿态并转换为 3D 人体姿态的技术，确定了相关数据集以及确定了效果较好 的网络结构和参数。 
- 开发 3D 模型重定向转换技术，并构建相关服务，最终实现将用户提供的视频人物模型转换成不同卡通 人物骨架与人物模型。 

#### 技术要点：

解决不同数据集定义格式相互间转换的问题，将 3.6m 数据集数据转为 maximo 数据集格式数据。 

部署实验环境，调用 VideoPose3D 与 Detectron 识别视频中人体姿态并转换为三维数据。



### 我所写过的论文：

- Liu, Y., Xie, D., Zhuo, H. H., Lai, L. (2020). Plan2Dance: Planning Based Choreographing from  Music. Proceedings of the AAAI Conference on Artificial Intelligence, 34(09), 13624-13625.  https://doi.org/10.1609/aaai.v34i09.7099。 

- Temporal Planning-Based Choreography from Music 被 ChineseCSCW（Computer Supported  Cooperative Work）2022 录用为长文。

