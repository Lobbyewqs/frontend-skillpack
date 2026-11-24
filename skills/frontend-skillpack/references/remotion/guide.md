# Remotion 视频制作

把视频写成可按帧求值的 React 组件。先约定画幅、帧率、时长、素材与交付格式。已有工程沿用其中注册合成的入口和本地 Remotion 版本。

## 从时间线到画面

- 在根组件里注册一个有稳定 ID 的 Composition，指定宽、高、fps、durationInFrames 和默认参数。画面内容放在它引用的 React 组件里。总帧数为 90 时，有效帧为 0 到 89。
- 用 Sequence 表达镜头的起点和长度。在 Sequence 内，useCurrentFrame() 从该镜头的第 0 帧开始计数。需要把几个镜头对齐到同一段音频时，明确每个值属于全片时间还是镜头局部时间。
- 对位移、透明度或材质参数，用当前帧计算所需值。插值超出区间时按设计截断，在预览中任意拖动时间轴都应得到相同画面。Three.js 场景也应由视频帧驱动。
- 播放项目自带的视频、旁白和字体时，使用项目的素材目录和加载机制。检查首帧、转场交界和最后一帧。文字含换行或字体替换时，在目标画幅下预览实际排版。

例如，这个标题在镜头开始的半秒内淡入。把组件放进 Sequence 后，动画就随镜头起点移动。

```tsx
import {interpolate, useCurrentFrame, useVideoConfig} from 'remotion'

export function ChapterTitle({title}: {title: string}) {
  const frame = useCurrentFrame()
  const {fps} = useVideoConfig()
  const fadeFrames = Math.max(1, Math.round(fps / 2))
  const opacity = interpolate(frame, [0, fadeFrames], [0, 1], {
    extrapolateLeft: 'clamp',
    extrapolateRight: 'clamp',
  })
  return <h1 style={{opacity}}>{title}</h1>
}
```

## 字幕和声音

把对齐音频的字幕保留为毫秒区间。对第 `frame` 帧，用 `frame * 1000 / fps` 取得时间戳。采用“起点包含、终点排除”的区间，相邻字幕在交界帧只显示一条。分词高亮时沿用词级时间戳，移动整段镜头时检查旁白和字幕是否同时移动。导出前听一次开头和结尾，检查音频是否被截断。

## 预览和交付

从项目本地 CLI 打开 Studio，先定位合成 ID，再检查关键帧。按项目使用的包管理器运行命令。下面以现有 npm 项目为例，入口和合成 ID 用项目中的实际值替换。

```sh
npx remotion studio
npx remotion still src/index.ts ProductIntro out/preview.png --frame=30
npx remotion render src/index.ts ProductIntro out/product-intro.mp4
```

预览、单帧与整片导出可以分别执行。交付成片时，核对文件能播放、画幅和时长符合要求，检查字幕切换、音画同步及最后一帧。嵌入播放器时，让页面控件和视频通过输入参数共享同一份数据。

## 深入具体任务

以下链接指向本包采用的官方版本。项目中已装有原版 Remotion 技能时，也可直接阅读其目录里同名的 REFERENCE.md。

| 任务 | 官方资料 |
|---|---|
| 新建工程、注册合成、镜头和时间线 | [创建](https://github.com/remotion-dev/skills/blob/89c8afa3eee9cdd83838ac31979c2ba1384615aa/skills/remotion-best-practices/remotion-create/REFERENCE.md) · [合成标记](https://github.com/remotion-dev/skills/blob/89c8afa3eee9cdd83838ac31979c2ba1384615aa/skills/remotion-best-practices/remotion-markup/REFERENCE.md) |
| 字幕转录、SRT、音视频时长与裁切 | [字幕](https://github.com/remotion-dev/skills/blob/89c8afa3eee9cdd83838ac31979c2ba1384615aa/skills/remotion-best-practices/remotion-captions/REFERENCE.md) · [多媒体](https://github.com/remotion-dev/skills/blob/89c8afa3eee9cdd83838ac31979c2ba1384615aa/skills/remotion-best-practices/remotion-multimedia/REFERENCE.md) |
| 地图、路线、编辑器中的交互参数 | [地图](https://github.com/remotion-dev/skills/blob/89c8afa3eee9cdd83838ac31979c2ba1384615aa/skills/remotion-best-practices/remotion-maps/REFERENCE.md) · [交互](https://github.com/remotion-dev/skills/blob/89c8afa3eee9cdd83838ac31979c2ba1384615aa/skills/remotion-best-practices/remotion-interactivity/REFERENCE.md) |
| Studio、渲染配置、应用内播放器及服务端渲染 | [Studio](https://github.com/remotion-dev/skills/blob/89c8afa3eee9cdd83838ac31979c2ba1384615aa/skills/remotion-best-practices/remotion-studio/REFERENCE.md) · [渲染](https://github.com/remotion-dev/skills/blob/89c8afa3eee9cdd83838ac31979c2ba1384615aa/skills/remotion-best-practices/remotion-render/REFERENCE.md) · [应用集成](https://github.com/remotion-dev/skills/blob/89c8afa3eee9cdd83838ac31979c2ba1384615aa/skills/remotion-best-practices/remotion-saas/REFERENCE.md) |
| 核对 API、升级依赖或确认授权条件 | [文档](https://github.com/remotion-dev/skills/blob/89c8afa3eee9cdd83838ac31979c2ba1384615aa/skills/remotion-best-practices/remotion-docs/REFERENCE.md) · [升级](https://github.com/remotion-dev/skills/blob/89c8afa3eee9cdd83838ac31979c2ba1384615aa/skills/remotion-best-practices/remotion-upgrade/REFERENCE.md) · [许可](https://github.com/remotion-dev/skills/blob/89c8afa3eee9cdd83838ac31979c2ba1384615aa/skills/remotion-best-practices/remotion-license/REFERENCE.md) |
