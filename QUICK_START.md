# Decap CMS 快速开始指南

## 🎯 接下来需要做的 3 个步骤

### 步骤 1：创建 GitHub OAuth App（5 分钟）

**访问地址：** https://github.com/settings/developers

**操作步骤：**

1. 点击左侧菜单的 **"OAuth Apps"**
2. 点击右上角的 **"New OAuth App"** 按钮
3. 填写以下信息：

   ```
   Application name: Alili Tech CMS
   Homepage URL: https://time-friend.com
   Authorization callback URL: https://time-friend.com/admin/
   ```

   **关于 Authorization callback URL 的说明：**
   - 这是 GitHub OAuth 授权完成后，GitHub 重定向回你网站的地址
   - 必须与 Decap CMS 的入口地址完全一致
   - 你的 CMS 入口在 `static/admin/index.html`，所以访问路径是 `/admin/`
   - 完整 URL 就是：`https://time-friend.com/admin/`
   - ⚠️ 注意：末尾的斜杠 `/` 很重要，必须包含

4. 点击 **"Register application"**
5. **重要**：复制页面上的 **Client ID**（一串类似 `Iv1.xxxxxxxxxxxxx` 的字符串）
   - ⚠️ 注意：**不需要** Client Secret（PKCE 流程不需要）

### 步骤 2：更新配置文件（1 分钟）

编辑 `static/admin/config.yml` 文件，在第 7 行添加 `client_id`：

```yaml
backend:
  name: github
  repo: 0x1428571429/alili.tech
  branch: master
  base_url: https://time-friend.com
  auth_type: pkce
  client_id: 你的-Client-ID-粘贴在这里  # 👈 在这里粘贴步骤 1 获得的 Client ID
```

### 步骤 3：提交并部署（2 分钟）

```bash
# 提交更改
git add static/admin/config.yml
git commit -m "Add GitHub OAuth client_id for Decap CMS"
git push origin master
```

GitHub Actions 会自动部署，等待 2-3 分钟后访问：**https://time-friend.com/admin/**

---

## ✅ 验证是否成功

1. 访问：https://time-friend.com/admin/
2. 应该看到 "Login with GitHub" 按钮
3. 点击登录，授权后即可看到 CMS 界面

---

## 📍 关键链接汇总

- **创建 OAuth App**: https://github.com/settings/developers
- **查看已创建的 OAuth Apps**: https://github.com/settings/developers/oauth_apps
- **CMS 访问地址**: https://time-friend.com/admin/
- **GitHub 仓库**: https://github.com/0x1428571429/alili.tech

---

## ❓ 常见问题

### Q: 找不到 "OAuth Apps" 菜单？
A: 确保你登录了 GitHub，并且访问的是：https://github.com/settings/developers

### Q: Client ID 在哪里？
A: 创建 OAuth App 后，在应用详情页面的顶部就能看到 "Client ID"

### Q: 需要填写 Client Secret 吗？
A: **不需要**，PKCE 流程只需要 Client ID

### Q: 回调 URL 填错了怎么办？
A: 可以编辑已创建的 OAuth App，修改 "Authorization callback URL"

### Q: 本地开发怎么测试？
A: 可以创建第二个 OAuth App，回调 URL 设置为：`http://localhost:1313/admin/`

---

## 🚀 开始使用

配置完成后，你就可以：
- ✅ 在线创建和编辑文章
- ✅ 上传图片（自动保存到 `static/images/uploads/`）
- ✅ 批量导入 AI 生成的内容
- ✅ 所有更改自动提交到 GitHub 并触发部署

