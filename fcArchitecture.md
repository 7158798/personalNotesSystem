[TOC]

## 系统架构

FARMS

金融资产交易、衍生与管理系统（以下简称FA-XDMS）：Finance Asset Exchange Derivative Management System

金融资产交易、衍生与管理系统（以下简称FA-XDMS）是一个面向互联网的金融资产交易平台，为金融产品提供方提供灵活的金融资产组合定价，上线销售，客户服务，风险管理以及营销管理等功能，同时为投资者提供可靠的金融产品投资渠道，灵活地管理自己的投资需求，通过**网站、移动应用等方式**安全便捷地完成投资交易。

FA-XDMS系统基于互联网开放架构，支持云计算环境部署，并提供基于负载的横向可扩展性。FA-XDMS系统采用微服务架构，各个业务模块具有独立的应用服务器集群和数据库集群，各模块之间采用HTTP REST服务调用的方式或消息队列进行通信，可以独立升级和维护，避免了单个集中式系统的复杂性和性能压力。为了支持海量数据的管理，系统提供分布式的数据管理方案，通过数据库的分库策略和读写分离策略，确保系统可以支持面向互联网用户的高并发访问性能压力。

不同的金融产品具有差异化的数量结构，业务流程，业务交易，用户界面等需求，FA-XDMS支持金融产品的完全可配置性，用一套统一的产品模型和金融服务合同模型支持各种产品线，如基金，证券，保险，债权，众筹，信贷等，并为将来的混业金融创新提供了一个基础系统支持平台。

FA-XDMS系统包括交易接口网关，金融产品管理，金融服务合同管理，账户管理，客户信息管理，营销活动管理等业务模块。

FA-XDMS系统不仅为客户提供基于Web的访问方式，同时提供了基于Android/iOS的移动应用访问方式，便于客户随时随地管理自己的投资，最大化投资收益。





## 富聪系统架构及规范

名词解释

Product        由富聪利用第三方产品供应商提供的产品原型，进行包装、组合而形成，面向终端客户的理财产品。产品不局限于保险、基金等传统理财产品。

Agreement	客户在富聪平台上进行产品购买的凭证，用户对产品进行交易操作的基本单位。

Account		客户个人账务记录的最小单位，一个用户允许有多个account存在，多个account的集合即体现为我得财富。

钱包			指的是易钱包，用户在富聪上面的基础产品，具有稳定收益的功能。

交易		![交易](.\imagenote\富聪--交易--概念.png)



| 中文      | 英文                | 说明                                      |
| ------- | ----------------- | --------------------------------------- |
| 平台商     | PasCompany        | 分销富聪NFS产品的其他平台，如网易理财，玩途。富聪本省也作为一个平台商管理。 |
| 业务伙伴    | ProductProvider   | 包括：产品供应商，支付网关等                          |
| 支付网关    | PaymentProvider   |                                         |
| 金融服务合同  | Agreement         |                                         |
| 合同请求/交易 | Agreement         |                                         |
| 客户      | Client            |                                         |
| 用户账户    | SecurityUser      |                                         |
| 金融账户    | Account           |                                         |
| 产品定义/模板 | ProductDefinition |                                         |
| 产品      | ProductOffering   |                                         |
| 富聪NFS产品 |                   | 服从给予供应商产品包装的产品                          |
| 供应商产品   |                   |                                         |





我们的系统：

- 集中式系统
- 基于springMVC
- 自定义的ORM层
- 模型引擎 
- 产品引擎
- 完善的管理后台
- 开放平台（open-API

业务架构

![](.\imagenote\业务架构.png)

![](.\imagenote\业务架构2.png)





编码规范

关于工厂类

工厂模式：用来构造一批有共性的对象供调用者使用。

关于返回null

```
Every time you write code that conflates null strings and empty strings, the Guava team weeps
出自：https://code.google.com/p/guava-libraries/wiki/UsingAndAvoidingNullExplained#Optional
```







##  日志集中管理和分析工具: ElasticSearch + Log Stash

1. 测试环境地址：http://172.16.1.96/kibana/index.html#/dashboard/file/default.json
2. 打开WEB页面，选择Unconfigured Dashboard。

##  Build工具

Maven

```
$ mvn install-Dmaven.test.skip=true
$ mvn package -Dmaven.test.skip=true
$ mvn clean source:jar deploy -Dmaven.test.skip=true
```

FARMS:
Financial Assets Registration and Management System

AIAF


