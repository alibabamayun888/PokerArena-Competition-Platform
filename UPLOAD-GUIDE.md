# PokerArena 文件上传与发布指南

## 需要上传或覆盖的文件

将压缩包中的内容合并到仓库根目录：

```text
README.md
README.zh-TW.md
README.en.md
GITHUB-METADATA.md
SECURITY.md
PRIVACY.md
RESPONSIBLE-USE.md
docs/
```

其中 `docs/Assets/Screenshots/` 包含线上仓库现有的 4 张截图。覆盖前可以核对文件大小；本压缩包不会修改 Unity 工程或 `Clinet/`、`Doc/`、`UnityFramework/` 等代码目录。

## 设置 About 与 Topics

1. 打开仓库首页右侧 **About** 区域。
2. 点击设置图标。
3. 将 `GITHUB-METADATA.md` 中的 About 填入 Description。
4. 将 Website 设置为 GitHub Pages 地址。
5. 添加列出的 20 个 Topics 并保存。

## 启用 GitHub Pages

1. 打开仓库 **Settings → Pages**。
2. Source 选择 **Deploy from a branch**。
3. Branch 选择 `main`，目录选择 `/docs`。
4. 保存并等待 Pages 部署完成。
5. 打开 `https://alibabamayun888.github.io/PokerArena-Competition-Platform/`，确认 4 张截图、繁体页和英文页均能显示。

## 提交搜索引擎

1. 在 Google Search Console 添加 Pages 地址并验证所有权。
2. 提交 `https://alibabamayun888.github.io/PokerArena-Competition-Platform/sitemap.xml`。
3. 在 Bing Webmaster Tools 添加同一网站，可从 Google Search Console 导入。
4. 请求抓取首页、`/zh-TW/` 和 `/en/`。
5. 每次重要更新后同步更新 README、页面正文和截图说明。

## 发布前必须处理

- 选择真实适用的开源或商业许可证并添加根目录 `LICENSE`。在此之前不要在 About 或 README 宣称 MIT。
- 核对 Unity、C++、Java、MySQL、Redis 等实际版本，删除不存在的技术描述。
- 若服务器和后台代码将公开，补充可执行的构建与部署文档。
- 补充 `CONTRIBUTING.md`、变更日志、版本标签和 Release 说明。
- 清除仓库中的密钥、证书、服务器地址、真实用户数据和人脸认证材料。
- 对产品截图中可能涉及的第三方赛事名称、图片和商标确认使用权。

## 建议的后续优化

- 将当前目录名 `Clinet/` 更正为 `Client/`，但必须同时更新 Unity 引用并单独测试。
- 为 C++ 服务器、Java 后台和协议分别建立清晰目录，而不是把文件散落在根目录。
- 添加可复现的性能测试报告，包含硬件、版本、并发模型、持续时间和测试脚本。
- 在 GitHub Releases 发布有版本号的构建说明，不要把“下载”关键词堆入 README。
- 持续修复 GitHub Issues，并通过真实更新积累外部链接和项目可信度。
