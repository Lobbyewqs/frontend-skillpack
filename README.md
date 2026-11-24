# frontend skillpack

一个用于前端开发与 UI 设计的 Codex 技能。用 `$frontend-skillpack` 处理页面设计、组件实现、界面审查、交互式 3D 或程序化视频。入口会按任务选择专题，跨框架的问题也可以在同一次调用中处理。

## 安装

```sh
npx skills add Lobbyewqs/frontend-skillpack --skill frontend-skillpack -a codex -g
```

也可以[下载独立技能包](dist/frontend-skillpack.zip)，将其中的 `frontend-skillpack` 文件夹放入 Codex 的用户技能目录。技能使用独立名称，可与原有专题技能共存。正常安装只需这个包。

## 包含的专题

| 用途 | 具体场景 |
|---|---|
| 视觉设计与网页审查 | 页面层级与排版、键盘交互、表单和可访问性 |
| 响应式 CSS 与 Tailwind v4 | Grid、Flexbox、容器查询、主题变量和组件变体 |
| React 与 Next.js | 请求瀑布、包体积、重渲染、组合组件与状态归属 |
| Vue 3 与 Nuxt 4 | 响应性、组件通信、服务端取数与水合 |
| Three.js 与 Remotion | 原生 3D 场景、材质与动画，按帧构图、字幕和视频导出 |

例如，`用 $frontend-skillpack 排查这个 Nuxt 商品页为什么首次打开会发出两次请求。` 也可以指定交付物，如 `用 $frontend-skillpack 把这个 React 标题动画做成 3 秒的 Remotion 片头。`

九个专题随包附带参考资料。Remotion 专题含本地指南和示例，扩展主题链接到固定版本的官方文档。各项目的出处、版本和随附许可见[来源记录](skills/frontend-skillpack/notices/sources.md)。
