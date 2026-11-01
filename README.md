# 译学 · AI 翻译与语法学习

一个单文件网页，用大模型做中日英三语的**自然翻译**和**语法分析**，支持 DeepSeek、OpenAI、Gemini、Claude 以及任何 OpenAI 兼容接口，顶栏一键切换。手机、电脑打开同一个网址即可使用，可添加到主屏幕当 App 用。

## 功能

- 多接口：DeepSeek / OpenAI（Responses API）/ Gemini / Claude / 自定义 OpenAI 兼容接口，每个接口分别保存 Key 和模型，顶栏随时切换；模型列表可从接口实时拉取，也可手动输入
- 思考强度可调（关 / 低 / 高），模型不支持的档位自动回退
- 自动识别输入语言（含假名判日语，含繁体或日本新字体判日语，其余汉字判中文，字母判英语），可手动指定
- 中文输入 → 日语口语（タメ口）/ 日语敬语（です・ます 为主）/ 美式英语口语
- 日语输入 → 自然中文 / 美式英语口语
- 英语输入 → 自然中文 / 日语口语
- 三个译文框并行流式输出，停止输入约 1 秒后自动翻译
- 点击任意译文或「分析」按钮：展开词汇读音、语法句型、替换表达、注意点（面向 N1 学习者，英语部分更简洁）
- 较短的日语表达自动进入「语法深究」：含义、接续、5 个例句、近似表达对比、口语实战
- 振假名开关（标注日语译文中所有汉字读音）
- 朗读（浏览器自带语音）、一键复制
- 历史记录与收藏，本地保存；可选通过私密 GitHub Gist 在多设备间同步
- 深色模式、PWA 离线外壳

## 使用

1. 打开网页，点右上角 ⚙ 设置，选择一个接口并填入它的 API Key，点「拉取列表」选模型，点「测试连接」确认后保存。可以把几家都填上，之后在顶栏的模型按钮里切换。
   - DeepSeek：<https://platform.deepseek.com/api_keys>
   - OpenAI：<https://platform.openai.com/api-keys>
   - Gemini：<https://aistudio.google.com/apikey>
   - Claude：<https://console.anthropic.com/settings/keys>

   Key 只保存在当前设备的浏览器 localStorage 里，网页直接请求各家官方接口，不经过任何中间服务器。
2. 输入文字即可。⌘/Ctrl + Enter 立即翻译。
3. 多设备同步（可选）：在 <https://github.com/settings/tokens/new?scopes=gist&description=yixue-sync> 生成一个只勾选 **gist** 的 Token，填到设置里，每台设备填同一个。

## 部署到 GitHub Pages

```bash
git init -b main
git add .
git commit -m "译学 v1.0"
git remote add origin https://github.com/<你的用户名>/yixue.git
git push -u origin main
```

然后在仓库 Settings → Pages → Build and deployment 选 **Deploy from a branch**，Branch 选 `main` / `(root)`，保存。
一两分钟后访问 `https://<你的用户名>.github.io/yixue/`。

## 本地开发

`dev/mock-server.js` 提供静态文件服务，并模拟四种接口的流式响应（API Key 一律填 `test`；API 地址：DeepSeek/自定义 `http://localhost:8787`，OpenAI 与 Claude `http://localhost:8787/v1`，Gemini `http://localhost:8787/v1beta`），不消耗真实额度：

```bash
node dev/mock-server.js
```

## 文件

- `index.html` 全部界面与逻辑
- `manifest.json`、`sw.js`、`icon-*.png` PWA 相关
