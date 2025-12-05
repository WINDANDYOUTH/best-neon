# 🚀 部署到 Vercel 完整指南

## ⚠️ 重要提醒

**永远不要将 `.env.local` 推送到 GitHub！**
- 它包含敏感的 API 密钥
- 已经在 `.gitignore` 中被排除
- 环境变量应该在 Vercel 后台配置

---

## 📋 部署步骤

### 步骤 1: 推送代码到 GitHub

```bash
# 确保你在项目根目录
cd c:\best-neon

# 查看当前状态
git status

# 添加所有更改（.env.local 会被自动忽略）
git add .

# 提交更改
git commit -m "Add Shopify setup documentation"

# 推送到 GitHub
git push origin main
```

### 步骤 2: 在 Vercel 中配置环境变量

#### 方法 A: 通过 Vercel Dashboard（推荐）

1. **登录 Vercel**
   - 访问: https://vercel.com
   - 登录你的账号

2. **选择项目**
   - 如果还没有导入项目，点击 "Add New" → "Project"
   - 从 GitHub 导入你的仓库

3. **配置环境变量**
   - 在项目页面，点击 **Settings** 标签
   - 在左侧菜单选择 **Environment Variables**
   - 添加以下变量：

   | 变量名 | 值 | 环境 |
   |--------|-----|------|
   | `COMPANY_NAME` | 你的公司名称 | Production, Preview, Development |
   | `SITE_NAME` | 你的网站名称 | Production, Preview, Development |
   | `SHOPIFY_STORE_DOMAIN` | your-store.myshopify.com | Production, Preview, Development |
   | `SHOPIFY_STOREFRONT_ACCESS_TOKEN` | 你的 Storefront API 令牌 | Production, Preview, Development |
   | `SHOPIFY_REVALIDATION_SECRET` | 任意随机字符串 | Production, Preview, Development |

   **注意**: 
   - 每个变量都要勾选所有三个环境（Production, Preview, Development）
   - `SHOPIFY_STORE_DOMAIN` 不要包含 `https://` 或方括号 `[]`

4. **重新部署**
   - 添加环境变量后，点击 **Deployments** 标签
   - 找到最新的部署，点击右侧的三个点 `...`
   - 选择 **Redeploy**
   - 或者，直接推送新的提交到 GitHub 会自动触发部署

#### 方法 B: 使用 Vercel CLI

如果你想使用命令行部署：

```bash
# 安装 Vercel CLI（全局安装）
npm install -g vercel

# 登录 Vercel
vercel login

# 部署到生产环境
vercel --prod

# CLI 会提示你输入环境变量，或者你可以在 vercel.json 中配置
```

### 步骤 3: 验证部署

1. **检查构建日志**
   - 在 Vercel Dashboard 中查看部署日志
   - 确保没有环境变量相关的错误

2. **访问你的网站**
   - Vercel 会提供一个 URL（例如：`your-project.vercel.app`）
   - 打开浏览器访问，确保网站正常运行

3. **测试 Shopify 集成**
   - 检查产品是否正常显示
   - 测试购物车功能

---

## 🔧 常见问题

### Q: 部署后仍然报错 "prerender error"？
**A**: 检查 Vercel 环境变量是否正确配置：
- 所有 5 个环境变量都已添加
- `SHOPIFY_STORE_DOMAIN` 格式正确（不含 https:// 或括号）
- `SHOPIFY_STOREFRONT_ACCESS_TOKEN` 是有效的
- 重新部署以应用环境变量

### Q: 如何查看 Vercel 的环境变量？
**A**: 
1. 进入项目 Settings → Environment Variables
2. 你可以看到变量名，但值会被隐藏（安全考虑）
3. 如果需要修改，删除旧的并添加新的

### Q: 本地开发和 Vercel 部署使用不同的环境变量？
**A**: 
- **本地开发**: 使用 `.env.local` 文件
- **Vercel 部署**: 使用 Vercel Dashboard 中配置的环境变量
- 两者的变量名和值应该相同

### Q: 如何在 Preview 部署中测试？
**A**:
- 创建新分支并推送
- Vercel 会自动创建 Preview 部署
- Preview 部署也会使用你配置的环境变量

---

## 📝 推荐的工作流程

```bash
# 1. 本地开发
# 创建 .env.local 并填写 Shopify 凭据
npm run dev

# 2. 测试构建
npm run build

# 3. 提交代码（.env.local 会被自动忽略）
git add .
git commit -m "Your commit message"
git push origin main

# 4. Vercel 自动部署
# 在 Vercel Dashboard 中配置环境变量（只需要配置一次）
# 之后每次推送都会自动部署
```

---

## 🎯 快速检查清单

部署前确保：
- [ ] `.env.local` 在本地工作正常
- [ ] `npm run build` 本地构建成功
- [ ] 代码已推送到 GitHub
- [ ] Vercel 中已配置所有 5 个环境变量
- [ ] 环境变量应用到所有环境（Production, Preview, Development）
- [ ] 触发重新部署

---

## 🔗 相关链接

- [Vercel Environment Variables 文档](https://vercel.com/docs/concepts/projects/environment-variables)
- [Next.js 环境变量文档](https://nextjs.org/docs/basic-features/environment-variables)
- [Shopify Storefront API 文档](https://shopify.dev/docs/api/storefront)

---

**需要帮助？** 如果在部署过程中遇到问题，请提供：
1. Vercel 构建日志的错误信息
2. 你已经配置的环境变量列表（不要包含实际的值）
3. 具体的错误截图
