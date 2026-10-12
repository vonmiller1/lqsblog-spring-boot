# lqsblog-backend-java-springboot

一个基于 Spring Boot 的博客后端项目，采用 Maven 构建，提供管理端和 PC 端 API，并按模块组织公共代码、数据访问和业务服务。

## 功能

- 登录与注销，使用 Shiro 和 JWT 进行身份验证
- 首页与数据统计
- 随笔、作品、专题和友情链接管理
- 站点设置，包括关于信息、标签、账号、角色、菜单、API 和站点配置
- 可扩展的 Web 前台模块

## 技术栈

- Java、Spring Boot、Spring Framework
- Apache Shiro、JWT
- MyBatis、MyBatis-Plus
- SLF4J、Jackson、Fastjson、Lombok
- Maven、Thymeleaf

## 模块结构

```text
├── lqsblog-api             管理端和 PC 端 API
├── lqsblog-api-common      API 公共模块
├── lqsblog-common          项目公共模块
├── lqsblog-database        实体类、DTO 和 VO
├── lqsblog-service         业务服务模块
├── lqsblog-webs            PC Web 前台
├── lqsblog-webs-common     Web 公共模块
└── pom.xml                 Maven 配置
```

## 环境要求

- JDK 11 或更高版本
- MySQL 5.7 或更高版本
- Maven 3.6 或更高版本
- IntelliJ IDEA（建议启用 Lombok 插件及注解处理）

## 构建

在项目根目录执行：

```sh
mvn clean package
```
