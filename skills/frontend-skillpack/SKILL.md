---
name: frontend-skillpack
description: 设计、实现和审查 Web 前端。用于页面视觉与可访问性、响应式 CSS 和 Tailwind、React / Next.js 性能与组件组合、Vue / Nuxt、原生 Three.js 场景，以及用 Remotion 制作或渲染程序化视频。
---

# frontend skillpack

从用户希望改变的页面、组件或画面出发。已有项目先看对应代码、依赖版本和设计约定，再从下表选择资料。表中的链接相对于本文件，专题内的规则、示例和素材相对于引用它们的文档。

| 遇到的任务 | 阅读哪份资料 | 应用重点 |
|---|---|---|
| 新页面、视觉改版、品牌风格 | [界面设计](references/design/guide.md) | 从内容、受众和主要操作出发确定层级、字体、配色与图像方向，沿用已有的品牌约束。 |
| 审查页面体验、可访问性或交互细节 | [网页审查](references/web-review/guide.md) | 对照内置规则检查键盘焦点、表单标签、交互状态等，给出问题位置和修复办法。 |
| 小屏溢出、卡片网格、可复用的自适应组件 | [响应式布局](references/layout/guide.md) | 页面断点看内容何时放不下，组件断点看容器宽度。按排列关系选 Grid 或 Flexbox。 |
| Tailwind 主题、设计变量和组件变体 | [Tailwind 设计系统](references/tailwind/guide.md) | 指南以 v4 为基准。先看项目依赖和 CSS 入口，再选择对应版本的配置写法。 |
| React 或 Next.js 首屏慢、请求串行、包体积或重渲染 | [React 与 Next.js 性能](references/react-performance/guide.md) | 沿实际请求和渲染路径查找瓶颈，再阅读对应规则及改动前后的代码示例。 |
| React 组件布尔参数过多、组合困难、状态归属不清 | [React 组件组合](references/react-composition/guide.md) | 检查调用方和状态拥有者，通过组合、插槽式子组件或清晰的变体表达契约。React 19 的 API 只用于相应版本。 |
| Vue 3 单文件组件、响应性、composable、组件通信 | [Vue 组件开发](references/vue/guide.md) | 明确状态所有者和 props / emits 契约，再选择 computed、watch 或 composable。跟随项目采用的 API 风格。 |
| Nuxt 路由、服务端取数、SSR 与水合 | [Nuxt 4](references/nuxt/guide.md) | 在服务端渲染与浏览器接管之间追踪数据。组件内部的响应性和数据流见 Vue 专题。 |
| 交互式 3D 场景、材质、光照、着色器或动画 | [Three.js](references/three/guide.md) | 按场景、相机、资源加载或动画选择参考。示例使用原生 Three.js，导入路径和清理逻辑要匹配项目版本。 |
| 用 React 制作视频、字幕、地图动画、预览或导出 | [Remotion](references/remotion/guide.md) | 按工作内容进入构图、帧时间、字幕或渲染资料。确定画幅、帧率和时长后，用预览核对关键帧，交付视频时再核对导出文件。 |

跨专题时，用同一个可观察结果串起检查。例如，Nuxt 页面首次加载出现重复请求时，沿取数和水合路径检查，再看触发请求的 Vue 响应式副作用。Tailwind 卡片嵌入窄侧栏后溢出时，应在实际容器宽度下验证布局。Three.js 场景嵌入 Remotion 时，用视频帧号驱动动画，并在相同帧号核对预览与导出画面。

合并包保留了各专题的[上游项目与版本记录](notices/sources.md)。
