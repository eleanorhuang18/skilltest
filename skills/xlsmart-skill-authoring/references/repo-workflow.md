# 仓库操作手册

## 工作副本

固定一份本地克隆，不要每次重新 clone：

```text
/root/.openclaw/workspace/repos/skilltest
```

远程：`https://github.com/eleanorhuang18/skilltest`，主分支 `main`。

## 首次准备（新环境才需要）

```bash
git clone https://github.com/eleanorhuang18/skilltest /root/.openclaw/workspace/repos/skilltest
cd /root/.openclaw/workspace/repos/skilltest
git config credential.helper '!gh auth git-credential'
```

`gh` 已登录时，这行让 git 复用它的凭据；只作用于本仓库，不改全局配置。若 `gh auth status` 显示未登录，先让用户走 Control UI 的 Connect GitHub，不要自己拼 token。

## 每次提交

```bash
cd /root/.openclaw/workspace/repos/skilltest
git pull --rebase --autostash origin main      # 先同步，避免分叉
git add -A
git status --short                              # 确认只包含本次改动
git commit -m "feat(skill): add <name>"
git push origin main
```

## 推送后必须验证

```bash
gh api repos/eleanorhuang18/skilltest/commits/main \
  --jq '.sha[0:8]+"  "+.commit.message+"  by "+.commit.author.name'
gh api repos/eleanorhuang18/skilltest/contents/skills --jq '.[].name'
```

两条都要看到本次 commit 和目录。看不到就等于没成功，不要向用户报"已完成"。

## 提交信息规范

| 场景 | 格式 |
| --- | --- |
| 新增 skill | `feat(skill): add <name>` |
| 修改 skill | `fix(skill): <name> — <一句话>` 或 `feat(skill): <name> — <一句话>` |
| 仅文档/索引 | `docs: <改动>` |
| 仓库结构 | `chore: <改动>` |

一条 commit 只做一件事；同时新增和修改两个 skill 就分两次提交。

## 索引维护

根目录 `README.md` 的索引表按名称排序，一行一个 skill：

```markdown
| [<name>](skills/<name>/SKILL.md) | <一句话用途> | 可用 |
```

状态用：`草稿` / `可用` / `已废弃`。

## 推送失败怎么办

1. `git pull --rebase` 后重推一次。
2. 仍失败就停下，把原始报错贴给用户，说明是权限、冲突还是网络。
3. 不要反复重试、不要 force push、不要改写远端历史。
