# OpenDragon

<div align="center">

**基于微服务、大数据和 AI 的虚拟人系统**

[![License](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](LICENSE)
[![Java Version](https://img.shields.io/badge/Java-17-orange.svg)](https://openjdk.org/projects/jdk/17/)
[![Spring Boot](https://img.shields.io/badge/Spring%20Boot-3.2.0-brightgreen.svg)](https://spring.io/projects/spring-boot)

[文档](#文档) | [快速开始](#快速开始) | [API 文档](#api-文档) | [贡献指南](#贡献指南)

</div>

---

## 项目简介

OpenDragon 是一个企业级的虚拟人系统平台,采用微服务架构,集成了人工智能、大数据处理等先进技术,为用户提供智能化的虚拟人交互服务。

### 核心特性

- 🚀 **微服务架构** - 基于 Spring Boot 的分布式系统设计
- 🔐 **统一认证授权** - 完整的 IDaaS 身份管理解决方案
- 🤖 **AI 集成** - 支持智能对话和虚拟人交互
- 📊 **大数据处理** - 高效的数据采集、存储和分析
- 🔧 **多环境支持** - 本地、开发、测试、生产等环境一键切换

---

## 技术栈

### 后端技术

| 技术 | 版本 | 说明 |
|------|------|------|
| Java | 17 | 编程语言 |
| Spring Boot | 3.2.0 | 应用框架 |
| Spring Security | 6.2.0 | 安全框架 |
| Spring Data JPA | - | 数据持久化 |
| JWT | 0.11.5 | 令牌认证 |
| H2 Database | - | 开发环境数据库 |
| MySQL | 8.0+ | 生产环境数据库 |
| Lombok | 1.18.30 | 代码简化 |
| Hutool | 5.8.22 | 工具库 |
| Swagger/OpenAPI | 2.2.0 | API 文档 |

### 架构设计

- **DDD 分层架构** - Domain-Driven Design 领域驱动设计
- **RBAC 权限模型** - 基于角色的访问控制
- **RESTful API** - REST 架构风格
- **Maven 多模块** - 模块化项目结构

---

## 模块说明

### IDaaS 模块

身份即服务(IDaaS)模块,提供完整的用户认证和授权功能。

#### 功能特性

- **用户管理** - 用户注册、登录、信息维护
- **角色管理** - 角色创建、分配、权限绑定
- **部门管理** - 组织架构管理、层级关系维护
- **菜单管理** - 系统菜单配置、权限控制
- **权限管理** - 细粒度权限控制、RBAC 模型
- **JWT 认证** - 基于 Token 的无状态认证
- **API 文档** - Swagger 自动生成接口文档

详细信息请查看 [idaas-module/README.md](idaas-module/README.md)

---

## 快速开始

### 环境要求

- **JDK**: 17 或更高版本
- **Maven**: 3.6+
- **操作系统**: Windows / Linux / macOS

### 安装步骤

#### 1. 克隆仓库

```bash
git clone https://github.com/qoobot/opendragon.git
cd opendragon
```

#### 2. 编译项目

```bash
# 完整编译(包含测试)
mvn clean install

# 跳过测试编译
mvn clean install -DskipTests

# 编译特定模块
mvn clean install -pl idaas-module -am
```

#### 3. 启动服务

##### 启动 IDaaS 模块

**Windows:**
```bash
cd idaas-module
start.bat
```

**Linux/macOS:**
```bash
cd idaas-module
./mvnw spring-boot:run
```

或使用 Maven:
```bash
mvn spring-boot:run -pl idaas-module
```

#### 4. 访问服务

启动成功后,可通过以下地址访问服务:

| 服务 | 地址 | 说明 |
|------|------|------|
| IDaaS 服务 | http://localhost:8080/idaas | 主服务地址 |
| Swagger UI | http://localhost:8080/idaas/swagger-ui.html | API 文档 |
| H2 控制台 | http://localhost:8080/idaas/h2-console | 数据库管理 |

---

## 环境配置

项目支持多环境配置,通过 Maven Profile 管理不同环境的构建和部署。

### 环境列表

| 环境 | 名称 | Maven Profile | 版本后缀 | 说明 |
|------|------|----------------|----------|------|
| Local | 本地开发 | `local` | SNAPSHOT | 开发者本地环境(默认) |
| Dev | 开发环境 | `dev` | SNAPSHOT | 开发团队联调环境 |
| Test | 测试环境 | `test` | Alpha | 功能测试环境 |
| SIT | 系统集成测试 | `sit` | Beta | 模块集成测试环境 |
| UAT | 用户验收测试 | `uat` | RC.1 | 业务验收测试环境 |
| Pre | 预生产环境 | `pre` | RC.2 | 上线前验证环境 |
| Prod | 生产环境 | `prod` | Release | 正式线上环境 |

### 使用示例

```bash
# 构建开发环境版本
mvn clean install -P dev

# 构建测试环境版本
mvn clean install -P test

# 构建生产环境版本
mvn clean install -P prod

# 打包指定环境
mvn clean package -P prod
```

---

## 项目结构

```
opendragon/
├── idaas-module/                    # IDaaS 身份认证模块
│   ├── src/
│   │   ├── main/
│   │   │   ├── java/com/qoobot/idaas/
│   │   │   │   ├── application/    # 应用服务层
│   │   │   │   ├── domain/         # 领域模型层
│   │   │   │   ├── infrastructure/# 基础设施层
│   │   │   │   ├── interfaces/     # 接口层
│   │   │   │   └── common/         # 公共组件
│   │   │   └── resources/
│   │   │       └── application.yml # 配置文件
│   │   └── test/                   # 测试代码
│   ├── pom.xml                     # 模块 POM
│   ├── start.bat                   # Windows 启动脚本
│   └── README.md                   # 模块说明文档
├── src/                            # 公共资源
├── pom.xml                         # 父 POM 配置
├── LICENSE                         # 开源许可证
└── README.md                       # 项目说明文档
```

### IDaaS 模块详细结构

```
idaas-module/
├── application/                    # 应用层
│   └── service/                    # 业务服务
│       ├── UserService.java
│       ├── RoleService.java
│       ├── DepartmentService.java
│       ├── MenuService.java
│       └── PermissionService.java
├── domain/                         # 领域层
│   ├── model/                      # 实体模型
│   │   ├── User.java
│   │   ├── Role.java
│   │   ├── Department.java
│   │   ├── Menu.java
│   │   └── Permission.java
│   └── repository/                 # 数据仓库
│       ├── UserRepository.java
│       ├── RoleRepository.java
│       ├── DepartmentRepository.java
│       ├── MenuRepository.java
│       └── PermissionRepository.java
├── infrastructure/                 # 基础设施层
│   └── config/                     # 配置类
│       ├── SecurityConfig.java
│       ├── JwtTokenProvider.java
│       ├── JwtAuthenticationFilter.java
│       ├── CustomUserDetailsService.java
│       └── IdaasConfig.java
└── interfaces/                     # 接口层
    ├── controller/                 # 控制器
    │   ├── UserController.java
    │   ├── RoleController.java
    │   ├── DepartmentController.java
    │   ├── MenuController.java
    │   └── PermissionController.java
    └── dto/                        # 数据传输对象
        ├── UserDTO.java
        ├── RoleDTO.java
        ├── DepartmentDTO.java
        ├── MenuDTO.java
        ├── PermissionDTO.java
        └── LoginRequestDTO.java
```

---

## API 文档

### Swagger UI

启动服务后,访问 Swagger UI 查看完整的 API 文档:

- **地址**: http://localhost:8080/idaas/swagger-ui.html
- **OpenAPI JSON**: http://localhost:8080/idaas/v3/api-docs

### 主要接口

#### 认证相关

| 方法 | 路径 | 说明 |
|------|------|------|
| POST | `/api/auth/login` | 用户登录 |
| POST | `/api/auth/register` | 用户注册 |
| GET | `/api/auth/profile` | 获取用户信息 |

#### 用户管理

| 方法 | 路径 | 说明 |
|------|------|------|
| GET | `/api/users` | 获取用户列表 |
| POST | `/api/users` | 创建用户 |
| PUT | `/api/users/{id}` | 更新用户 |
| DELETE | `/api/users/{id}` | 删除用户 |

#### 角色管理

| 方法 | 路径 | 说明 |
|------|------|------|
| GET | `/api/roles` | 获取角色列表 |
| POST | `/api/roles` | 创建角色 |
| PUT | `/api/roles/{id}` | 更新角色 |
| DELETE | `/api/roles/{id}` | 删除角色 |

#### 部门管理

| 方法 | 路径 | 说明 |
|------|------|------|
| GET | `/api/departments` | 获取部门列表 |
| GET | `/api/departments/tree` | 获取部门树 |
| POST | `/api/departments` | 创建部门 |
| PUT | `/api/departments/{id}` | 更新部门 |

#### 菜单管理

| 方法 | 路径 | 说明 |
|------|------|------|
| GET | `/api/menus` | 获取菜单列表 |
| GET | `/api/menus/tree` | 获取菜单树 |
| POST | `/api/menus` | 创建菜单 |
| PUT | `/api/menus/{id}` | 更新菜单 |

---

## 测试

### 运行测试

```bash
# 运行所有测试
mvn test

# 运行特定模块测试
mvn test -pl idaas-module

# 跳过测试
mvn clean install -DskipTests

# 生成测试报告
mvn test surefire-report:report
```

### 测试账户

| 用户名 | 密码 | 角色 | 说明 |
|--------|------|------|------|
| admin | admin123 | 系统管理员 | 拥有所有权限 |

**注意**: 生产环境请修改默认账户密码!

---

## 构建与部署

### 本地构建

```bash
# 打包为 JAR
mvn clean package

# 打包并跳过测试
mvn clean package -DskipTests

# 打包指定环境
mvn clean package -P prod
```

### Docker 部署

```bash
# 构建镜像
docker build -t opendragon:latest .

# 运行容器
docker run -d \
  --name opendragon \
  -p 8080:8080 \
  opendragon:latest

# 查看日志
docker logs -f opendragon

# 停止容器
docker stop opendragon
docker rm opendragon
```

### 生产环境部署

```bash
# 构建生产版本
mvn clean package -P prod

# 运行 JAR
java -jar idaas-module/target/idaas-module-10.5.0-Release.jar

# 指定配置文件运行
java -jar idaas-module/target/idaas-module-10.5.0-Release.jar \
  --spring.profiles.active=prod
```

---

## 配置说明

### 数据库配置

开发环境使用 H2 内存数据库,生产环境建议使用 MySQL。

**H2 配置(默认)**:
```yaml
spring:
  datasource:
    url: jdbc:h2:mem:idaasdb;DB_CLOSE_DELAY=-1
    driver-class-name: org.h2.Driver
    username: sa
    password:
```

**MySQL 配置**:
```yaml
spring:
  datasource:
    url: jdbc:mysql://localhost:3306/idaasdb?useSSL=false&serverTimezone=UTC
    driver-class-name: com.mysql.cj.jdbc.Driver
    username: root
    password: your_password
```

### JWT 配置

```yaml
app:
  jwt:
    secret: your-secret-key-must-be-long-enough
    expiration: 3600000        # 1小时
    refresh-expiration: 86400000 # 24小时
```

**安全提示**: 生产环境务必修改 JWT 密钥为复杂的随机字符串!

---

## 开发指南

### 代码规范

1. **命名规范**
   - 类名: 大驼峰命名法 (PascalCase)
   - 方法名: 小驼峰命名法 (camelCase)
   - 常量: 全大写下划线分隔 (UPPER_SNAKE_CASE)

2. **注释规范**
   - 所有公共类和方法必须添加 Javadoc 注释
   - 复杂逻辑添加行内注释说明

3. **分层架构**
   - **interfaces**: 处理 HTTP 请求和响应,不包含业务逻辑
   - **application**: 编排业务流程,协调领域服务
   - **domain**: 核心业务逻辑和领域模型
   - **infrastructure**: 技术实现,如数据库、外部 API

### Git 工作流

```bash
# 创建特性分支
git checkout -b feature/your-feature-name

# 提交更改
git add .
git commit -m "feat: add new feature"

# 推送到远程
git push origin feature/your-feature-name

# 创建 Pull Request
```

### 提交信息规范

遵循 [Conventional Commits](https://www.conventionalcommits.org/) 规范:

- `feat:` 新功能
- `fix:` 修复 bug
- `docs:` 文档更新
- `style:` 代码格式调整
- `refactor:` 重构
- `test:` 测试相关
- `chore:` 构建/工具相关

---

## 常见问题

### Q1: 如何切换到 MySQL 数据库?

A: 修改 `application.yml` 中的数据源配置,并确保已添加 MySQL 驱动依赖。

### Q2: 如何修改 JWT 密钥和过期时间?

A: 在配置文件中修改 `app.jwt.secret` 和 `app.jwt.expiration` 属性。

### Q3: 如何添加新的业务模块?

A: 参照 `idaas-module` 的结构,创建新的子模块,并在父 POM 的 `<modules>` 中声明。

### Q4: 如何启用 HTTPS?

A: 在 `application.yml` 中配置 SSL 证书和端口,或使用 Nginx 反向代理。

### Q5: 开发环境如何热加载?

A: 已集成 `spring-boot-devtools`,修改代码后会自动重启应用。

---

## 路线图

### 已完成 ✅

- [x] 项目基础架构搭建
- [x] IDaaS 身份认证模块
- [x] RBAC 权限模型
- [x] 多环境配置支持
- [x] Swagger API 文档
- [x] JWT 认证机制

### 计划中 📋

- [ ] 虚拟人对话模块
- [ ] 大数据分析模块
- [ ] 消息推送服务
- [ ] 监控告警系统
- [ ] 容器化部署
- [ ] CI/CD 流水线

---

## 贡献指南

我们欢迎所有形式的贡献!

### 如何贡献

1. Fork 本仓库
2. 创建特性分支 (`git checkout -b feature/AmazingFeature`)
3. 提交更改 (`git commit -m 'Add some AmazingFeature'`)
4. 推送到分支 (`git push origin feature/AmazingFeature`)
5. 提交 Pull Request

### 代码审查

所有 Pull Request 都需要通过代码审查后才能合并。

### 报告问题

在提交 Issue 时,请提供:
- 问题描述
- 复现步骤
- 预期行为
- 实际行为
- 环境信息(系统、JDK 版本等)

---

## 许可证

本项目采用 [Apache License 2.0](LICENSE) 开源许可证。

```
Copyright 2026 OpenDragon Team

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

    http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
```

---

## 联系方式

- **项目负责人**: Team Lead
- **邮箱**: parker_1225@163.com
- **GitHub**: https://github.com/qoobot/opendragon
- **问题反馈**: [GitHub Issues](https://github.com/qoobot/opendragon/issues)

---

## 致谢

感谢所有为 OpenDragon 项目做出贡献的开发者!

---

<div align="center">

**Made with ❤️ by OpenDragon Team**

[⬆ 回到顶部](#opendragon)

</div>
