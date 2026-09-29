# My Trip 项目计划

## 一句话概括

一个用独立手绘地图、路线、文字与影像，长期记录并回顾每一次旅行的个人旅行手账网站。

英文仓库描述：

> A personal travel journal featuring uniquely illustrated maps, routes, stories, and memories from every journey.

## 项目定位

My Trip 是一个轻量的个人旅行档案网站，不是导航地图、攻略平台或通用地图生成器。

网站提供稳定的旅行叙事框架，但每趟旅行都是一件独立作品：拥有自己的抽象地图、构图、配色、贴纸、字体、路线和动画。即使再次前往同一座城市，也可以根据当次旅行的季节、同行者、主题和记忆重新设计。

核心原则：

- 整体保持“左侧旅行地图、右侧旅行手账”的主要布局。
- 右侧标题、DAY 切换、行程列表和地点详情多数情况下保持稳定。
- 每趟旅行的地图区域独立创作，不套用统一城市模板。
- 地图强调当地特色和旅行记忆，不追求精确导航或真实比例。
- 复用布局、状态和交互，不复用每趟旅行的艺术表达。
- 第一阶段保持静态、轻量，不引入账号、数据库和后台管理。

## 技术方向

- Vue 3
- Vite
- JavaScript（需要更严格的数据约束时再迁移 TypeScript）
- Vue Router
- SVG、CSS 动画和少量 Web Animations API
- JSON 旅行数据
- GitHub Actions
- GitHub Pages

Vue 项目使用官方 `create-vue` 创建，底层构建工具为 Vite。GitHub Pages 通过 GitHub Actions 自动部署。

---

## 第一阶段：建立 Vue 3 项目并部署 GitHub Pages

### 目标

先建立稳定的开发和发布链路。这个阶段只验证项目能够开发、构建和上线，不制作完整旅行页面。

### 工作内容

- [ ] 使用官方 `create-vue` 创建 Vue 3 + Vite 项目。
- [ ] 清理官方示例内容，保留最小项目骨架。
- [ ] 配置代码格式和基础目录。
- [ ] 配置 Vue Router；GitHub Pages 首版采用兼容静态托管的路由方式。
- [ ] 根据 Pages 地址配置 Vite `base`。
- [ ] 创建 `.github/workflows/deploy.yml`。
- [ ] 在 GitHub 仓库中启用 Pages，并将发布源设置为 GitHub Actions。
- [ ] 推送到 `main` 后自动安装依赖、构建并发布 `dist`。
- [ ] 更新 README，记录本地开发、构建和部署方式。

### 建议初始目录

```text
my-trip/
├─ .github/
│  └─ workflows/
│     └─ deploy.yml
├─ public/
├─ src/
│  ├─ assets/
│  ├─ router/
│  ├─ views/
│  ├─ App.vue
│  └─ main.js
├─ index.html
├─ package.json
├─ vite.config.js
└─ README.md
```

### 验收标准

- [ ] `npm run dev` 可以启动本地开发环境。
- [ ] `npm run build` 成功生成 `dist`。
- [ ] GitHub Actions 部署流程成功。
- [ ] GitHub Pages 地址可以访问 Vue 首页。
- [ ] CSS、JavaScript、字体和图片路径正常。
- [ ] 页面刷新后不出现 404。

### 阶段产物

- 可运行的 Vue 3 项目。
- 可访问的 GitHub Pages 地址。
- 自动部署工作流。
- 基础 README。

---

## 第二阶段：完成第一趟旅行 Demo

### 目标

将现有“福州 → 广州”静态 Demo 迁移成 Vue 版本，完成一套可以继续迭代的旅行详情页。

### 组件边界

只进行轻量组件化，不把每个标签、按钮或贴纸都拆成组件。

```text
TripView.vue
├─ 左侧：本次旅行独立的 MapScene.vue
└─ 右侧：相对稳定的 ItineraryPanel.vue
```

- `TripView.vue`：负责左右布局，保存当前 DAY 和当前选中地点。
- `ItineraryPanel.vue`：负责旅行标题、摘要、DAY 切换、行程列表和地点详情。
- `MapScene.vue`：本趟旅行独立创作的 SVG 地图、贴纸、路线和动画。
- `trip.json`：记录日期、地点、DAY、时间、文字和媒体引用，不控制艺术风格。

### 建议目录

```text
src/
├─ views/
│  ├─ TripView.vue
│  └─ TripArchive.vue
├─ components/
│  └─ ItineraryPanel.vue
├─ trips/
│  └─ guangzhou-2026/
│     ├─ trip.json
│     ├─ MapScene.vue
│     ├─ theme.css
│     ├─ stickers/
│     └─ media/
└─ router/
   └─ index.js
```

### 工作内容

- [ ] 将当前页面的色彩、纸张纹理、字体和整体布局迁移到 Vue。
- [ ] 保留桌面端“左侧地图、右侧手账”。
- [ ] 移动端改为“地图在上、行程在下”。
- [ ] 实现 `DAY 01 / DAY 02` 切换。
- [ ] 实现福州到广州的进入路线动画。
- [ ] 切换 DAY 时擦除旧路线并绘制新路线。
- [ ] 根据当天数据渲染地点贴纸和行程卡片。
- [ ] 点击地图贴纸时选中右侧行程。
- [ ] 点击右侧行程时突出显示地图地点。
- [ ] 显示地点详情和未来媒体占位。
- [ ] 放大并重新平衡左侧地图，减少无意义的底部空白。
- [ ] 在地图下方预留地点手账、照片或视频展示区域。
- [ ] 将广州地图保留为独立 `MapScene.vue`，不抽象成通用城市底图。
- [ ] 在 GitHub Pages 验证与本地一致的交互和视觉效果。

### 验收标准

- [ ] GitHub Pages 上可以完整浏览广州 Demo。
- [ ] DAY 切换后只聚焦当天地点和路线。
- [ ] 地图贴纸与右侧行程双向联动。
- [ ] 路线绘制和贴纸进入动画正常。
- [ ] 电脑和手机没有横向溢出或重要内容遮挡。
- [ ] 旅行文字来自 `trip.json`。
- [ ] 广州地图可以在不修改核心引擎的情况下独立调整。

### 阶段产物

- 第一篇可公开访问的旅行作品。
- 可复用的旅行详情页骨架。
- 一套地图与手账之间的交互约定。

---

## 第三阶段：固化项目愿景与设计基线

### 目标

根据第一版实际成品，将项目定位、视觉原则、数据约定和新增旅行流程写成文档，作为后续迭代的判断依据。

### 文档产物

#### `docs/PRODUCT_VISION.md`

记录：

- 网站存在的目的。
- 面向个人记录与长期回顾的核心场景。
- 网站明确不做的事情。
- 首页、旅行详情和未来旅行档案的关系。
- 后续功能的优先级判断原则。

#### `docs/DESIGN_GUIDE.md`

记录：

- 左地图、右手账的整体构图。
- 手绘、拼贴、纸张纹理等基础视觉语言。
- 哪些布局保持统一，哪些内容允许每次重新设计。
- 地图的抽象程度和当地特色表达原则。
- 色彩、字体、贴纸、路线和动画的使用原则。
- 地图空白区域如何承担内容或交互，而不是堆装饰。
- 需要避免的“统一模板换文字”效果。

#### `docs/TRIP_FORMAT.md`

记录：

- `trip.json` 字段及示例。
- DAY、地点、路线和媒体的数据结构。
- `TripView`、`MapScene` 和 `ItineraryPanel` 的交互接口。
- 新增一趟旅行所需的文件和步骤。
- 同一城市再次旅行时创建独立艺术包的规则。
- 图片、视频和静态资源的组织方式。

### 验收标准

- [ ] 新加入项目的人可以通过文档理解网站目标。
- [ ] 可以明确区分“稳定的旅行引擎”和“独立的旅行艺术包”。
- [ ] 新增旅行时不需要复制或修改核心交互逻辑。
- [ ] 文档足以判断一个新设计是否符合项目方向。
- [ ] 后续迭代不会把网站逐渐变成千篇一律的地图模板。

---

## 长期内容结构

每趟旅行建立独立目录：

```text
src/trips/
├─ guangzhou-2026-autumn/
│  ├─ trip.json
│  ├─ MapScene.vue
│  ├─ theme.css
│  └─ media/
├─ guangzhou-2028-night/
│  ├─ trip.json
│  ├─ MapScene.vue
│  ├─ theme.css
│  └─ media/
└─ fuzhou-2027-spring/
   ├─ trip.json
   ├─ MapScene.vue
   ├─ theme.css
   └─ media/
```

同一城市的两次旅行不共享地图组件，只共享网站提供的布局、DAY 状态、地点选择和媒体展示能力。

## 暂不纳入首版

- 登录和账号系统。
- 数据库。
- 在线后台编辑器。
- 在线图片上传。
- 精确地图、导航和真实路线计算。
- 高德、百度或 Mapbox 地图 API。
- 多用户协作。
- 服务端渲染。

这些功能只有在真实使用过程中产生明确需求时再考虑。

## 总结

项目按以下顺序推进：

1. 建立 Vue 3 + Vite 项目并部署 GitHub Pages。
2. 将广州静态页面迁移为第一个 Vue 旅行 Demo。
3. 根据实际成品固化产品愿景、设计规则和旅行数据格式。

最终原则：

> 用统一的旅行叙事框架，承载每一次都独一无二的手绘旅行记忆。

## 官方参考

- [Vue 快速开始](https://vuejs.org/guide/quick-start.html)
- [Vite 静态站点部署](https://vite.dev/guide/static-deploy.html)
- [GitHub Pages 文档](https://docs.github.com/pages)
