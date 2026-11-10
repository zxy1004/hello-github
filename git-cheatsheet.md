# Git 速查表

我的第一个仓库备忘。配合 `zxy1004` 账号使用。

---

## 一、先记住这一张图

文件在 Git 里要经过四个位置：

```
工作区  →  暂存区  →  本地仓库  →  远程仓库
(改文件)   (git add)   (git commit)   (git push)
```

| 位置 | 是什么 | 对应命令 |
|---|---|---|
| 工作区 | 你看到的那些文件 | 编辑、保存 |
| 暂存区 | 待提交清单，挑选这次要提交哪些改动 | `git add` |
| 本地仓库 | 存档点，每提交一次生成一个版本号 | `git commit` |
| 远程仓库 | GitHub 上的副本 | `git push` |

分四步而不是"一键上传"，是为了能**只提交你想提交的那部分改动**。

---

## 二、首次配置（只做一次，已完成）

```powershell
git config --global user.name "zxy1004"
git config --global user.email "zxy1004@users.noreply.github.com"
```

`noreply` 邮箱是 GitHub 提供的匿名地址，能正常算作你的提交，但不会把真实邮箱暴露在公开的提交历史里。

查看当前配置：

```powershell
git config --global --list
```

---

## 三、日常操作：四行命令

```powershell
git status                      # 看有哪些改动
git add -A                      # 全部放进暂存区
git commit -m "说明改了什么"     # 存档
git push                        # 上传
```

### 每步成功后屏幕上长什么样

```
PS> git status
On branch main
Changes not staged for commit:
	modified:   hello.txt

PS> git add -A
（没输出就是成功）

PS> git commit -m "Update hello.txt"
[main 7a1c2f9] Update hello.txt
 1 file changed, 2 insertions(+), 1 deletion(-)

PS> git push
To https://github.com/zxy1004/hello-github.git
   36ebca7..7a1c2f9  main -> main
```

**判断推送成功看最后一行**：`旧版本..新版本 main -> main`。

---

## 四、建一个新仓库

### 网页端

1. 右上角 `+` → New repository（或直接访问 `https://github.com/new`）
2. Repository name 填名字
3. 选 **Public**
4. **勾上 Add a README file**
5. 点 Create repository

> 必须勾 README：空仓库没有默认分支，本地克隆会因为"当前分支不存在"报错。

### 本地端

```powershell
cd C:\Users\HUAWEI\Documents
git clone https://github.com/zxy1004/仓库名.git
cd 仓库名
```

克隆 = 把远程仓库连历史一起完整复制到本地。

### 更省事的替代：网页直接传文件

只想放文件（例如单文件 HTML 课件）时，不用命令行：

仓库页面 → **Add file** → **Upload files** → 拖进去 → **Commit changes**。

适合一次性放几个文件；反复修改的项目用命令行更快。

---

## 五、提交信息怎么写

惯例：**祈使句开头、首字母大写、不加句号**，读起来像在下指令。

| 好 | 差 |
|---|---|
| `Add 幼儿园晨检流程图` | `更新` |
| `Fix 表格导出乱码` | `改了点东西` |
| `Update README 安装步骤` | `123` |

原因：`git log` 是给三个月后的自己看的。写"更新"等于没写。

常用动词：`Add`（新增）、`Update`（修改）、`Fix`（修复）、`Remove`（删除）、`Refactor`（重构）。

---

## 六、命令速查

| 目的 | 命令 |
|---|---|
| 看当前状态 | `git status` |
| 看改动内容 | `git diff` |
| 看提交历史 | `git log --oneline` |
| 把某个文件加入暂存 | `git add 文件名` |
| 撤销暂存（保留改动） | `git restore --staged 文件名` |
| 丢弃未提交的改动 | `git restore 文件名` |
| 拉取远程最新 | `git pull` |
| 查看远程地址 | `git remote -v` |
| 查看当前分支 | `git branch` |

---

## 七、常见报错

| 报错 | 意思 | 怎么办 |
|---|---|---|
| `not a git repository` | 不在仓库目录里 | `cd` 到正确的文件夹 |
| `Authentication failed` | 授权失效 | 在"凭据管理器"里删掉 `git:https://github.com` 后重新授权 |
| `Updates were rejected` | 远程有你本地没有的提交 | 先 `git pull`，再 `git push` |
| `nothing to commit` | 没有改动，或忘了 `git add` | 先 `git add -A` |
| `fatal: pathspec ... did not match` | 文件名写错或不在当前目录 | 用 `Get-ChildItem` 看真实文件名 |

---

## 八、三条该养成的习惯

1. **动手前先 `git status`**。它会告诉你现在在哪、有没有未提交的东西。
2. **`git push` 之前先 `git pull`**。只要在网页上改过东西（改 README 也算），本地就会落后。
3. **永远不要提交密码、密钥、token**。推上去之后即使删掉，历史里也永久保留。这类文件写进 `.gitignore`。

---

## 九、排障：网站打不开时先分清两种情况

| 现象 | 判断 | 处理 |
|---|---|---|
| DNS 返回**奇怪的 IP**（不是该网站真实地址） | 域名被污染 | 换 DNS 或换网络 |
| DNS **正常**但连不上 | 链路中断 | 只能等或换网络（手机热点） |

诊断命令：

```powershell
Resolve-DnsName github.com -Type A
Test-NetConnection github.com -Port 443
```

前者看 IP 对不对，后者看端口通不通。

---

## 十、本仓库信息

- 账号：`zxy1004`
- 仓库：`https://github.com/zxy1004/hello-github`
- 本地路径：`C:\Users\HUAWEI\Documents\hello-github`
- 默认分支：`main`

---

_最后更新：2026-11-10_
