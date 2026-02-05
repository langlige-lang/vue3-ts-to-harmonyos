<template>
  <section class="concepts" id="concepts">
    <div class="section-header">
      <span class="section-tag">概念对照</span>
      <h2 class="section-title">Vue vs 鸿蒙</h2>
      <p class="section-subtitle">一一对应，快速理解</p>
    </div>
    
    <div class="cards-container">
      <div 
        v-for="(card, index) in conceptCards" 
        :key="index"
        class="concept-card"
        :class="{ 'flipped': flippedCards.has(index) }"
        :style="{ 
          animationDelay: `${index * 0.1}s`,
          '--card-index': index 
        }"
        @click="flipCard(index)"
        @mouseenter="handleCardHover(index, true)"
        @mouseleave="handleCardHover(index, false)"
      >
        <div class="card-inner">
          <!-- 正面 - Vue -->
          <div class="card-face card-front">
            <div class="card-glow"></div>
            <div class="card-content">
              <div class="card-header">
                <span class="card-badge vue">Vue3</span>
                <div class="card-icon-wrapper">
                  <component :is="card.vueIcon" class="card-icon" />
                </div>
              </div>
              <h3 class="card-title">{{ card.vueConcept }}</h3>
              <code class="card-code vue">{{ card.vueCode }}</code>
              <p class="card-desc">{{ card.vueDesc }}</p>
              <div class="card-hint">
                <span class="hint-icon">👆</span>
                <span>点击翻转</span>
              </div>
            </div>
          </div>
          
          <!-- 背面 - Harmony -->
          <div class="card-face card-back">
            <div class="card-glow"></div>
            <div class="card-content">
              <div class="card-header">
                <span class="card-badge harmony">HarmonyOS</span>
                <div class="card-icon-wrapper harmony">
                  <component :is="card.harmonyIcon" class="card-icon" />
                </div>
              </div>
              <h3 class="card-title">{{ card.harmonyConcept }}</h3>
              <code class="card-code harmony">{{ card.harmonyCode }}</code>
              <p class="card-desc">{{ card.harmonyDesc }}</p>
              <div class="card-hint">
                <span class="hint-icon">🔄</span>
                <span>点击返回</span>
              </div>
            </div>
          </div>
        </div>
        
        <!-- 悬浮粒子 -->
        <div class="card-particles">
          <span v-for="n in 3" :key="n" class="particle"></span>
        </div>
      </div>
    </div>
    
    <!-- 装饰元素 -->
    <div class="decoration-circle"></div>
    <div class="decoration-line"></div>
  </section>
</template>

<script setup lang="ts">
import { ref, h } from 'vue'

// 图标组件 - 使用 h() 函数
const RefIcon = () => h('svg', { viewBox: '0 0 24 24', fill: 'none', stroke: 'currentColor', 'stroke-width': '2' }, [
  h('circle', { cx: '12', cy: '12', r: '3' }),
  h('path', { d: 'M12 1v6m0 6v6m4.22-10.22l4.24-4.24M6.34 17.66l-4.24 4.24M23 12h-6m-6 0H1m20.24 4.24l-4.24-4.24M6.34 6.34L2.1 2.1' })
])

const ListIcon = () => h('svg', { viewBox: '0 0 24 24', fill: 'none', stroke: 'currentColor', 'stroke-width': '2' }, [
  h('line', { x1: '8', y1: '6', x2: '21', y2: '6' }),
  h('line', { x1: '8', y1: '12', x2: '21', y2: '12' }),
  h('line', { x1: '8', y1: '18', x2: '21', y2: '18' }),
  h('line', { x1: '3', y1: '6', x2: '3.01', y2: '6' }),
  h('line', { x1: '3', y1: '12', x2: '3.01', y2: '12' }),
  h('line', { x1: '3', y1: '18', x2: '3.01', y2: '18' })
])

const IfIcon = () => h('svg', { viewBox: '0 0 24 24', fill: 'none', stroke: 'currentColor', 'stroke-width': '2' }, [
  h('path', { d: 'M9 12h6m-6 4h6m2 5H7a2 2 0 01-2-2V5a2 2 0 012-2h5.586a1 1 0 01.707.293l5.414 5.414a1 1 0 01.293.707V19a2 2 0 01-2 2z' })
])

const ClickIcon = () => h('svg', { viewBox: '0 0 24 24', fill: 'none', stroke: 'currentColor', 'stroke-width': '2' }, [
  h('path', { d: 'M15 15l-2 5L9 9l11 4-5 2zm0 0l5 5M7.188 2.239l.777 2.897M5.136 7.965l-2.898-.777M13.95 4.05l-2.122 2.122m-5.657 5.656l-2.12 2.122' })
])

const PropsIcon = () => h('svg', { viewBox: '0 0 24 24', fill: 'none', stroke: 'currentColor', 'stroke-width': '2' }, [
  h('path', { d: 'M4 4h16c1.1 0 2 .9 2 2v12c0 1.1-.9 2-2 2H4c-1.1 0-2-.9-2-2V6c0-1.1.9-2 2-2z' }),
  h('polyline', { points: '22,6 12,13 2,6' })
])

const ComputedIcon = () => h('svg', { viewBox: '0 0 24 24', fill: 'none', stroke: 'currentColor', 'stroke-width': '2' }, [
  h('path', { d: 'M12 2L2 7l10 5 10-5-10-5zM2 17l10 5 10-5M2 12l10 5 10-5' })
])

const WatchIcon = () => h('svg', { viewBox: '0 0 24 24', fill: 'none', stroke: 'currentColor', 'stroke-width': '2' }, [
  h('circle', { cx: '12', cy: '12', r: '10' }),
  h('polyline', { points: '12 6 12 12 16 14' })
])

const StyleIcon = () => h('svg', { viewBox: '0 0 24 24', fill: 'none', stroke: 'currentColor', 'stroke-width': '2' }, [
  h('path', { d: 'M12 2L2 7l10 5 10-5-10-5zM2 17l10 5 10-5M2 12l10 5 10-5' })
])

const conceptCards = [
  {
    vueConcept: 'ref() / reactive()',
    vueCode: "const count = ref(0)",
    vueDesc: 'Vue3响应式状态声明',
    vueIcon: RefIcon,
    harmonyConcept: '@State',
    harmonyCode: '@State count: number = 0',
    harmonyDesc: 'ArkTS组件状态装饰器',
    harmonyIcon: RefIcon
  },
  {
    vueConcept: 'v-for',
    vueCode: '<li v-for="item in list">',
    vueDesc: '列表渲染指令',
    vueIcon: ListIcon,
    harmonyConcept: 'ForEach',
    harmonyCode: 'ForEach(this.list, (item) => {})',
    harmonyDesc: 'ArkTS列表组件',
    harmonyIcon: ListIcon
  },
  {
    vueConcept: 'v-if / v-show',
    vueCode: '<div v-if="isShow">',
    vueDesc: '条件渲染指令',
    vueIcon: IfIcon,
    harmonyConcept: 'if() / visibility()',
    harmonyCode: 'if (this.isShow) { Text() }',
    harmonyDesc: 'ArkTS条件渲染',
    harmonyIcon: IfIcon
  },
  {
    vueConcept: '@click',
    vueCode: '<button @click="handle">',
    vueDesc: '事件绑定',
    vueIcon: ClickIcon,
    harmonyConcept: '.onClick()',
    harmonyCode: 'Button().onClick(() => {})',
    harmonyDesc: 'ArkTS事件链式调用',
    harmonyIcon: ClickIcon
  },
  {
    vueConcept: 'props',
    vueCode: 'defineProps(["title"])',
    vueDesc: '父子组件传参',
    vueIcon: PropsIcon,
    harmonyConcept: '@Prop',
    harmonyCode: '@Prop title: string',
    harmonyDesc: 'ArkTS属性装饰器',
    harmonyIcon: PropsIcon
  },
  {
    vueConcept: 'computed()',
    vueCode: 'const double = computed(() => count * 2)',
    vueDesc: '计算属性',
    vueIcon: ComputedIcon,
    harmonyConcept: '@Computed',
    harmonyCode: '@Computed get double(): number',
    harmonyDesc: 'ArkTS计算属性装饰器',
    harmonyIcon: ComputedIcon
  },
  {
    vueConcept: 'watch()',
    vueCode: 'watch(count, (newVal) => {})',
    vueDesc: '监听器',
    vueIcon: WatchIcon,
    harmonyConcept: '@Watch',
    harmonyCode: '@Watch("onCountChange")',
    harmonyDesc: 'ArkTS监听装饰器',
    harmonyIcon: WatchIcon
  },
  {
    vueConcept: 'CSS Styles',
    vueCode: '.class { color: red; }',
    vueDesc: '样式定义',
    vueIcon: StyleIcon,
    harmonyConcept: '链式样式',
    harmonyCode: 'Text().fontColor(Color.Red)',
    harmonyDesc: 'ArkTS链式样式调用',
    harmonyIcon: StyleIcon
  }
]

const flippedCards = ref(new Set<number>())

const flipCard = (index: number) => {
  if (flippedCards.value.has(index)) {
    flippedCards.value.delete(index)
  } else {
    flippedCards.value.add(index)
  }
}

const handleCardHover = (_index: number, _isHovering: boolean) => {
  // 可以添加额外的悬停效果
}
</script>

<style scoped>
.concepts {
  padding: 120px 40px;
  position: relative;
  overflow: hidden;
}

.section-header {
  text-align: center;
  margin-bottom: 80px;
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
  background: linear-gradient(135deg, #42b883 0%, #fe8301 50%, #35495e 100%);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
}

.section-subtitle {
  font-size: 1.2rem;
  color: var(--body);
  opacity: 0.7;
}

/* 卡片网格 */
.cards-container {
  max-width: 1400px;
  margin: 0 auto;
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(320px, 1fr));
  gap: 30px;
  perspective: 2000px;
}

/* 3D翻转卡片 */
.concept-card {
  height: 420px;
  cursor: pointer;
  perspective: 1000px;
  animation: slideInUp 0.8s ease-out forwards;
  opacity: 0;
  transform-style: preserve-3d;
}

.card-inner {
  position: relative;
  width: 100%;
  height: 100%;
  transform-style: preserve-3d;
  transition: transform 0.8s cubic-bezier(0.19, 1, 0.22, 1);
}

.concept-card.flipped .card-inner {
  transform: rotateY(180deg);
}

.card-face {
  position: absolute;
  width: 100%;
  height: 100%;
  backface-visibility: hidden;
  border-radius: 24px;
  overflow: hidden;
  transition: all 0.4s cubic-bezier(0.19, 1, 0.22, 1);
}

.card-front {
  background: linear-gradient(145deg, #ffffff 0%, #f8f9fa 100%);
  border: 1px solid rgba(66, 184, 131, 0.2);
  box-shadow: 
    0 10px 40px rgba(0, 0, 0, 0.08),
    0 0 0 1px rgba(66, 184, 131, 0.1);
}

.card-back {
  background: linear-gradient(145deg, #ffffff 0%, #f8f9fa 100%);
  border: 1px solid rgba(254, 131, 1, 0.2);
  box-shadow: 
    0 10px 40px rgba(0, 0, 0, 0.08),
    0 0 0 1px rgba(254, 131, 1, 0.1);
  transform: rotateY(180deg);
}

/* 卡片悬停效果 */
.concept-card:hover .card-front,
.concept-card:hover .card-back {
  transform: translateY(-10px);
  box-shadow: 
    0 30px 60px rgba(0, 0, 0, 0.12),
    0 0 0 1px rgba(254, 131, 1, 0.2);
}

.concept-card.flipped:hover .card-inner {
  transform: rotateY(180deg) translateY(-10px);
}

/* 光晕效果 */
.card-glow {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  opacity: 0;
  transition: opacity 0.4s ease;
  pointer-events: none;
}

.card-front .card-glow {
  background: radial-gradient(
    circle at 50% 0%,
    rgba(66, 184, 131, 0.15) 0%,
    transparent 70%
  );
}

.card-back .card-glow {
  background: radial-gradient(
    circle at 50% 0%,
    rgba(254, 131, 1, 0.15) 0%,
    transparent 70%
  );
}

.concept-card:hover .card-glow {
  opacity: 1;
}

/* 卡片内容 */
.card-content {
  padding: 30px;
  height: 100%;
  display: flex;
  flex-direction: column;
  position: relative;
  z-index: 1;
}

.card-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 20px;
}

.card-badge {
  padding: 6px 14px;
  border-radius: 20px;
  font-size: 0.75rem;
  font-weight: 700;
  text-transform: uppercase;
  letter-spacing: 0.5px;
}

.card-badge.vue {
  background: rgba(66, 184, 131, 0.15);
  color: #42b883;
}

.card-badge.harmony {
  background: rgba(254, 131, 1, 0.15);
  color: #fe8301;
}

.card-icon-wrapper {
  width: 50px;
  height: 50px;
  background: rgba(66, 184, 131, 0.1);
  border-radius: 14px;
  display: flex;
  align-items: center;
  justify-content: center;
  color: #42b883;
  transition: all 0.4s cubic-bezier(0.68, -0.6, 0.32, 1.6);
}

.card-icon-wrapper.harmony {
  background: rgba(254, 131, 1, 0.1);
  color: #fe8301;
}

.concept-card:hover .card-icon-wrapper {
  transform: rotateY(360deg) scale(1.1);
}

.card-icon {
  width: 24px;
  height: 24px;
}

.card-title {
  font-size: 1.4rem;
  font-weight: 700;
  margin-bottom: 16px;
  color: var(--title);
}

.card-code {
  display: block;
  padding: 16px;
  border-radius: 12px;
  font-family: 'Fira Code', monospace;
  font-size: 0.85rem;
  margin-bottom: 16px;
  overflow-x: auto;
}

.card-code.vue {
  background: rgba(66, 184, 131, 0.08);
  color: #2c3e50;
  border-left: 3px solid #42b883;
}

.card-code.harmony {
  background: rgba(254, 131, 1, 0.08);
  color: #2c3e50;
  border-left: 3px solid #fe8301;
}

.card-desc {
  font-size: 0.95rem;
  color: var(--body);
  opacity: 0.8;
  line-height: 1.6;
  flex: 1;
}

.card-hint {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 8px;
  margin-top: 16px;
  padding-top: 16px;
  border-top: 1px solid rgba(0, 0, 0, 0.05);
  font-size: 0.8rem;
  color: var(--body);
  opacity: 0.6;
}

.hint-icon {
  font-size: 1rem;
}

/* 悬浮粒子 */
.card-particles {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  pointer-events: none;
  overflow: hidden;
  border-radius: 24px;
}

.particle {
  position: absolute;
  width: 6px;
  height: 6px;
  background: var(--primary);
  border-radius: 50%;
  opacity: 0;
}

.concept-card:hover .particle {
  animation: particleFloat 1s ease-out forwards;
}

.particle:nth-child(1) {
  top: 20%;
  left: 10%;
  animation-delay: 0s;
}

.particle:nth-child(2) {
  top: 60%;
  right: 15%;
  animation-delay: 0.2s;
}

.particle:nth-child(3) {
  bottom: 20%;
  left: 30%;
  animation-delay: 0.4s;
}

@keyframes particleFloat {
  0% {
    opacity: 0.6;
    transform: translateY(0) scale(1);
  }
  100% {
    opacity: 0;
    transform: translateY(-40px) scale(0);
  }
}

/* 装饰元素 */
.decoration-circle {
  position: absolute;
  top: 10%;
  right: -100px;
  width: 400px;
  height: 400px;
  border: 1px solid rgba(254, 131, 1, 0.1);
  border-radius: 50%;
  pointer-events: none;
  animation: rotate 30s linear infinite;
}

.decoration-line {
  position: absolute;
  bottom: 20%;
  left: -50px;
  width: 200px;
  height: 2px;
  background: linear-gradient(90deg, transparent, rgba(254, 131, 1, 0.3), transparent);
  transform: rotate(-45deg);
  pointer-events: none;
}

/* 响应式 */
@media (max-width: 768px) {
  .concepts {
    padding: 80px 20px;
  }
  
  .cards-container {
    grid-template-columns: 1fr;
  }
  
  .concept-card {
    height: 380px;
  }
}
</style>