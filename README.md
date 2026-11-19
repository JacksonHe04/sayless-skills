# sayless-skills

我公开的 Agent Skills 集合。遵循 [Agent Skills](https://agentskills.io) 开放标准：一个技能 = 一个目录 + 一份 `SKILL.md`，没有构建步骤，也不发包到 npm。

Sayless's public agent skills, published in the [Agent Skills](https://agentskills.io) open format. A skill is a directory with a `SKILL.md` — no build step, no npm package.

## 安装 / Install

```bash
npx skills add JacksonHe04/sayless-skills                    # 装到当前项目
npx skills add JacksonHe04/sayless-skills --list             # 只看有什么，不装
npx skills add JacksonHe04/sayless-skills --skill <name> -g  # 全局装某一个
gh skill install JacksonHe04/sayless-skills <name>           # GitHub CLI 也行
```

技能会被软链进各客户端的技能目录（`~/.claude/skills/`、`~/.agents/skills/` …），一处更新全部生效。

## 目录 / Layout

```
SKILL.md              # 本仓库自身的技能：公开技能的索引 + 发布流程 + 脱敏清单
README.md             # 你在看的这份
LICENSE
skills/               # 公开技能，每个一个子目录
```

## 加一个技能 / Add a skill

`skills/<name>/SKILL.md`，`name` 必须与目录同名（小写、数字、连字符）。完整规范、发布步骤和**公开前脱敏清单**都在 [SKILL.md](SKILL.md) 里 —— 那个文件是给 agent 读的，也是这个仓库唯一需要维护的说明。

## License

MIT
