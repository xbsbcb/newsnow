# NewsNow 项目结构分析

## 项目概述

NewsNow 是一个开源的 RSS/新闻聚合平台，支持多个新闻源的数据聚合。

## 目录结构

```
newsnow/
├── index.html              # 入口 HTML
├── package.json            # 项目配置
├── nitro.config.ts         # Nitro 服务器配置
├── pwa.config.ts          # PWA 配置
├── vite.config.ts         # Vite 配置
├── uno.config.ts          # UnoCSS 配置
│
├── src/                   # 前端源代码
│   ├── main.tsx           # 前端入口
│   ├── routeTree.gen.ts   # 路由树（自动生成）
│   ├── atoms/             # 状态管理原子
│   ├── components/        # React 组件
│   │   └── column/        # 栏目相关组件
│   ├── hooks/             # 自定义 Hooks
│   ├── routes/           # 路由页面
│   ├── styles/            # 样式文件
│   └── utils/            # 前端工具函数
│
├── server/                # 后端源代码
│   ├── api/               # API 路由
│   │   ├── latest.ts      # 获取最新内容
│   │   ├── login.ts       # 登录接口
│   │   ├── oauth/         # OAuth 认证
│   │   ├── me/            # 用户相关接口
│   │   └── s/             # 内容接口
│   ├── database/          # 数据库相关
│   │   ├── cache.ts       # 缓存处理
│   │   └── user.ts       # 用户数据
│   ├── middleware/        # 中间件
│   │   └── auth.ts        # 认证中间件
│   ├── sources/           # 新闻源解析器
│   │   ├── baidu.ts       # 百度
│   │   ├── bilibili.ts    # 哔哩哔哩
│   │   ├── zhihu.ts       # 知乎
│   │   ├── weibo.ts       # 微博
│   │   ├── github.ts      # GitHub
│   │   ├── v2ex.ts        # V2EX
│   │   ├── ithome.ts      # IT之家
│   │   ├── sspai.ts       #少数派
│   │   └── ... (更多新闻源)
│   ├── utils/             # 后端工具函数
│   │   ├── fetch.ts       # 网络请求
│   │   ├── date.ts        # 日期处理
│   │   ├── logger.ts      # 日志
│   │   └── rss2json.ts    # RSS 转 JSON
│   └── types.ts           # 后端类型定义
│
├── shared/                # 前后端共享
│   ├── types.ts           # 共享类型
│   ├── sources.ts         # 新闻源配置
│   ├── consts.ts          # 常量
│   └── utils.ts           # 共享工具
│
├── public/                # 静态资源
│   └── sw.js             # Service Worker
│
├── scripts/               # 构建脚本
│   ├── favicon.ts        # 图标生成
│   └── source.ts         # 数据源脚本
│
├── test/                  # 测试文件
├── tools/                 # 工具脚本
├── docs/                  # 文档目录
└── screenshots/           # 截图
```

## 技术栈

| 层级 | 技术 |
|------|------|
| 前端框架 | React + TypeScript |
| 构建工具 | Vite |
| 后端框架 | Nitro |
| 样式方案 | UnoCSS |
| 状态管理 | Jotai (atoms) |
| 数据源 | 40+ RSS/API 新闻源 |

## 新闻源列表 (server/sources/)

- **科技/开发者**: github, v2ex, solidot, hackernews, juejin, sspai, ithome
- **社交/社区**: zhihu, weibo, douban, tieba, coolapk, linuxdo, nowcoder
- **视频/娱乐**: bilibili, douyin, kuaishou, iqiyi, qqvideo, steam
- **新闻/财经**: ifeng, thepaper, wallstreetcn, zaobao, jin10, 36kr, smzdm
- **其他**: baidu, tencent, toutiao, xueqiu, fastbull, freebuf, gelonghui 等

## API 设计

- `GET /api/latest` - 获取最新内容
- `POST /api/login` - 用户登录
- `GET /api/me` - 获取当前用户信息
- `POST /api/s/entire` - 获取全部内容
- `GET /api/s` - 获取内容列表
