# Git 速查卡（啊蹦专用）

## 我的环境
| 项目 | 值 |
|---|---|
| Git 版本 | 2.56.1.windows.1 |
| 安装位置 | `D:\Git`（不在 C 盘） |
| 桌面图标 | `Git Bash.lnk`（双击打开命令行） |
| 练习仓库 | `F:\2026-11-19-00-24-58\git-practice` |
| 身份 | 嘣伏妖 <2140106870@qq.com> |
| SSH 密钥 | `C:\Users\Administrator\.ssh\id_ed25519`（已生成） |

## 日常五条（覆盖 90% 场景）
```bash
git status                       # 我现在处于什么状态
git add -A                       # 把改动放进暂存区
git commit -m "说明改了什么"      # 打一个快照
git log --oneline                # 看快照链
git push                         # 推到 GitHub（远端）
```

## 撤销三招（按危险程度递增）
```bash
# 1. 只改错了工作区文件，还没提交 —— 丢弃文件改动
git restore 文件名

# 2. 已经提交但还没 push —— 把当前分支退一格，改动内容也可以保留
git reset --soft HEAD~1     # 退一格，改动留在暂存区（安全）
git reset --hard HEAD~1     # 退一格，改动全部丢弃（危险）

# 3. 已经 push 出去了 —— 用反向快照抵消，历史不动
git revert <那个提交的sha>
```

## 救命命令
```bash
git reflog                  # 快照链的完整地图：被 reset 掉的提交也能找回
git reset --hard <sha>      # 从上一步找到 sha，直接回到那个状态
```

## 三条铁律
1. **`reset --hard` 只对"还没 push"的提交用**，推上去的历史别改写。
2. **`.env`、密钥、`node_modules/` 先写进 `.gitignore`**，公开仓库里的密钥几分钟就会被爬走。
3. **commit 说明写"为什么改"，不要写"update"**。

## 当前网络现实（01:16 实测）
| 目标 | 状态 |
|---|---|
| `github.com` 网页 | 正常（200） |
| `git ls-remote https://github.com/git/git` | 成功 |
| `ssh git@github.com`（22 端口） | 通，只差公钥没登记到账号 |

结论：**网络没问题**。早先"打不开"的判断是假阴性（命令行带了代理环境变量导致超时），已更正。

