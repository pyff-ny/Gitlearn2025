# Gitlearn2025
Notes generated with the assistance of AI (ChatGPT)

下面是“从 0 开始，把本地一个文件夹推到 GitHub”的标准步骤（macOS/Windows 都通用；命令行以 bash/zsh 为例）。你照做即可，不需要任何前置仓库。

---

## 0) 先准备：在 GitHub 新建一个空仓库

1. 打开 GitHub → **New repository**
2. 只填：**Repository name**
3. 选 Public/Private
4. **不要勾选** README / .gitignore / License（保持空仓库，避免第一次 push 冲突）
5. 创建后，你会看到仓库地址（HTTPS/SSH 二选一）

---

## 1) 进入你的本地文件夹

```bash
cd /path/to/your-folder
```

确认你就在正确目录：

```bash
pwd
ls
```

---

## 2) 初始化 Git 仓库

```bash
git init
```

（可选但建议）设置默认分支为 main：

```bash
git branch -M main
```

---

## 3) 添加文件并首次提交

```bash
git add .
git commit -m "Initial commit"
```

如果提示需要设置用户名邮箱：

```bash
git config --global user.name "Your Name"
git config --global user.email "you@example.com"
```

然后重新执行 commit。

---

## 4) 绑定远端 GitHub 仓库（origin）

把下面的 URL 换成你仓库页面的地址：

### 用 HTTPS

```bash
git remote add origin https://github.com/<owner>/<repo>.git
```

### 或用 SSH

```bash
git remote add origin git@github.com:<owner>/<repo>.git
```

检查是否绑定成功：

```bash
git remote -v
```

---

## 5) 推送到 GitHub

```bash
git push -u origin main
```

`-u` 的作用：把本地 `main` 和远端 `origin/main` 设为“上游跟踪”，以后你只要 `git push` / `git pull` 即可。

---

## 6) 验收

回到 GitHub 仓库页面刷新：文件应已出现。

---

# 常见故障（你大概率会遇到其中一个）

## A) HTTPS 提示要密码/认证失败

GitHub 现在不支持用账户密码进行 git 推送；需要：

* 使用 **Personal Access Token (PAT)** 当“密码”
* 或改用 SSH（一次配置，长期省事）

（你如果走 HTTPS，我建议你直接改 SSH，后续更顺。）

## B) 远端已有 README 导致冲突（你第 0 步没保持空仓库）

典型报错：`rejected` / “fetch first”
处理方式（择一）：

1. 先拉再合并（最稳妥）：

```bash
git pull origin main --allow-unrelated-histories
# 解决冲突（如有）后
git push
```

2. 你确定要用本地覆盖远端（谨慎）：

```bash
git push -u origin main --force
```

---

# 最简“一屏命令版”（假设远端是空仓库）

```bash
cd /path/to/your-folder
git init
git branch -M main
git add .
git commit -m "Initial commit"
git remote add origin <your-repo-url>
git push -u origin main
```

---

### English summary

Create an empty GitHub repo, `cd` into your local folder, `git init`, (optionally `git branch -M main`), `git add .`, `git commit`, add remote `git remote add origin <url>`, then `git push -u origin main`. If HTTPS auth fails, use a PAT or switch to SSH; if remote isn’t empty, `git pull --allow-unrelated-histories` then push.
