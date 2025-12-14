# GitHub Personal Access Token 配置指南

## 方式 1：使用 macOS Keychain（推荐）

当你第一次推送代码时，Git 会提示输入凭证：
- **用户名**：你的 GitHub 用户名
- **密码**：你的 Personal Access Token（不是 GitHub 密码）

Token 会自动保存到 macOS Keychain，之后无需再次输入。

## 方式 2：在远程 URL 中包含 Token

如果你已经创建了 GitHub 仓库，可以这样设置远程地址：

```bash
git remote add origin https://YOUR_TOKEN@github.com/YOUR_USERNAME/YOUR_REPO.git
```

或者修改现有的远程地址：

```bash
git remote set-url origin https://YOUR_TOKEN@github.com/YOUR_USERNAME/YOUR_REPO.git
```

**注意**：这种方式会将 token 暴露在 `.git/config` 文件中，安全性较低。

## 方式 3：使用 Git Credential Helper（手动配置）

清除已保存的凭证（如果需要）：
```bash
git credential-osxkeychain erase
host=github.com
protocol=https
```

然后下次推送时会提示输入新的凭证。

## 完整的上传流程

1. **添加文件到暂存区**：
   ```bash
   git add .
   ```

2. **提交更改**：
   ```bash
   git commit -m "Initial commit"
   ```

3. **添加远程仓库**（如果还没有）：
   ```bash
   git remote add origin https://github.com/YOUR_USERNAME/YOUR_REPO.git
   ```

4. **推送代码**：
   ```bash
   git push -u origin main
   ```
   或
   ```bash
   git push -u origin master
   ```
   （根据你的默认分支名称）

   此时会提示输入用户名和密码，输入你的 GitHub 用户名和 Personal Access Token。

## 验证配置

检查远程仓库配置：
```bash
git remote -v
```

## 注意事项

- Personal Access Token 需要具有 `repo` 权限才能推送代码
- Token 一旦生成，只会显示一次，请妥善保管
- 如果 token 泄露，应立即在 GitHub 设置中撤销并重新生成

