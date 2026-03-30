---
layout: default
title: 2026 NestJS 全栈技术栈完整方案：Monorepo 架构设计
no_duoshuo: false
permalink: /nestjs-fullstack-tech-stack-2026/
---

# 2026 NestJS 全栈技术栈完整方案

经过深入调研和对比，我为需要企业级后端的项目整理了一套完整的推荐技术栈。这套方案覆盖 Web、Admin、Mobile 三个端，特点是"大而全"，避免后续重构。

---

## AI 项目初始化提示词

> 以下提示词可复制给 AI，帮助快速初始化项目

```
请帮我初始化一个 Monorepo 项目，结构如下：

my-project/
├── apps/
│   ├── web/              # 前端 (Next.js 或 Vite + React)
│   ├── admin/            # 管理后台 (Vite + React + Arco Design)
│   ├── mobile/           # 移动端 (Expo + React Native)
│   └── server/           # NestJS API 后端
├── shared-types/         # 共享类型定义
└── turbo.json

技术栈要求：
- 后端：NestJS + Drizzle ORM + Better Auth + @nestjs/schedule + @nestjs/websockets + Stripe
- 前端构建：Vite / Next.js
- Web UI：Tailwind + shadcn/ui
- Admin UI：Arco Design
- 移动端：Expo + React Native
- i18n：react-i18next (前端) + nestjs-i18n (后端)
- 状态管理：TanStack Query + Zustand

请执行以下步骤：
1. 初始化 pnpm workspace + turbo
2. 创建 NestJS server，安装上述依赖
3. 创建 web 前端
4. 创建 admin 管理后台
5. 创建 mobile 移动端
6. 创建 shared-types 共享类型
7. 配置 CORS、数据库连接、环境变量

端口：server=3000, web=3001, admin=3002, mobile=8081
```

---

## 推荐架构

```
my-project/
├── apps/
│   ├── web/              # 前端 (Next.js 或 Vite + React + i18n)
│   ├── admin/            # 管理后台 (Vite + React + Arco Design)
│   ├── mobile/           # 移动端 (Expo + React Native)
│   └── server/           # NestJS API 后端
├── shared-types/         # 共享类型定义
└── turbo.json
```

---

## 核心技术选型

| 模块 | 推荐方案 | 说明 |
|------|----------|------|
| **后端框架** | NestJS | 企业级架构，模块化、依赖注入、微服务支持 |
| **移动端** | Expo + React Native | 跨平台 iOS/Android，一套代码多端运行 |
| **ORM** | Drizzle / Prisma | Drizzle 轻量高性能，Prisma 上手快 |
| **Auth** | Better Auth | 官方支持 NestJS 集成，完整 Auth 解决方案 |
| **前端构建** | Vite / Next.js | 极速 HMR，Next.js 支持 SSR |
| **前端框架** | React | 生态最大，人才最多 |
| **Web UI** | Tailwind + shadcn/ui | 现代 CSS 框架 + 可定制组件库 |
| **Admin UI** | Arco Design | 完整 admin 组件库，企业级设计 |
| **状态管理** | TanStack Query + Zustand | Query 管服务端状态，Zustand 管客户端状态 |
| **i18n** | react-i18next (前端) + nestjs-i18n (后端) | 完整国际化方案 |
| **支付** | Stripe | 国际标准，API 友好 |
| **实时** | @nestjs/websockets | 原生 WebSocket 支持 |
| **定时任务** | @nestjs/schedule | 原生 Cron 支持 |

---

## 核心模块详解

### 1. ORM - Drizzle 推荐理由

| 特性 | Drizzle | Prisma |
|------|---------|--------|
| 性能 | ✅ 极快 | 中 |
| SQL 控制 | ✅ 接近原生 | 抽象较多 |
| 类型安全 | ✅ 强 | ✅ 强 |
| 迁移体验 | ✅ 好 | ✅ 好 |
| 2026 趋势 | ⬆️ 上升中 | ⬇️ 放缓 |

```typescript
// Drizzle 示例
import { pgTable, serial, text, integer } from 'drizzle-orm/pg-core';

export const users = pgTable('users', {
  id: serial('id').primaryKey(),
  name: text('name').notNull(),
  email: text('email').notNull().unique(),
});

// 类型自动生成
type User = typeof users.$inferSelect;
```

---

### 2. Auth - Better Auth 集成

Better Auth 已官方支持 NestJS，集成简单：

```bash
npm install better-auth nestjs-better-auth
```

```typescript
// main.ts
app.use(bodyParser.json()); // 禁用默认 body parser

// app.module.ts
import { AuthModule } from "nestjs-better-auth";

@Module({
  imports: [AuthModule],
})
export class AppModule {}

// 路由保护
@Controller('posts')
export class PostsController {
  @Get()
  @UseGuards(AuthGuard) // 全局守卫，所有路由受保护
  getPosts(@Session() session: Session) {
    // session.user 包含用户信息
  }
}
```

**优势**：
- 完整 Auth 方案（Email、OAuth、Session）
- 官方 NestJS 支持
- 安全最佳实践内置
- 多 Provider 支持

---

### 3. i18n 完整方案

**前端**：`react-i18next`

```typescript
// i18n.ts
import i18n from 'i18next';
import { initReactI18next } from 'react-i18next';

i18n.use(initReactI18next).init({
  resources: {
    en: { translation: { hello: 'Hello' } },
    zh: { translation: { hello: '你好' } },
  },
});
```

**后端**：`nestjs-i18n`

```typescript
import { I18nModule } from 'nestjs-i18n';

@Module({
  imports: [
    I18nModule.forRoot({
      fallbackLanguage: 'en',
      resolver: AcceptLanguageResolver,
      path: './src/locales',
    }),
  ],
})
export class AppModule {}
```

---

### 4. Web + Admin 双前端方案

**apps/web** — 用户端

- 技术选型：**Next.js** 或 **Vite + React**
- 特点：注重用户体验、SEO（Next.js）、响应式设计
- UI：Tailwind CSS + shadcn/ui

**apps/admin** — 管理后台

- 技术选型：**Vite + React + Arco Design**
- 特点：注重效率、复杂表单、数据可视化
- UI：Arco Design（字节跳动企业级组件库）
- 优势：完整 admin 生态（表格、表单、图表、权限）

```typescript
// Arco Design 示例
import { Button, Table, Form, Input } from '@arco-design/web-react';

const App = () => (
  <div>
    <Form>
      <Form.Item label="用户名">
        <Input placeholder="请输入用户名" />
      </Form.Item>
    </Form>
    <Table columns={columns} data={data} />
  </div>
);
```

**共享层**（shared-types）：
- 类型定义：User、Order、Product 等共享类型

---

### 5. 移动端 - Expo + React Native

**apps/mobile** — 移动端

- 技术选型：**Expo + React Native**
- 特点：跨平台 iOS/Android，一套代码多端运行
- 优势：开发体验接近 Web，快捷预览、Hot Reload

```typescript
// Expo + React Native 示例
import { View, Text, Button } from 'react-native';

export default function App() {
  return (
    <View>
      <Text>Hello Mobile!</Text>
      <Button title="Click me" onPress={() => {}} />
    </View>
  );
}
```

**与 Web 共享**：
- 业务逻辑：自定义 Hooks、工具函数
- 类型定义：shared-types 完全共享
- 部分 UI：简单组件可复用（需要 React Native 适配）

---

### 6. 支付集成 - Stripe

```typescript
import { Stripe } from 'stripe';

@Injectable()
export class PaymentService {
  private stripe: Stripe;

  async createPaymentIntent(amount: number) {
    return this.stripe.paymentIntents.create({
      amount: amount * 100, // 转为分
      currency: 'usd',
    });
  }

  // Webhook 处理
  async handleWebhook(payload: Buffer, signature: string) {
    const event = this.stripe.webhooks.constructEvent(
      payload,
      signature,
      process.env.STRIPE_WEBHOOK_SECRET
    );
    // 处理事件...
  }
}
```

---

## 为什么选这套方案

1. **大而全** — 避免后续重构，每个模块都选好
2. **成熟稳定** — 全部经过大量生产验证
3. **灵活性** — NestJS 模块化，需要可替换
4. **团队一致** — Monorepo 统一规范
5. **未来扩展** — 微服务、WebSocket、定时任务原生支持

---

## 适用场景

| 场景 | 推荐 |
|------|------|
| 中大型项目 | ✅ 完美 |
| 多端应用（Web + Admin + Mobile） | ✅ 完美 |
| 需要企业级后端 | ✅ 完美 |
| 小型/MVP | ⚠️ 可能过度 |
| 单页面应用 | ❌ 不适合 |

---

（2026 年 3 月 30 日）
