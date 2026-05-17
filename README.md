# jerlin-weread-skill

微信读书官方 Skill 的重构版。Agent 不用每次把整份接口文档读一遍再自己重复拼请求，改为一条命令直接调，需要什么查什么。

## 安装

1. 获取 API Key：前往 [weread-skills](https://weread.qq.com/r/weread-skills) 登录微信读书账号
2. 配置环境变量：
```bash
export WEREAD_API_KEY=wrk-你的apikey
```
3. 安装 Skill：
```bash
npx skills add jerlinn/jerlin-weread
```

## 结构

```
├── SKILL.md                意图路由 + 通用规则
├── scripts/weread.sh       CLI, 17 个子命令, -h 查参数和回包
└── references/             语义陷阱、规则、工作流
```

## 面向 Agent 重新设计

1. API 调用收进 CLI 脚本，读 reference 做决策，精准组合对应接口，`-h` 按需查用法
2. 领域知识从示例升维为规则，编码决策边界和语义陷阱
3. 砍掉 Agent 不需要的常识性描述
4. 新增阅读画像构建，组合行为数据和驱动层采集，生成可持续迭代的读者档案

## Credits

基于微信读书官方团队的 [WeRead Skill](https://weread.qq.com/r/weread-skills) 优化。API 接口和数据归微信读书所有，使用需遵守其服务条款。
