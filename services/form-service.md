# 表单处理服务

表单处理服务用来处理这种表单提交服务，如联系表单，报名表单和反馈表单，表单整合了通知组件，可以再制定表单提交后，像响应的邮箱发送邮件、短信通知。

每个表单可以配置单独的通知方式，和通知邮件模板，表单再提交的时候需要提交唯一的 `clientId` 信息来匹配配置信息。

## 使用方法

### 环境变量

```yaml
MAIL_APP_ID: 阿里邮件的APP ID
MAIL_SECRET: 阿里邮件的密钥
MAIL_TIMEOUT: 阿里邮件服务超时时间
SEND_EMAIL_ADDRESS: 阿里邮件发送人地址
RECAPTCHA_SECRET: reCaptcha 服务端密钥
RECAPTCHA_TIMEOUT: reCaptcha 超时时间
```

1. 配置表单配置文件`config.json`
2. 配置前端页面表单提表单的 id 信息。
3. 提交表单

### 表单配置文件说明

// TODO: 待更新

### 提交表单说明

#### POST /api/form/

##### Body

```yaml
clientId: 表单对应的唯一 ID
token: reCaptcha 的客户端验证 token (v3版本)
"...": 其他自义字段
```

##### Response

成功返回值 `statusCode: 201`

```json
{ "status": "success" }
```

失败返回值 `statusCode: 400`

```json
{
  "status": "error",
  "error": {
    "type": "INVALID_TOKEN",
    "message": "无效的验证 token"
  }
}
```
