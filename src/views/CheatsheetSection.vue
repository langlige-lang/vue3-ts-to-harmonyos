<template>
  <section class="cheatsheet" id="cheatsheet">
    <div class="section-header">
      <span class="section-tag">速查手册</span>
      <h2 class="section-title">常用语法速查</h2>
      <p class="section-subtitle">开发时随手查阅，提高效率</p>
    </div>
    
    <div class="cheatsheet-container">
      <div 
        v-for="(section, sectionIndex) in cheatSections" 
        :key="sectionIndex"
        class="cheat-section"
        :class="{ 'expanded': expandedSections.has(sectionIndex) }"
        :style="{ animationDelay: `${sectionIndex * 0.1}s` }"
      >
        <div 
          class="section-header-bar"
          @click="toggleSection(sectionIndex)"
        >
          <div class="section-icon" :class="section.iconClass">
            <component :is="section.icon" />
          </div>
          <h3 class="section-name">{{ section.title }}</h3>
          <span class="section-count">{{ section.items.length }} 项</span>
          <span class="expand-icon">
            <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
              <polyline points="6 9 12 15 18 9"></polyline>
            </svg>
          </span>
        </div>
        
        <div class="section-content">
          <div class="items-grid">
            <div 
              v-for="(item, itemIndex) in section.items" 
              :key="itemIndex"
              class="cheat-item"
              :style="{ animationDelay: `${itemIndex * 0.05}s` }"
            >
              <div class="item-header">
                <code class="item-code">{{ item.code }}</code>
                <span class="item-badge" :class="item.type">{{ item.type }}</span>
              </div>
              <p class="item-desc">{{ item.desc }}</p>
              <div class="item-example" v-if="item.example">
                <code>{{ item.example }}</code>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
    
    <!-- 搜索提示 -->
    <div class="search-hint">
      <div class="hint-icon">💡</div>
      <p>提示：使用浏览器搜索功能 (Ctrl+F) 快速查找内容</p>
    </div>
  </section>
</template>

<script setup lang="ts">
import { ref } from 'vue'

// 图标组件
const DecoratorIcon = () => (
  <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
    <rect x="4" y="4" width="16" height="16" rx="2" ry="2"></rect>
    <rect x="9" y="9" width="6" height="6"></rect>
    <line x1="9" y1="1" x2="9" y2="4"></line>
    <line x1="15" y1="1" x2="15" y2="4"></line>
    <line x1="9" y1="20" x2="9" y2="23"></line>
    <line x1="15" y1="20" x2="15" y2="23"></line>
    <line x1="20" y1="9" x2="23" y2="9"></line>
    <line x1="20" y1="14" x2="23" y2="14"></line>
    <line x1="1" y1="9" x2="4" y2="9"></line>
    <line x1="1" y1="14" x2="4" y2="14"></line>
  </svg>
)

const ComponentIcon = () => (
  <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
    <polygon points="12 2 2 7 12 12 22 7 12 2"></polygon>
    <polyline points="2 17 12 22 22 17"></polyline>
    <polyline points="2 12 12 17 22 12"></polyline>
  </svg>
)

const StyleIcon = () => (
  <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
    <circle cx="12" cy="12" r="10"></circle>
    <circle cx="12" cy="12" r="4"></circle>
    <line x1="4.93" y1="4.93" x2="9.17" y2="9.17"></line>
    <line x1="14.83" y1="14.83" x2="19.07" y2="19.07"></line>
    <line x1="14.83" y1="9.17" x2="19.07" y2="4.93"></line>
    <line x1="14.83" y1="9.17" x2="18.36" y2="5.64"></line>
    <line x1="4.93" y1="19.07" x2="9.17" y2="14.83"></line>
  </svg>
)

const AnimationIcon = () => (
  <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
    <polygon points="13 2 3 14 12 14 11 22 21 10 12 10 13 2"></polygon>
  </svg>
)

const RouteIcon = () => (
  <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
    <circle cx="12" cy="12" r="10"></circle>
    <polygon points="16.24 7.76 14.12 14.12 7.76 16.24 9.88 9.88 16.24 7.76"></polygon>
  </svg>
)

const StorageIcon = () => (
  <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
    <ellipse cx="12" cy="5" rx="9" ry="3"></ellipse>
    <path d="M21 12c0 1.66-4 3-9 3s-9-1.34-9-3"></path>
    <path d="M3 5v14c0 1.66 4 3 9 3s9-1.34 9-3V5"></path>
  </svg>
)

const cheatSections = [
  {
    title: '装饰器',
    icon: DecoratorIcon,
    iconClass: 'decorator',
    items: [
      { code: '@State', desc: '组件内部响应式状态', example: '@State count: number = 0', type: '状态' },
      { code: '@Prop', desc: '父组件传入的属性（单向）', example: '@Prop title: string', type: '传参' },
      { code: '@Link', desc: '双向绑定', example: '@Link value: number', type: '绑定' },
      { code: '@Provide', desc: '跨层级提供数据', example: '@Provide theme: string = "dark"', type: '注入' },
      { code: '@Consume', desc: '跨层级消费数据', example: '@Consume theme: string', type: '注入' },
      { code: '@Computed', desc: '计算属性', example: '@Computed get double(): number', type: '计算' },
      { code: '@Watch', desc: '监听状态变化', example: '@Watch("onChange") @State count: number', type: '监听' },
      { code: '@StorageLink', desc: '本地存储绑定', example: '@StorageLink("token") token: string', type: '存储' }
    ]
  },
  {
    title: '布局组件',
    icon: ComponentIcon,
    iconClass: 'component',
    items: [
      { code: 'Column', desc: '垂直排列（flex-col）', example: 'Column({ space: 10 }) { }', type: '布局' },
      { code: 'Row', desc: '水平排列（flex-row）', example: 'Row({ space: 10 }) { }', type: '布局' },
      { code: 'Flex', desc: '通用Flex布局', example: 'Flex({ wrap: FlexWrap.Wrap })', type: '布局' },
      { code: 'Stack', desc: '层叠布局（absolute）', example: 'Stack({ alignContent: Alignment.Center })', type: '布局' },
      { code: 'Grid', desc: '网格布局', example: 'Grid().columnsTemplate("1fr 1fr")', type: '布局' },
      { code: 'List', desc: '列表（虚拟滚动）', example: 'List({ space: 10 }) { ForEach() }', type: '列表' },
      { code: 'Scroll', desc: '滚动容器', example: 'Scroll() { Column() }', type: '滚动' },
      { code: 'Swiper', desc: '轮播组件', example: 'Swiper() { ForEach(images) }', type: '轮播' }
    ]
  },
  {
    title: '基础组件',
    icon: ComponentIcon,
    iconClass: 'basic',
    items: [
      { code: 'Text', desc: '文本显示', example: 'Text("Hello").fontSize(16)', type: '文本' },
      { code: 'Button', desc: '按钮', example: 'Button("Click").onClick(() => {})', type: '按钮' },
      { code: 'TextInput', desc: '输入框', example: 'TextInput({ text: $$this.value })', type: '输入' },
      { code: 'Image', desc: '图片', example: 'Image($r("app.media.logo"))', type: '图片' },
      { code: 'Checkbox', desc: '复选框', example: 'Checkbox().select(this.checked)', type: '选择' },
      { code: 'Slider', desc: '滑块', example: 'Slider({ value: this.val, min: 0, max: 100 })', type: '滑块' },
      { code: 'Progress', desc: '进度条', example: 'Progress({ value: 50, total: 100 })', type: '进度' },
      { code: 'Toggle', desc: '开关', example: 'Toggle({ type: ToggleType.Switch })', type: '开关' }
    ]
  },
  {
    title: '样式属性',
    icon: StyleIcon,
    iconClass: 'style',
    items: [
      { code: '.width()', desc: '设置宽度', example: '.width(100) 或 .width("100%")', type: '尺寸' },
      { code: '.height()', desc: '设置高度', example: '.height(50)', type: '尺寸' },
      { code: '.padding()', desc: '内边距', example: '.padding(16) 或 .padding({ top: 10 })', type: '边距' },
      { code: '.margin()', desc: '外边距', example: '.margin(8)', type: '边距' },
      { code: '.backgroundColor()', desc: '背景颜色', example: '.backgroundColor("#fff")', type: '背景' },
      { code: '.borderRadius()', desc: '圆角', example: '.borderRadius(8)', type: '边框' },
      { code: '.fontSize()', desc: '字体大小', example: '.fontSize(14)', type: '文字' },
      { code: '.fontColor()', desc: '字体颜色', example: '.fontColor(Color.Red)', type: '文字' }
    ]
  },
  {
    title: '动画',
    icon: AnimationIcon,
    iconClass: 'animation',
    items: [
      { code: '.animation()', desc: '属性动画', example: '.animation({ duration: 300 })', type: '动画' },
      { code: 'animateTo()', desc: '显式动画', example: 'animateTo({ curve: Curve.Spring })', type: '动画' },
      { code: '.transition()', desc: '转场动画', example: '.transition(TransitionType.All)', type: '转场' },
      { code: 'Curve', desc: '动画曲线', example: 'Curve.EaseInOut | Curve.Spring', type: '曲线' }
    ]
  },
  {
    title: '路由导航',
    icon: RouteIcon,
    iconClass: 'route',
    items: [
      { code: 'router.pushUrl()', desc: '跳转页面', example: 'router.pushUrl({ url: "pages/Detail" })', type: '跳转' },
      { code: 'router.replaceUrl()', desc: '替换页面', example: 'router.replaceUrl({ url: "pages/Home" })', type: '替换' },
      { code: 'router.back()', desc: '返回上一页', example: 'router.back()', type: '返回' },
      { code: 'router.getParams()', desc: '获取参数', example: 'const params = router.getParams()', type: '参数' }
    ]
  },
  {
    title: '数据存储',
    icon: StorageIcon,
    iconClass: 'storage',
    items: [
      { code: 'preferences.put()', desc: '存储数据', example: 'await pref.put("key", value)', type: '存储' },
      { code: 'preferences.get()', desc: '读取数据', example: 'await pref.get("key", default)', type: '读取' },
      { code: 'preferences.delete()', desc: '删除数据', example: 'await pref.delete("key")', type: '删除' },
      { code: 'preferences.flush()', desc: '提交更改', example: 'await pref.flush()', type: '提交' }
    ]
  }
]

const expandedSections = ref(new Set([0])) // 默认展开第一个

const toggleSection = (index: number) => {
  if (expandedSections.value.has(index)) {
    expandedSections.value.delete(index)
  } else {
    expandedSections.value.add(index)
  }
}
</script>

<style scoped>
.cheatsheet {
  padding: 120px 40px;
  position: relative;
}

.section-header {
  text-align: center;
  margin-bottom: 60px;
}

.section-tag {
  display: inline-block;
  padding: 8px 20px;
  background: rgba(254, 131, 1, 0.1);
  border: 1px solid rgba(254, 131, 1, 0.3);
  border-radius: 50px;
  font-size: 0.85rem;
  font-weight: 600;
  color: var(--primary);
  margin-bottom: 20px;
}

.section-title {
  font-size: clamp(2.5rem, 5vw, 4rem);
  font-weight: 800;
  margin-bottom: 16px;
  color: var(--title);
}

.section-subtitle {
  font-size: 1.2rem;
  color: var(--body);
  opacity: 0.7;
}

/* 速查表容器 */
.cheatsheet-container {
  max-width: 1000px;
  margin: 0 auto;
  display: flex;
  flex-direction: column;
  gap: 16px;
}

.cheat-section {
  background: white;
  border-radius: 16px;
  overflow: hidden;
  box-shadow: 0 4px 20px rgba(0, 0, 0, 0.06);
  animation: slideInUp 0.6s ease-out forwards;
  opacity: 0;
  transition: all 0.4s cubic-bezier(0.19, 1, 0.22, 1);
}

.cheat-section:hover {
  box-shadow: 0 8px 30px rgba(0, 0, 0, 0.1);
}

.section-header-bar {
  display: flex;
  align-items: center;
  gap: 16px;
  padding: 20px 24px;
  cursor: pointer;
  transition: background 0.3s ease;
  user-select: none;
}

.section-header-bar:hover {
  background: rgba(254, 131, 1, 0.03);
}

.section-icon {
  width: 44px;
  height: 44px;
  border-radius: 12px;
  display: flex;
  align-items: center;
  justify-content: center;
  color: white;
  flex-shrink: 0;
}

.section-icon.decorator {
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
}

.section-icon.component {
  background: linear-gradient(135deg, #f093fb 0%, #f5576c 100%);
}

.section-icon.basic {
  background: linear-gradient(135deg, #4facfe 0%, #00f2fe 100%);
}

.section-icon.style {
  background: linear-gradient(135deg, #43e97b 0%, #38f9d7 100%);
}

.section-icon.animation {
  background: linear-gradient(135deg, #fa709a 0%, #fee140 100%);
}

.section-icon.route {
  background: linear-gradient(135deg, #a8edea 0%, #fed6e3 100%);
  color: #333;
}

.section-icon.storage {
  background: linear-gradient(135deg, #ff9a9e 0%, #fecfef 100%);
  color: #333;
}

.section-icon svg {
  width: 22px;
  height: 22px;
}

.section-name {
  flex: 1;
  font-size: 1.2rem;
  font-weight: 700;
  color: var(--title);
}

.section-count {
  padding: 4px 12px;
  background: rgba(0, 0, 0, 0.05);
  border-radius: 20px;
  font-size: 0.8rem;
  font-weight: 600;
  color: var(--body);
}

.expand-icon {
  width: 24px;
  height: 24px;
  color: var(--body);
  opacity: 0.5;
  transition: transform 0.4s cubic-bezier(0.68, -0.6, 0.32, 1.6);
}

.cheat-section.expanded .expand-icon {
  transform: rotate(180deg);
}

/* 展开内容 */
.section-content {
  max-height: 0;
  overflow: hidden;
  transition: max-height 0.5s cubic-bezier(0.19, 1, 0.22, 1);
}

.cheat-section.expanded .section-content {
  max-height: 2000px;
}

.items-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
  gap: 16px;
  padding: 0 24px 24px;
}

.cheat-item {
  padding: 16px;
  background: #f8f9fa;
  border-radius: 12px;
  border-left: 3px solid var(--primary);
  animation: slideInUp 0.4s ease-out forwards;
  opacity: 0;
  transition: all 0.3s ease;
}

.cheat-item:hover {
  background: #fff5eb;
  transform: translateX(5px);
}

.item-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 8px;
}

.item-code {
  font-family: 'Fira Code', monospace;
  font-size: 0.95rem;
  font-weight: 600;
  color: var(--primary);
}

.item-badge {
  padding: 2px 8px;
  border-radius: 4px;
  font-size: 0.7rem;
  font-weight: 600;
  text-transform: uppercase;
}

.item-badge.状态 {
  background: rgba(102, 126, 234, 0.15);
  color: #667eea;
}

.item-badge.传参 {
  background: rgba(240, 147, 251, 0.15);
  color: #f093fb;
}

.item-badge.绑定 {
  background: rgba(67, 233, 123, 0.15);
  color: #43e97b;
}

.item-badge.布局 {
  background: rgba(79, 172, 254, 0.15);
  color: #4facfe;
}

.item-badge.文字 {
  background: rgba(250, 112, 154, 0.15);
  color: #fa709a;
}

.item-badge.动画 {
  background: rgba(254, 131, 1, 0.15);
  color: #fe8301;
}

.item-desc {
  font-size: 0.85rem;
  color: var(--body);
  opacity: 0.8;
  margin-bottom: 8px;
}

.item-example {
  padding: 8px 12px;
  background: rgba(0, 0, 0, 0.05);
  border-radius: 6px;
}

.item-example code {
  font-family: 'Fira Code', monospace;
  font-size: 0.75rem;
  color: #666;
}

/* 搜索提示 */
.search-hint {
  max-width: 1000px;
  margin: 40px auto 0;
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 12px;
  padding: 20px;
  background: rgba(254, 131, 1, 0.05);
  border-radius: 12px;
  border: 1px dashed rgba(254, 131, 1, 0.3);
}

.hint-icon {
  font-size: 1.5rem;
}

.search-hint p {
  font-size: 0.95rem;
  color: var(--body);
}

/* 响应式 */
@media (max-width: 768px) {
  .cheatsheet {
    padding: 80px 20px;
  }
  
  .items-grid {
    grid-template-columns: 1fr;
    padding: 0 16px 16px;
  }
  
  .section-header-bar {
    padding: 16px;
  }
}
</style>