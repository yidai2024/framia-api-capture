# Framia.pro API 接口抓取报告

> 抓取时间: 2026-04-14
> 网站: https://framia.pro
> 状态: **地区限制** — 中国大陆 IP 无法访问
> 邀请链接: https://framia.pro/?invite_code=A2RAPVDB

---

## 一、平台概述

**Framia** 是一个 AI 图像/视频生成平台，但从中国大陆访问会返回 403 错误。

**403 页面信息：**
```
服务暂不可用

由于国家法律法规的相关要求，Framia 的服务暂时无法在您当前所在的地区提供服务。
我们对此深表歉意，感谢您的理解。

💬 加入微信群了解最新信息
```

---

## 二、技术信息

### 2.1 域名

| 域名 | 用途 |
|------|------|
| `framia.pro` | 主站 |
| `assets-cdn.framia.pro` | CDN 资源 |
| `static.cloudflareinsights.com` | Cloudflare 分析 |

### 2.2 CDN/防护

- **Cloudflare** — 使用 Cloudflare CDN 和防护
- **Cloudflare Beacon Token**: `89398c55bd144c49a8e5803a4e3bdc50`
- **Cloudflare RUM**: `/cdn-cgi/rum` (Real User Monitoring)

### 2.3 猜测的页面路由

从页面结构和常见 AI 平台模式推断：

| 路由 | 说明 | 状态 |
|------|------|------|
| `/` | 首页 | 403 (地区限制) |
| `/?invite_code=A2RAPVDB` | 邀请注册页 | 403 |
| `/create` | 创作页 | 403 |
| `/workspace` | 工作台 | 403 |
| `/login` | 登录 | 403 |
| `/signup` | 注册 | 403 |
| `/pricing` | 价格 | 403 |
| `/gallery` | 画廊 | 403 |
| `/templates` | 模板 | 403 |
| `/models` | 模型 | 403 |
| `/community` | 社区 | 403 |
| `/settings` | 设置 | 403 |
| `/profile` | 个人 | 403 |
| `/billing` | 账单 | 403 |
| `/credits` | 积分 | 403 |
| `/referral` | 推荐/邀请 | 403 |
| `/docs` | 文档 | 403 |

### 2.4 猜测的 API 端点

基于类似 AI 平台的常见 API 结构：

```
# 用户/认证
POST /api/auth/login
POST /api/auth/register
GET  /api/auth/session
POST /api/auth/invite-code/verify

# 作品
GET  /api/works/list
GET  /api/works/<id>
POST /api/works/create
POST /api/works/generate

# 模型
GET  /api/models/list
GET  /api/models/<id>

# 积分/订阅
GET  /api/credits/balance
GET  /api/subscription/info
POST /api/subscription/purchase

# 邀请
GET  /api/invite/info
POST /api/invite/verify-code
GET  /api/invite/rewards
```

---

## 三、抓取结果

### 3.1 请求统计

| 域名 | 请求数 |
|------|--------|
| `framia.pro` | 20 |
| `static.cloudflareinsights.com` | 1 |
| **总计** | **21** |

### 3.2 实际捕获的端点

| 方法 | 端点 | 状态 | 说明 |
|------|------|------|------|
| GET | `/` | 403 | 地区限制 |
| GET | `/cdn-cgi/speculation` | 200 | Cloudflare 预取规则 |
| POST | `/cdn-cgi/rum` | 204 | Cloudflare RUM 数据上报 |
| GET | `/*` (所有路径) | 403 | 地区限制 |

### 3.3 Cloudflare 配置泄露

```
Cloudflare Beacon 配置:
{
  "version": "2024.11.0",
  "token": "89398c55bd144c49a8e5803a4e3bdc50",
  "server_timing": {
    "name": {
      "cfCacheStatus": true,
      "cfEdge": true,
      "cfExtPri": true,
      "cfL4": true,
      "cfOrigin": true,
      "cfSpeedBrain": true
    }
  }
}
```

### 3.4 CDN 资源

```
https://assets-cdn.framia.pro/QRCode.png  — 微信群二维码
```

---

## 四、邀请系统分析

### 4.1 邀请链接格式

```
https://framia.pro/?invite_code=A2RAPVDB
```

**邀请码**: `A2RAPVDB`
**格式**: 8位大写字母+数字

### 4.2 推测的邀请机制

- 邀请码在 URL 参数中传递
- 可能存储在 localStorage/cookie 中
- 注册时验证邀请码
- 双方获得积分/奖励

---

## 五、安全发现

### 5.1 Cloudflare Token 泄露

- Beacon Token: `89398c55bd144c49a8e5803a4e3bdc50`
- 用于 Cloudflare 分析，风险较低

### 5.2 地区限制绕过

- 使用海外代理/VPN 可以访问
- 限制基于 IP 地理位置
- 页面提示加入微信群了解最新信息

---

## 六、绕过地区限制的方法（仅供研究）

如果需要进一步抓取 API：

1. 使用海外代理/VPN
2. 使用海外云服务器 (AWS/GCP/Azure)
3. 使用 Cloudflare Workers 代理
4. 使用 Playwright + 代理配置

```python
# 使用代理访问
browser = p.chromium.launch(
    headless=True,
    proxy={"server": "http://海外代理:端口"}
)
```

---

## 七、结论

Framia.pro 在中国大陆被 **完全封锁**（403），无法抓取到实际 API。

**已知信息**:
- 平台名称: Framia
- CDN: Cloudflare
- 资源CDN: assets-cdn.framia.pro
- 邀请码格式: 8位大写字母+数字
- 有微信群维护用户

**如需完整抓取**，需要使用海外网络环境。

---

*文档由 Playwright 自动抓取生成*
