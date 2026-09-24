# Cloudflare → GitHub Pages 静态页面测试

这是一个无构建步骤、无外部依赖的单页测试站。`index.html` 是网站内容；`CNAME` 指定截图中的自定义域名 `paistar.eu.cc`。

## 部署

1. 在 GitHub 账号 `paistar250` 下新建一个公开仓库，例如 `pages-test`，先将本目录的 `index.html` 上传到仓库根目录的 `main` 分支。
2. 打开该仓库的 **Settings → Pages**，在 **Build and deployment** 中选择 **Deploy from a branch**，分支选 `main`，目录选 `/ (root)`，保存。先访问 GitHub 给出的 `https://paistar250.github.io/pages-test/`，确认页面发布成功。如果仓库名称不同，URL 中的路径也要相应变化。
3. 将本目录的 `CNAME` 也上传到仓库根目录，并在 **仓库的 Settings → Pages → Custom domain** 填写 `paistar.eu.cc` 后保存。确认 GitHub 显示的域名和 `CNAME` 一致。截图中的 GitHub 个人资料设置页不是仓库的 Pages 设置页。
4. 在 Cloudflare 的 `paistar.eu.cc` DNS 页面，为根域名 `@` 添加以下四条 `A` 记录（四条的“名称”都填 `@`）：

   | 类型 | 名称 | IPv4 地址 |
   | --- | --- | --- |
   | A | @ | 185.199.108.153 |
   | A | @ | 185.199.109.153 |
   | A | @ | 185.199.110.153 |
   | A | @ | 185.199.111.153 |

   初次验证时可将这四条记录设为 **DNS only（灰云）**，等待 GitHub 的 DNS 检查和 HTTPS 证书完成。之后如需测试 Cloudflare 代理，再切换为 **Proxied（橙云）**。请不要把域名指向 `pages.dev`，那是 Cloudflare Pages 的另一套服务。
5. 访问 `https://paistar.eu.cc/`，检查是否看到 `test-v1`。点击“再次检测”查看 HTTP 状态和可读取的 Cloudflare 响应头。在浏览器开发者工具的 Network 面板也可查看响应头。

DNS 与证书生效可能需要一段时间。若 GitHub Pages 自带地址可以访问，而自定义域名不行，先检查 Cloudflare 的 DNS 记录、GitHub Pages 的 Custom domain 状态和 HTTPS 设置。

## 本地预览

直接用浏览器打开 `index.html` 即可预览外观；“再次检测”需要通过 HTTP(S) 访问才有意义。也可以在此目录运行 `python -m http.server 8000`，然后打开 `http://localhost:8000/`。
