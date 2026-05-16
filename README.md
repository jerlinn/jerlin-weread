# jerlin-weread

基于微信读书官方 Skill 的重构版本。

核心改动：API spec 下沉到 CLI 按需获取，领域知识从 few-shot 示例提炼为决策规则和语义陷阱，移除 Agent 可自行推断的常识描述。Agent 每次请求只加载路由表 + 对应领域 reference，不再全量读入 API 文档。

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
jerlin-weread-skill/
├── SKILL.md              意图路由 + 通用规则
├── scripts/weread.sh     API CLI, 17 个子命令 (weread.sh -h)
└── references/           语义陷阱、计算规则、工作流
```

## 主要优化

官方版本将 API 规格和领域知识混合在多个 markdown 中。本版本做关注点分离：

- API 调用机制收编为 CLI 脚本，Agent 通过 `-h` 按需查阅参数和回包字段
- 领域知识从 few-shot 重构为推理规则，编码决策边界和语义陷阱而非罗列正确/错误示例
- 移除 Agent 可推断的流程描述和常识说明，只保留不可推断的信号

## Credits

基于微信读书官方团队的 [WeRead Skill](https://weread.qq.com/r/weread-skills) 优化。API 接口和数据归微信读书所有，使用需遵守其服务条款。本项目仅重构 Skill 的文档结构和 Agent 交互方式。