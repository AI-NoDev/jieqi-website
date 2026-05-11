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

## 当前部署（GitHub Pages · AI-NoDev 组织）

- 仓库：https://github.com/AI-NoDev/jieqi-website
- 在线 URL：**https://ai-nodev.github.io/jieqi-website/**

**ASC 填写**：
- Support URL: `https://ai-nodev.github.io/jieqi-website/`
- Privacy Policy URL: `https://ai-nodev.github.io/jieqi-website/privacy.html`
- Marketing URL: `https://ai-nodev.github.io/jieqi-website/`（可选）

## 重新部署（本目录 → AI-NoDev/jieqi-website）

```sh
# 单文件 PUT（绕过 HTTPS push 在中国不稳定的问题）
cd apps/jieqi/website
for f in README.md favicon.png icon.png index.html privacy.html terms.html; do
  CONTENT=$(base64 -i "$f")
  SHA=$(gh api repos/AI-NoDev/jieqi-website/contents/"$f" --jq .sha 2>/dev/null)
  gh api repos/AI-NoDev/jieqi-website/contents/"$f" -X PUT \
    -f message="Update $f" \
    -f content="$CONTENT" \
    ${SHA:+-f sha="$SHA"}
done
```

## 测试本地预览

```sh
cd apps/jieqi/website
python3 -m http.server 8000
# 浏览器打开 http://localhost:8000
```

## 联系邮箱

站点和 app 内所有联系方式统一为 **`qiyuzhou666@gmail.com`**。

如需更换，全局替换并重新部署：

```sh
OLD="qiyuzhou666@gmail.com"
NEW="your-new@email.com"
find apps/jieqi -type f \( -name "*.html" -o -name "*.md" -o -name "*.tsx" \) \
  -exec sed -i '' "s/$OLD/$NEW/g" {} \;
```

## 后续

这些 URL 和邮箱已经写进 `apps/jieqi/store/ASC_CHECKLIST.md` 和 6 份 `aso/*.md`，提交 ASC 时直接复制粘贴即可。
