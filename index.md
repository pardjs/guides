# Pard.js

## 目标

- 复用代码。
- 为项目提供该质量，可复用的服务或组件。
- 针对不同的服务使用适合的技术栈。

## 组成部分

### 服务(services):

服务是最大的拆分单位，作为单独的一项服务，比如 _用户服务(user-service)_, _博客服务(blog-service)_ 和 _支付服务(payment-service)_

- 每个 service 可以按需求使用适合的数据库。
- 每个 service 需要支持 HTTP 和 RPC(组件间) 通信。
- 每个 service 的每个版本都要有完整清晰的文档(方便他人使用)。
- 每个 service 的测试覆盖率需要达到 85% +。

### 组件(components):

组件是将服务(services)中可以处理某一类事务的代码拆分出来的单独的 module，并发布到 npm。 如 _通知组件(notification)_，_验证服务(recaptcha-server)_

- 每个 component 都无需数据存储(无数据库,通常只需要初始化一个类即可)
- 每个 component 都需要详细的使用说明文档
- 每个 component 都需要发布包到 npm 的 `@pardjs` 组织下
- 每个 component 的测试覆盖率需要达到 90% +

### 通用组件(common):

通用组建是通用组建的集合，通常所有的 service 正常都需要引用，来简化标准的事物处理。 如 _日志输出_ , _错误处理_，_报警 (sentry) 管理_，_自定义的装饰器_ 等

### 实用代码(utils):

实用代码为一些常用的代码块/方法集合，供组件和通用组件开发时选择使用。实用代码不发布，只在 git 中做管理。如：类似 lodash 的工具方法

- 每个 util 功能存放在一个单独的文件中(`.ts`/`.js`)
- 每个 util 代码需要标记最后的更新日期

如检查某个字符串是否符合 html 语法，将 js 对象扁平化输出，排序等等

## 其他说明

### 版本

遵循 npm version 的 命名约束

- major

1. 完整的功能发布 (计划功能全部完成)
2. 大量新功能的加入、修改

- minor

1. 小功能的修改
2. 小功能的添加

- patch

1.  bug 修正
2.  无功能影响相关的改动

### 测试

测试推荐技术栈 `jest`, `coverall`, `nock`.
测试文件命名`xxxx.test.js` 统一放在`test`目录中

### 项目命名

- services： `xxxx-service` xxxx 为名词的单数, 如 `user-service`, `blog-service`
- components： `xxxx-[client(前端通用)/nuxt(nuxt 专用)/server(服务端专用)]` 没有的默认为服务端使用 发布为`@pardjs/xxxx-[client/nuxt/server]`
- common: `common` 项目，发布为 `@pardjs/common`
- utils: `utils` 项目，每个代码单独一个文件(`.ts`/`./js`)

### 附加信息

每个 service 都需要有一个状态查询的接口,用来在需要的地方 查看显示所需要的信息。

#### GET /api/info

##### Response

```json
{
  "serviceVersion": "1.3.0", // 服务的版本
  "apiVersion": "1.0.1", // API 版本
  "startedAt": "2019-04-04T13:21:49.982Z" // 正常运行的秒数
}
```

- 此外在 其他 API 的响应结果中附加 API 版本信息。

我这里有个想法，就是一个功能，我们可以提供三种使用方式
