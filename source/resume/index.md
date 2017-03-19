---
title: 简历
date: 2016-08-17 14:36:54
layout: post
---

# 联系方式

- 手机：15800822331
- Email：kyyblabla@163.com
- QQ/微信：337994130

---

# 个人信息

 - 康岩岩/男/1992 
 - 本科/中原工学院/计算机科学与技术/2015届
 - 工作年限：1年
 - 技术博客：http://kyyblabla.github.io/
 - Github: https://github.com/kyyblabla
 - OSChina:http://git.oschina.net/kyyblabla
 - 期望职位：**Java Web工程师**
 - 期望薪资：8K~12K，目前薪资为8K*13月
 - 期望城市：上海
 
---

# 工作/项目经历


## 北京源石云科技有限公司 （2015年6月 ~ 至今）

### 分期消费电商平台（小象优品 ）

分期消费电商App，主打优选商品与分期消费。

技术方案：SpringMVC+MyBatis+MySql+Memcache

主要分工：

- 商品、订单模块的设计与实现，面向APP
- 商品、订单、用户后台管理模块的设计与实现
- 独立负责管理后台的前端设计与实现，并协助调试后台管理接口

由于之前习惯使用JAP，对Mybatis纯过程sql语句书写很不适应，但是最终做到了细粒度的查询优化，进一步提高了对sql的掌握程度与优化经验。提出并使用SpringRmi作为各子系统之间远程调用方案（原方案为纯Http调用）, 使远程接口的调用更高效、可靠。本人参考主流电商平台的商品模型，设计出适用于小型电商的SKU管理方案。后台管理使用AngularJS快速推进开发进度，前端严格遵循模块化开发规范提高了系统组件的复用性。


### 基于阿里Tanx的DSP广告投放系统（ 源石DSP ）

广告投放平台，对接Tanx（阿里妈妈旗下互联网推广的营销平台），主要投放目标为移动网页、app。 高并发系统，集群环境，日均PV300万。

主要分工：

- 广告展示、点击事件的回调追踪模块，根据规则（千次点击）进行计费
- 设计与实现后台管理系统前端界面(AngularJS+Bootstrap+RequireJS)，并协助后台系统完成API测试与改进
- 广告浏览用户地理位置查询接口（基于用户经纬度）

根据产品原型独立实现后台管理系统前端界面，提供广告编辑、预览（模拟移动设备）与投放计划管理。
使用MongoDB的地理位置Geohash检索，索引全国最小行政单位（村委、街道）数据70万+，数据来源为百度地图api，查询准确率达96%。由于Tanx平台要求单次请求响应时间为160ms，因此系统采用长连接技术，各个模块高度压榨运行效率。

### 信贷员在线拍标工具（ 发单宝）

面向信贷员的信贷信息拍卖平台，提供信贷信息实时在线竞拍。

技术方案：SpringMVC+SpringJPA+MySql+Memcache

- 向APP提供贷款订单、用户信息相关接口
- 订单、用户相关的后台管理模块设计与实现
- 后台管理系统前端设计与实现（Angular+BootStrap+RequireJs）

系统的一个难点为订单状态的追踪与埋点触发，本人通过细致的流程分析与产品沟通，确定了订单的各个状态转换与触发事件，做到了状态不遗漏、事件不误触。另外高并发环境下的Spring事务控制也通过此项目得到了很好的掌握。

### 其他项目
- 合作电商分期消费服务
- 信贷信息录入助手

 
## 上海直达软件有限公司【实习】（2014年10月 ~ 2015年4月）

### 期货交易通信接口

主要工作：

- 研读交易所开发文档（英文）、学习期货交易相关术语
- 采用VS2012开发环境，使用C++对交易所提供的C语言接口进行封装，联通内部交易系统
- 多线程通信程序，使用Boost库提供线程支持
- 配合SGX进行接口测试，为公司获取交易所认证资格


##  中原工学院【在校】（2012年10月~2014年10月）

###  舆情分析-新浪微博采集系统

舆情分析系统的子项目，采集最新微博内容，为核心分析引擎提供数据源。

技术与分工：

- 采用了Spring构建抓取框架,使用HttpClient模拟浏览器请求登陆并抓取微博信息
- 抓取程序支持动态IP代理更换以及动态账户更换，以防止新浪屏蔽IP及账户
- 使用Jsoup解析网页中微博信息，存入MySQL数据库，使用Spring JPA构建持久化接口
- 单台机器微博日均获取量400万

### 基于MQTT的消息服务器

毕业设计题目，可提供嵌入式设备与管理终端之间的通信服务，为智能化工厂项目的子系统，使用MQTT通信协议。

技术与功能：

- 提供平台无关的通信接口，数据格式为JSON，桌面/移动客户端、浏览器（Web Socket）都可接入
- 采用负载均衡技术、高效处理并发数据，对外提供多对多通信
- 该项目最终获取校级优秀毕业设计荣誉


---


# 技能列表

- Web开发：Java
- Web框架：Spring JPA/Spring MVC/Hibernate/MyBatis
- Web服务器：Nginx/Tomcat/Jetty
- 前端框架：Bootstrap/AngularJS/HTML5
- 前端工具：JQuery/Bower/RequireJs/Gulp/Underscore/LeSS
- 数据库：MySQL/MongoDB
- 缓存工具：Memcache/ECache
- 版本管理、文档和自动化部署工具：Svn/Git/Maven/NPM
- 单元测试：JUnit/Mocha(JavaScript)
- 云和开放平台：阿里云/Bae/微信应用后台
- 其他掌握语言、框架：C/C++/Qt C++/C#

---

# 自我评价

- 重视团队合作，注重开发流程规范，热爱文档
- 喜欢倒腾各种新奇、有趣的技术
- 喜欢关注IT行业的最新动态、技术大牛的轶事

---

## 技能关键字

- Java
- Spring
- Html
- Bootstrap
- AngularJs
- Mysql

---

# 致谢

感谢您花时间阅读我的简历，期待能有机会和您共事。