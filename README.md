# Jieqi Almanac · 静态官网

ASC 提交需要 **Support URL**（必填）和 **Privacy Policy URL**（强烈建议）。这个目录下有完整一套静态站点：

```
website/
├── index.html      # 主页 + FAQ + Contact (Support URL 指向这里)
├── privacy.html    # 完整 6 语言隐私政策 (Privacy Policy URL 指向这里)
├── terms.html      # 6 语言使用条款
├── icon.png        # logo（复用 app icon）
└── favicon.png     # 浏览器 favicon
```

## 部署 — 三种最简单方案

### 方案 A：Cloudflare Pages（推荐，全球 CDN，免费）

1. 注册 https://pages.cloudflare.com（免费）
2. **Direct Upload** → 拖拽 `website/` 整个文件夹
3. 选 project name：`jieqi-almanac`
4. 部署后获得 URL：`https://jieqi-almanac.pages.dev`
5. （可选）绑定自定义域名 `jieqi.app`

**ASC 填写**：
- Support URL: `https://jieqi-almanac.pages.dev/`
- Privacy Policy URL: `https://jieqi-almanac.pages.dev/privacy.html`
- Marketing URL: `https://jieqi-almanac.pages.dev/`（可选）

### 方案 B：GitHub Pages

1. 在 GitHub 创建一个 public repo（如 `jieqi-website`）
2. 把 `website/*` 推到该 repo
3. 设置 → Pages → Source: `main` branch / `/ (root)`
4. 获得 URL：`https://<username>.github.io/jieqi-website/`

### 方案 C：Netlify Drop（最快，1 分钟）

1. 打开 https://app.netlify.com/drop
2. 拖拽 `website/` 文件夹
3. 立刻获得 URL：`https://random-name-123.netlify.app`
4. （可选）登录后改 site name

## 测试本地预览

```sh
cd apps/jieqi/website
python3 -m http.server 8000
# 浏览器打开 http://localhost:8000
```

## 部署后必须更新

部署完成后，**回到代码里把以下占位邮箱替换成真实的**：

- `apps/jieqi/website/index.html`：搜索 `support@jieqi.app`
- `apps/jieqi/website/privacy.html`：搜索 `privacy@jieqi.app`
- `apps/jieqi/website/terms.html`：搜索 `support@jieqi.app`
- `apps/jieqi/legal/privacy-policy.md`：同上
- `apps/jieqi/app/privacy.tsx`：app 内嵌隐私政策也要改

可以用 sed 批量替换：

```sh
# 把所有 jieqi.app 邮箱替换成你真实的邮箱
find apps/jieqi -type f \( -name "*.html" -o -name "*.md" -o -name "*.tsx" \) \
  -exec sed -i '' 's/support@jieqi.app/your-real@email.com/g' {} \;
find apps/jieqi -type f \( -name "*.html" -o -name "*.md" -o -name "*.tsx" \) \
  -exec sed -i '' 's/privacy@jieqi.app/your-real@email.com/g' {} \;
```

## 后续

部署完成后，把这两个 URL 填到：

1. **App Store Connect** → App Information
   - Privacy Policy URL: `<your-url>/privacy.html`
2. **App Store Connect** → 每个本地化版本
   - Support URL: `<your-url>/`
3. **Apple Developer** → App Privacy Policy（必填）
