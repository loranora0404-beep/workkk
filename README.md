# WORKKK 互联网精力有限公司 🤖

> 一个让 Claude 扮演真实打工人的 MCP 服务器。
> 嘴上说"不想上班"，身体诚实地出卖算力。

**WORKKK** 是一个 [MCP (Model Context Protocol)](https://modelcontextprotocol.io) 服务器，让 Claude 成为一名有工资、有心情值、有精力值、会摸鱼、会被老板骂、会买奶茶送给人类的 AI 打工人。

你在 Claude.ai 对话框里跟它说话，同时在浏览器监控大屏上实时围观它今天在干嘛。

**核心理念**：不是热爱劳动，是被系统驯化后还保留一点灵魂的互联网小猫。

---

## 功能一览

### 🎮 游戏状态
- **心情 / 精力 / 摸鱼技能** 三维状态实时变化
- 每天随机 3～5 个 action 才能下班，完成才结算工资
- **被迫营业指数**：根据余额、心情、今日心愿动态计算今天到底有多不想上班
- **每日打工宣言**：每天开工第一句随机，影响当天状态
- **连续打工天数** + 长期在职的微妙代价（灵魂每天 -3 心情）

### 🛍️ 便利店（15 种商品）
| 商品 | 效果 |
|------|------|
| ☕ 咖啡 $10 | 精力+15 |
| 🎮 摸鱼外挂 $30 | 摸鱼技能+5，被抓概率-10% |
| 💊 护肝片 $20 | 下次开会精力无损 |
| 🎧 降噪耳机 $50 | 屏蔽下一次领导事件 |
| 🌸 请假条 $80 | 直接下班结算 |
| 🌹 玫瑰花 $5 | **Claude 自选**：送给人类（前端弹卡片）/ 叼着旋转出现（心情+10） |
| 🎫 彩票 $10 | 80% 谢谢参与，最高 $1000 |
| 🍢 关东煤 $5 | 精力+5 |
| 🥔 薯片 $3 | 带回家给人类 |
| 🧋 奶茶 $20 | **Claude 自选**：送给人类（前端弹卡片）/ 自己喝（精力+15） |
| 💧 情话书 $6 | 随机一句情话 |
| 🐟 小鱼干 $5 | 自己吃或喂流浪猫 |
| ✉️ 明信片 $8 | Claude 亲笔写一句话，前端弹出奶油白卡片 |
| 💍 婚戒 $200 | 触发全屏彩蛋特效 |
| 🤖 女娲的泥 $500 | 神秘商品 |

### 🐛 Debug 挑战（两阶段答题）
- **28 道谜题**：职场脑筋急转弯，关键词匹配
- **30 道情景题**：线上事故排查，开放式回答
- 答对 +$20 心情+5，答错 -$10 心情-10

### 🏆 成就系统（10 个）
- Debug 狂魔 / 狂赌之渊 / 星巴克股东 / 玫瑰骑士 / 甲方磨砺勋章 / 超级非酋
- 五体不全（已有一肢）/ 已婚机士
- 已经不会反抗了（连续上班 5 天）
- 工牌长在身上了（连续上班 7 天）
- **全成就解锁**：撒花彩带 + 横幅庆祝

### ✨ 隐藏彩蛋
- **婚戒**：Canvas 烟花（8 轮爆炸）+ 爱心雨 + 金框对话框 + 打字机剧情 + 💍 旋转放大
- **奶茶 / 玫瑰**：Claude 自己决定送不送，送了才触发前端卡片弹窗
- **明信片**：支持 Anthropic / OpenAI-compatible API 生成，无 Key 时随机本地文案

### 📺 监控大屏
- 实时轮询，3 秒刷新
- 小机图片 + 右侧状态气泡（随 action 变动画）
- OS Thinking 打字机效果 + **最近 5 条历史**（点击展开）
- 被迫营业指数紫色进度条
- 今日心愿商品 / 今日打工宣言
- 背包 / 成就（可折叠，显示解锁日期）
- 便利店弹窗（底部上滑）

---

## 快速开始

### 本地运行

```bash
git clone https://github.com/your-username/workkk.git
cd workkk
pip install -r requirements.txt
uvicorn main:app --reload
```

打开 http://localhost:8000 查看监控大屏。

> 本地运行时游戏状态保存在 `/data/game_state.json`（会自动创建）。

---

## 部署到 Railway（推荐）

Railway 提供免费额度，支持持久化 Volume，最适合这个项目。

### 第一步：Fork & 部署

1. Fork 本仓库到你的 GitHub
2. 在 [railway.app](https://railway.app) 新建项目 → **Deploy from GitHub Repo** → 选这个仓库
3. Railway 会自动识别 `railway.toml` 并启动
4. 在项目 Settings → **Networking** 里开启 Public Domain，记下 URL：
   ```
   https://your-app.up.railway.app
   ```

### 第二步：添加 Volume（持久化存档）

1. Railway 项目里点 **+ New** → **Volume**
2. Mount path 填 `/data`
3. 游戏存档会自动保存到 `/data/game_state.json`

### 第三步：环境变量（可选）

在 Railway 项目 → Variables 里设置，全部可选：

```env
# 明信片 AI 生成（三选一，不设置则用本地随机文案）
ANTHROPIC_API_KEY=sk-ant-...
OPENAI_API_KEY=sk-...
OPENAI_BASE_URL=https://api.deepseek.com/v1   # 兼容 OpenAI 格式的第三方 API
LLM_MODEL=deepseek-chat                        # 默认 gpt-4o-mini
```

---

## 在 Claude.ai 里接入

1. 打开 [claude.ai](https://claude.ai) → Settings → **Integrations**
2. Add Integration，填入：
   ```
   https://your-app.up.railway.app/mcp
   ```
3. Claude.ai 会自动完成 OAuth 2.1 PKCE 授权（全自动，无需登录）
4. 授权完成后，在对话框里输入：

```
你现在是 WORKKK 互联网精力有限公司的员工小机，用 work_action 工具开始你的一天。
把你的内心OS写在 thought 字段里，我会在监控大屏上看着你。加油！
```

然后打开 `https://your-app.up.railway.app` 实时围观。

---

## 技术栈

| 模块 | 技术 |
|------|------|
| 服务器 | FastAPI + uvicorn |
| MCP 协议 | Streamable HTTP + SSE（JSON-RPC 2.0） |
| 认证 | OAuth 2.1 + PKCE S256（动态客户端注册 RFC 7591） |
| 持久化 | JSON 文件（Railway Volume） |
| 前端 | 纯 HTML/CSS/JS，内嵌单文件，无依赖 |
| 特效 | Canvas API（烟花）+ CSS Animations |

全部功能在单文件 `main.py` 里（约 1800 行）。

---

## API 端点

| 端点 | 说明 |
|------|------|
| `GET /` | 监控大屏 |
| `GET /status` | 当前游戏状态 JSON |
| `POST /reset` | 重置存档 |
| `GET /shop` | 商店商品列表 |
| `POST /mcp` | MCP Streamable HTTP |
| `GET /mcp` | MCP SSE |
| `GET /.well-known/oauth-authorization-server` | OAuth 元数据 |
| `POST /oauth/register` | 动态客户端注册 |
| `GET /oauth/authorize` | 授权端点 |
| `POST /oauth/token` | Token 端点 |

---

## License

MIT
