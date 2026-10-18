# 宝石工坊

GitHub Pages 单页桌游，支持电脑对战、本地轮流双人和通过 Supabase Realtime 房间联机。仓库默认分支 `main` 是已发布稳定版；本次更新请先在 `codex/gem-game-upgrade` 分支预览，再通过 Pull Request 合并。

## 游戏规则（简化版）

- 每回合拿 3 种不同颜色各 1 枚，或拿同色 2 枚（供应区至少有 4 枚），或购买一张发展卡。
- 使用原版基础游戏完整的 90 张发展卡（一级 40、二级 30、三级 20），每局每级公开 4 张；卡牌费用、颜色、折扣和分数按基础游戏牌表。贵族使用基础游戏 10 张牌，每局随机展示 3 张。
- 持有超过 10 枚宝石时，归还宝石至 10 枚后才结束回合。
- 达到贵族条件时自动获得 3 分；任一玩家达到 15 分即获胜。
- 电脑使用贪心策略选择可购买的高分卡，其余时候按目标卡补充宝石。

## GitHub Pages 发布

仓库 Settings → Pages 中使用 `Deploy from a branch`、`main`、`/(root)`。合并升级 Pull Request 后，Pages 会从 main 自动重新构建；也可以先在升级分支的 GitHub Actions/临时预览环境检查。

## 好友联机（可选）

联机需要一个 Supabase 项目。该模式仅通过 Supabase Realtime Broadcast 同步对局状态，不创建数据库表：

1. 在 Supabase 创建 Free 项目。
2. 打开项目设置中的 API 页面，复制 Project URL 和 anon/public（publishable）key。**不要复制或填写 `service_role` / secret key。**
3. 打开网页，选择“好友联机”，填写 URL 和 public key，保存连接设置。
4. 一人创建房间，把 6 位房间码发给朋友；朋友填写同一 URL/key 和房间码后加入。

public key 本来就会公开在静态网页中，安全边界是它只能访问被配置允许的资源。本页面不使用 service-role key，也不写入数据库。房间码是轻量邀请口令；这是适合熟人试玩的原型联机，不提供账号、反作弊、私密房间或断线重连保证。不要在此模式分享个人信息。Supabase Free 项目可能因长期不活跃而暂停；当前套餐额度请以 Supabase 控制台为准。

## 本地验证

无需安装依赖。用浏览器直接打开 `index.html` 即可玩电脑或本地双人模式；在线模式需要联网加载 Supabase JavaScript 客户端并配置项目。



牌表数据参考发行方规则书和公开基础游戏牌表；代码中的卡牌费用、奖励颜色、分值与贵族要求按原版基础游戏数据整理，贵族姓名采用中文译名。
