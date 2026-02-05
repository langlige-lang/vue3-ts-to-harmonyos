<template>
  <section class="hero" id="hero">
    <div class="hero-container">
      <!-- 左侧内容 -->
      <div class="hero-content">
        <div class="badge">
          <span class="badge-dot"></span>
          Vue3开发者专属
        </div>
        
        <h1 class="hero-title">
          <span class="title-line" v-for="(line, index) in titleLines" :key="index"
                :style="{ animationDelay: `${0.2 + index * 0.15}s` }">
            {{ line }}
          </span>
        </h1>
        
        <p class="hero-subtitle" :style="{ animationDelay: '0.8s' }">
          用你熟悉的语法，探索全新的世界<br>
          从Vue到鸿蒙，无缝切换的开发体验
        </p>
        
        <div class="hero-stats">
          <div class="stat-item" v-for="(stat, index) in stats" :key="index"
               :style="{ animationDelay: `${1 + index * 0.1}s` }">
            <span class="stat-number">{{ stat.number }}</span>
            <span class="stat-label">{{ stat.label }}</span>
          </div>
        </div>
        
        <div class="hero-cta">
          <a href="#concepts" class="btn-primary magnetic-btn" ref="ctaBtn"
             @mousemove="handleMagneticMove" @mouseleave="handleMagneticLeave">
            开始学习
            <span class="btn-arrow">→</span>
          </a>
          <a href="#code" class="btn-secondary">
            查看代码对比
          </a>
        </div>
      </div>
      
      <!-- 右侧3D手机展示 -->
      <div class="hero-visual">
        <div class="phone-container" ref="phoneContainer"
             @mousemove="handlePhoneTilt" @mouseleave="resetPhoneTilt">
          <!-- 手机模型 -->
          <div class="phone" ref="phone">
            <div class="phone-frame">
              <div class="phone-screen">
                <div class="screen-content">
                  <div class="code-preview">
                    <div class="code-line">
                      <span class="code-keyword">@State</span>
                      <span class="code-var">message</span>: 
                      <span class="code-type">string</span> = 
                      <span class="code-string">'Hello Harmony!'</span>
                    </div>
                    <div class="code-line">
                      <span class="code-keyword">build</span>() {
                    </div>
                    <div class="code-line indent">
                      <span class="code-component">Column</span>() {
                    </div>
                    <div class="code-line indent2">
                      <span class="code-component">Text</span>(<span class="code-var">this</span>.message)
                    </div>
                    <div class="code-line indent2">
                      .<span class="code-prop">fontSize</span>(<span class="code-number">24</span>)
                    </div>
                    <div class="code-line indent">
                      }
                    </div>
                    <div class="code-line">
                      }
                    </div>
                  </div>
                </div>
              </div>
              <div class="phone-notch"></div>
              <div class="phone-reflection"></div>
            </div>
            
            <!-- 悬浮元素 -->
            <div class="floating-card card-1">
              <span class="card-icon">@</span>
              <span class="card-text">Decorator</span>
            </div>
            <div class="floating-card card-2">
              <span class="card-icon">{ }</span>
              <span class="card-text">Struct</span>
            </div>
            <div class="floating-card card-3">
              <span class="card-icon">&lt;/&gt;</span>
              <span class="card-text">Build</span>
            </div>
          </div>
          
          <!-- 光晕效果 -->
          <div class="glow-ring"></div>
          <div class="glow-ring ring-2"></div>
        </div>
      </div>
    </div>
    
    <!-- 滚动提示 -->
    <div class="scroll-hint">
      <span class="scroll-text">向下滚动</span>
      <div class="scroll-arrow"></div>
    </div>
  </section>
</template>

<script setup lang="ts">
import { ref, onMounted } from 'vue'

const titleLines = ['从 Vue', '到鸿蒙']
const stats = [
  { number: '90%', label: '语法相似度' },
  { number: '3天', label: '快速上手' },
  { number: '∞', label: '开发可能' }
]

const phone = ref<HTMLElement | null>(null)
const ctaBtn = ref<HTMLElement | null>(null)

// 手机3D倾斜效果
const handlePhoneTilt = (e: MouseEvent) => {
  if (!phone.value) return
  
  const rect = phone.value.getBoundingClientRect()
  const centerX = rect.left + rect.width / 2
  const centerY = rect.top + rect.height / 2
  
  const rotateY = ((e.clientX - centerX) / rect.width) * 20
  const rotateX = ((centerY - e.clientY) / rect.height) * 20
  
  phone.value.style.transform = `
    perspective(1000px)
    rotateX(${rotateX}deg)
    rotateY(${rotateY}deg)
    translateZ(20px)
  `
}

const resetPhoneTilt = () => {
  if (!phone.value) return
  phone.value.style.transform = ''
}

// 磁性按钮效果
const handleMagneticMove = (e: MouseEvent) => {
  if (!ctaBtn.value) return
  
  const rect = ctaBtn.value.getBoundingClientRect()
  const x = e.clientX - rect.left - rect.width / 2
  const y = e.clientY - rect.top - rect.height / 2
  
  ctaBtn.value.style.transform = `translate(${x * 0.2}px, ${y * 0.2}px) scale(1.05)`
}

const handleMagneticLeave = () => {
  if (!ctaBtn.value) return
  ctaBtn.value.style.transform = ''
}

onMounted(() => {
  // 入场动画
  const observer = new IntersectionObserver((entries) => {
    entries.forEach(entry => {
      if (entry.isIntersecting) {
        entry.target.classList.add('animate-in')
      }
    })
  })
  
  document.querySelectorAll('.stat-item').forEach(el => observer.observe(el))
})
</script>

<style scoped>
.hero {
  min-height: 100vh;
  display: flex;
  flex-direction: column;
  justify-content: center;
  padding: 120px 40px 80px;
  position: relative;
  overflow: hidden;
}

.hero-container {
  max-width: 1400px;
  margin: 0 auto;
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 80px;
  align-items: center;
}

/* 左侧内容 */
.hero-content {
  display: flex;
  flex-direction: column;
  gap: 24px;
}

.badge {
  display: inline-flex;
  align-items: center;
  gap: 8px;
  padding: 8px 16px;
  background: rgba(254, 131, 1, 0.1);
  border: 1px solid rgba(254, 131, 1, 0.3);
  border-radius: 50px;
  font-size: 0.85rem;
  font-weight: 600;
  color: var(--primary);
  width: fit-content;
  animation: slideInUp 0.6s ease-out forwards;
  opacity: 0;
}

.badge-dot {
  width: 8px;
  height: 8px;
  background: var(--primary);
  border-radius: 50%;
  animation: pulse 2s ease-in-out infinite;
}

.hero-title {
  font-size: clamp(3rem, 6vw, 5rem);
  font-weight: 800;
  line-height: 1.1;
  display: flex;
  flex-direction: column;
}

.title-line {
  display: block;
  animation: flipIn 1.2s cubic-bezier(0.19, 1, 0.22, 1) forwards;
  opacity: 0;
  transform-origin: center bottom;
}

.title-line:first-child {
  background: linear-gradient(135deg, #42b883 0%, #35495e 100%);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
}

.title-line:last-child {
  background: linear-gradient(135deg, #fe8301 0%, #ff6b00 100%);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
}

.hero-subtitle {
  font-size: 1.2rem;
  line-height: 1.8;
  color: var(--body);
  max-width: 500px;
  animation: slideInUp 1s ease-out forwards;
  opacity: 0;
}

.hero-stats {
  display: flex;
  gap: 40px;
  margin: 20px 0;
}

.stat-item {
  display: flex;
  flex-direction: column;
  gap: 4px;
  animation: slideInUp 0.8s ease-out forwards;
  opacity: 0;
}

.stat-number {
  font-family: 'Poppins', sans-serif;
  font-size: 2.5rem;
  font-weight: 800;
  color: var(--primary);
  line-height: 1;
}

.stat-label {
  font-size: 0.9rem;
  color: var(--body);
  opacity: 0.7;
}

.hero-cta {
  display: flex;
  gap: 20px;
  margin-top: 20px;
}

.btn-primary {
  display: flex;
  align-items: center;
  gap: 10px;
}

.btn-arrow {
  transition: transform 0.3s ease;
}

.btn-primary:hover .btn-arrow {
  transform: translateX(5px);
}

.btn-secondary {
  padding: 16px 40px;
  border-radius: 50px;
  font-weight: 600;
  font-size: 1.1rem;
  text-decoration: none;
  color: var(--title);
  border: 2px solid var(--title);
  transition: all 0.3s cubic-bezier(0.68, -0.6, 0.32, 1.6);
}

.btn-secondary:hover {
  background: var(--title);
  color: white;
  transform: scale(1.05);
}

/* 右侧3D手机 */
.hero-visual {
  display: flex;
  justify-content: center;
  align-items: center;
  perspective: 1000px;
}

.phone-container {
  position: relative;
  width: 320px;
  height: 640px;
  animation: float 6s ease-in-out infinite;
}

.phone {
  width: 100%;
  height: 100%;
  position: relative;
  transition: transform 0.3s ease-out;
  transform-style: preserve-3d;
}

.phone-frame {
  width: 100%;
  height: 100%;
  background: linear-gradient(145deg, #2a2a2a 0%, #1a1a1a 100%);
  border-radius: 40px;
  padding: 12px;
  box-shadow: 
    0 50px 100px -20px rgba(0, 0, 0, 0.5),
    0 30px 60px -30px rgba(0, 0, 0, 0.3),
    inset 0 0 0 2px rgba(255, 255, 255, 0.1);
  position: relative;
}

.phone-screen {
  width: 100%;
  height: 100%;
  background: #0d1117;
  border-radius: 32px;
  overflow: hidden;
  position: relative;
}

.screen-content {
  padding: 40px 20px;
  height: 100%;
  overflow: hidden;
}

.code-preview {
  font-family: 'Fira Code', monospace;
  font-size: 0.8rem;
  line-height: 1.8;
}

.code-line {
  color: #e6edf3;
}

.code-line.indent {
  padding-left: 20px;
}

.code-line.indent2 {
  padding-left: 40px;
}

.code-keyword {
  color: #ff7b72;
}

.code-var {
  color: #79c0ff;
}

.code-type {
  color: #ffa657;
}

.code-string {
  color: #a5d6ff;
}

.code-component {
  color: #d2a8ff;
}

.code-prop {
  color: #7ee787;
}

.code-number {
  color: #79c0ff;
}

.phone-notch {
  position: absolute;
  top: 12px;
  left: 50%;
  transform: translateX(-50%);
  width: 120px;
  height: 28px;
  background: #1a1a1a;
  border-radius: 0 0 20px 20px;
}

.phone-reflection {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: linear-gradient(
    135deg,
    rgba(255, 255, 255, 0.1) 0%,
    transparent 40%,
    transparent 60%,
    rgba(255, 255, 255, 0.05) 100%
  );
  border-radius: 40px;
  pointer-events: none;
}

/* 悬浮卡片 */
.floating-card {
  position: absolute;
  background: white;
  padding: 12px 20px;
  border-radius: 12px;
  box-shadow: 0 10px 30px rgba(0, 0, 0, 0.15);
  display: flex;
  align-items: center;
  gap: 10px;
  font-size: 0.85rem;
  font-weight: 600;
  animation: float 4s ease-in-out infinite;
}

.card-icon {
  width: 32px;
  height: 32px;
  background: linear-gradient(135deg, #fe8301 0%, #ff9a2e 100%);
  border-radius: 8px;
  display: flex;
  align-items: center;
  justify-content: center;
  color: white;
  font-size: 0.75rem;
}

.card-1 {
  top: -30px;
  right: -40px;
  animation-delay: 0s;
}

.card-2 {
  bottom: 100px;
  left: -50px;
  animation-delay: 1s;
}

.card-3 {
  bottom: -20px;
  right: 20px;
  animation-delay: 2s;
}

/* 光晕 */
.glow-ring {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  width: 500px;
  height: 500px;
  border: 1px solid rgba(254, 131, 1, 0.2);
  border-radius: 50%;
  pointer-events: none;
  animation: pulse 4s ease-in-out infinite;
  z-index: -1;
}

.ring-2 {
  width: 600px;
  height: 600px;
  border-color: rgba(254, 131, 1, 0.1);
  animation-delay: 1s;
}

/* 滚动提示 */
.scroll-hint {
  position: absolute;
  bottom: 40px;
  left: 50%;
  transform: translateX(-50%);
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 10px;
  animation: fadeInUp 1s ease-out 1.5s forwards;
  opacity: 0;
}

.scroll-text {
  font-size: 0.85rem;
  color: var(--body);
  opacity: 0.6;
}

.scroll-arrow {
  width: 24px;
  height: 24px;
  border-right: 2px solid var(--primary);
  border-bottom: 2px solid var(--primary);
  transform: rotate(45deg);
  animation: bounce 2s ease-in-out infinite;
}

@keyframes bounce {
  0%, 100% { transform: rotate(45deg) translateY(0); }
  50% { transform: rotate(45deg) translateY(10px); }
}

@keyframes fadeInUp {
  from {
    opacity: 0;
    transform: translateX(-50%) translateY(20px);
  }
  to {
    opacity: 1;
    transform: translateX(-50%) translateY(0);
  }
}

/* 响应式 */
@media (max-width: 1024px) {
  .hero-container {
    grid-template-columns: 1fr;
    text-align: center;
    gap: 60px;
  }
  
  .hero-content {
    align-items: center;
  }
  
  .hero-stats {
    justify-content: center;
  }
  
  .phone-container {
    width: 260px;
    height: 520px;
  }
  
  .floating-card {
    display: none;
  }
}

@media (max-width: 768px) {
  .hero {
    padding: 100px 20px 60px;
  }
  
  .hero-cta {
    flex-direction: column;
    width: 100%;
  }
  
  .btn-primary, .btn-secondary {
    width: 100%;
    justify-content: center;
  }
}
</style>