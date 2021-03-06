---
title: resume
date: 2016-08-17 14:36:54
layout: post
---

# 联系方式

- 手机：15800822331
- Email：kyyblabla@163.com
- QQ/微信：337994130/kyyblabla

---

# 个人信息

- 康岩岩/男/1992
- 本科/中原工学院/计算机科学与技术/2015届
- 工作年限：2年
- 目前已离职，可快速到岗
- 博客：http://www.jianshu.com/u/1d4626240769
- GitHub：https://github.com/kyyblabla
- OsChina：http://git.oschina.net/kyyblabla
- 期望职位：**Java Web工程师**
- 期望薪资：面议

---

# 自我评价
- 能够独立开发、测试、部署项目，熟悉主流Java Web开发技术和框架，如SpringBoot、SpringMVC、Mybatis、Hibernate、Struts2
- 经常使用流行Java技术与工具，如Cache、lambda、RPC、并发编程、AOP、异步消息、NIO
- 熟悉常用数据结构与算法，熟悉常用设计模式、UML建模
- 有扎实的前端技术功底，熟悉流行前端框架与技术（Vue、AngularJS、es6、npm、webpack）
- 有丰富的前后端结合开发经验，可以进行全栈式开发
 
---

# 工作/项目经历
## 上海吉百翁信息科技有限公司 （2016年7月 ~ 至今）

公司主营业务为保险咨询App，为大众用户（[吉百翁保险app](https://itunes.apple.com/cn/app/%E5%90%89%E7%99%BE%E7%BF%81%E4%BF%9D%E9%99%A9/id1086449802)）与专业保险经纪人（[吉小保app](https://itunes.apple.com/cn/app/%E5%90%89%E5%B0%8F%E4%BF%9D/id1157306685)）
之间搭建沟通平台。在工作期间内主要开发了两端app后台接口以及中后台管理系统。后端技术栈为：SpringBoot+MyBatis+Redis+MySql+Restful，前端技术栈为：Vue+VueMaterial+webpack

### app后台接口开发
- 重构老系统，借鉴微服务思想分拆业务模块，面向接口提供服务
- 使用SpringBoot作为主要后台框架，加快开发进度，减小部署难度，同时做到快速响应新需求
- 学习并搭建Jenkins持续集成平台，简化构建、测试、发布流程
- 使用GitBook编写与发布api文档，同时提供postman调用示例，方便app端接口调试
- 使用缓存策略优化接口访问速度

### 中后台管理系统
- 重写中后台管理系统，采用前后分离模式，解决老系统响应速度慢、数据交互冗余、浏览器兼容等弊端
- 与app后台系统共用公共组件（tool、model、部分service），同时提供交互接口，使app端与管理端形成业务功能闭环
- 使用vue(2.x)+VueMaterial重写前端页面，为中后台管理人员提供了清爽、便捷的使用体验

## 上海链家 （2016年4月 ~ 2016年7月）
### 交易流水线后台功能开发与维护
主要涉及资金流水业务模块，对收、付款单、发票、进行记录、处理，生成流水报表。

- 学习房产交易业务相关知识（非常复杂），并运用于业务系统开发与维护
- 解决项目遗留bug、重构部分功能代码
- 实现资金流水方面业务需求，在老的业务流程中埋点记录资金流水变动情况，定时任务处理资金数据变动情况
- 全栈式开发，独立完成后端接口与前端展现，主要前端技术为:JSP+AngularJS+jQuery

## 北京源石云科技有限公司 （2015年6月 ~ 2016年3月）

### 小象优品分期消费电商平台

分期消费电商App([小象优品](https://itunes.apple.com/cn/app/小象优品极速版/id1188969021?mt=8))，主打优选商品与分期消费。主要技术方案：SpringMVC+MyBatis+MySql+MemCache。

- 商品、订单模块的需求分析、设计实现，提供api接口与相关文档
- 商品、订单、用户模块后台管理api
- 独立负责管理后台的前端设计与实现（AngularJs+BootStrap+gulp+bower），并协助调试后台管理接口

### 基于阿里Tanx的DSP广告投放系统（ 源石DSP ）

广告投放平台，对接Tanx（阿里妈妈旗下互联网推广的营销平台），主要投放目标为移动网页、app。 高并发系统，集群环境，日均PV300万。

- 广告展示、点击事件的回调追踪模块，根据规则（千次点击）进行计费
- 设计与实现后台管理系统前端界面(AngularJS+Bootstrap+RequireJS)，并协助后台系统完成API测试与改进
- 实现广告浏览用户地理位置查询接口（基于用户经纬度）
- 根据产品原型独立实现后台管理系统前端界面，提供广告编辑、预览（模拟移动设备）与投放计划管理
- 使用MongoDB的地理位置GeoHash检索，索引全国最小行政单位（村委、街道）数据70万+，数据来源为百度地图api，查询准确率达96%。由于Tanx平台要求单次请求响应时间为160ms，因此系统采用长连接技术，各个模块高度压榨运行效率。

### 信贷员在线拍标工具（ 发单宝）

面向信贷员的信贷信息拍卖平台，提供信贷信息实时在线竞拍。主要技术方案：SpringMVC+SpringJPA+MySql+MemCache

- 向APP提供贷款订单、用户信息相关api，编写api文档
- 订单、用户相关的后台管理模块设计与实现
- 后台管理系统前端设计与实现（Angular+BootStrap+RequireJs）


## 上海直达软件【实习】（2014年10月 ~ 2015年4月）

### 期货交易通信接口

- 研读交易所开发文档（英文）、学习期货交易相关术语
- 采用VS2012开发环境，使用C++对交易所提供的C语言接口进行封装，对接内部交易系统
- 多线程通信程序，使用Boost库提供线程支持
- 配合SGX（新加坡交易所）进行接口测试，为公司获取交易所认证资格

##  中原工学院【在校】（2012年10月~2014年10月）

###  舆情分析-新浪微博爬虫

舆情分析系统的子项目，根据用户标示爬取微博内容，为核心分析引擎提供元数据。

- 多线程抓取程序，HttpClient模拟微博登陆、抓取微博信息
- 抓取程序支持动态代理IP更换以及动态账户更换，以防止新浪屏蔽IP及账户
- 使用JSoup解析网页中微博信息，采用使用Spring JPA构建持久化接口
- 单台机器微博日均获取量400万

### 基于MQTT的消息服务器

毕业设计题目，可提供嵌入式设备与管理终端之间的通信服务，为智能化工厂项目的子系统，使用MQTT通信协议。

- 提供平台无关的通信接口，数据格式为JSON，桌面/移动客户端、浏览器（Web Socket）都可接入
- 采用负载均衡技术、高效处理并发数据，对外提供多对多通信
- 该项目最终获取校级优秀毕业设计荣誉

---
 
# 常用技能列表

- Web框架、工具：Spring Boot/Spring MVC/MyBatis/Netty
- Web服务器：Tomcat/Jetty/Nginx
- 消息：RabbitMQ、WebSocket
- 持续集成：Jenkins
- 前端框架：Vue/AngularJS(1.x)/Bootstrap/HTML5/略懂React Native
- 前端工具：npm/bower/webpack/gulp/leSS
- 数据库：MySQL/MongoDB
- 缓存：Redis/MemCache
- 版本管理、文档和自动化部署工具：SVN/Git/GitBook/Markdown/Maven
- 操作系统及工具：maxOS、Linux、shell编程
- 其他掌握语言、框架：C++/Qt C++/C#/略懂node.js服务开发