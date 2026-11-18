# skilltest

OpenClaw 可复用 skill 仓库。每个 skill 一个目录，独立、可单独安装。

## 目录结构

```
skills/
└── <skill-name>/
    ├── SKILL.md        # 主文件：做什么、何时触发、怎么做
    ├── references/     # 长文档、查表资料（可选）
    └── scripts/        # 可执行脚本（可选）
```

## 约定

- 目录名用 kebab-case，和 skill 名一致。
- `SKILL.md` 保持精简（< 10k 字符），长内容拆到 `references/`。
- 描述（description）开头写触发场景，让人一眼知道什么时候该用它。
- 每个 skill 提交时同步更新下方索引。

## 索引

| Skill | 用途 | 状态 |
| --- | --- | --- |
| _（待添加）_ | | |
