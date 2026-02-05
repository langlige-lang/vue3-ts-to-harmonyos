<template>
  <section class="cta-section" id="start">
    <div class="cta-container">
      <!-- 背景效果 -->
      <div class="cta-bg">
        <div class="gradient-orb orb-1"></div>
        <div class="gradient-orb orb-2"></div>
        <div class="gradient-orb orb-3"></div>
      </div>
      
      <!-- 内容 -->
      <div class="cta-content">
        <h2 class="cta-title">
          <span class="title-word" v-for="(word, index) in titleWords" :key="index"
                :style="{ animationDelay: `${index * 0.1}s` }">
            {{ word }}
          </span>
        </h2>
        
        <p class="cta-subtitle">
          从今天开始，开启你的鸿蒙开发之旅
        </p>
        
        <div class="cta-buttons">
          <a href="#concepts" class="cta-btn primary magnetic-btn" ref="primaryBtn"
             @mousemove="handleMagneticMove" @mouseleave="handleMagneticLeave">
            <span class="btn-text">开始学习</span>
            <span class="btn-shine"></span>
            <span class="btn-icon">🚀</span>
          </a>
          
          <a href="https://developer.harmonyos.com" target="_blank" class="cta-btn secondary">
            <span class="btn-text">官方文档</span>
            <span class="btn-icon">📖</span>
          </a>
        </div>
        
        <!-- 学习路径 -->
        <div class="learning-path">
          <div class="path-item" v-for="(step, index) in learningSteps" :key="index"
               :style="{ animationDelay: `${0.5 + index * 0.15}s` }">
            <div class="path-number">{{ index + 1 }}</div>
            <div class="path-content">
              <h4>{{ step.title }}</h4>
              <p>{{ step.desc }}</p>
            </div>
            <div class="path-arrow" v-if="index < learningSteps.length - 1">→</div>
          </div>
        </div>
      </div>
      
      <!-- 装饰元素 -->
      <div class="floating-shapes">
        <span v-for="n in 6" :key="n" class="shape" :class="`shape-${n}`"></span>
      </div>
    </div>
  </section>
</template>

<script setup lang="ts">
import { ref } from 'vue'

const titleWords = ['准备', '开始', '了', '吗', '?']
const primaryBtn = ref<HTMLElement | null>(null)

const learningSteps = [
  { title: '熟悉语法', desc: '了解.ets文件结构' },
  { title: '掌握状态', desc: '学习@State装饰器' },
  { title: '练习布局', desc: 'Column/Row/Flex' },
  { title: '实战项目', desc: '完成TodoList' }
]

const handleMagneticMove = (e: MouseEvent) => {
  if (!primaryBtn.value) return
  
  const rect = primaryBtn.value.getBoundingClientRect()
  const x = e.clientX - rect.left - rect.width / 2
  const y = e.clientY - rect.top - rect.height / 2
  
  primaryBtn.value.style.transform = `translate(${x * 0.3}px, ${y * 0.3}px) scale(1.05)`
}

const handleMagneticLeave = () => {
  if (!primaryBtn.value) return
  primaryBtn.value.style.transform = ''
}
</script>

<style scoped>
.cta-section {
  padding: 120px 40px;
  position: relative;
  overflow: hidden;
}

.cta-container {
  max-width: 1000px;
  margin: 0 auto;
  position: relative;
  background: linear-gradient(145deg, #1a1a2e 0%, #16213e 100%);
  border-radius: 40px;
  padding: 80px 60px;
  overflow: hidden;
}

/* 背景效果 */
.cta-bg {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  overflow: hidden;
  pointer-events: none;
}

.gradient-orb {
  position: absolute;
  border-radius: 50%;
  filter: blur(80px);
  opacity: 0.5;
  animation: float 10s ease-in-out infinite;
}

.orb-1 {
  width: 400px;
  height: 400px;
  background: linear-gradient(135deg, #fe8301 0%, #ff6b00 100%);
  top: -100px;
  right: -100px;
  animation-delay: 0s;
}

.orb-2 {
  width: 300px;
  height: 300px;
  background: linear-gradient(135deg, #42b883 0%, #35495e 100%);
  bottom: -50px;
  left: -50px;
  animation-delay: 3s;
}

.orb-3 {
  width: 200px;
  height: 200px;
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  animation-delay: 6s;
}

/* 内容 */
.cta-content {
  position: relative;
  z-index: 1;
  text-align: center;
}

.cta-title {
  font-size: clamp(2.5rem, 6vw, 4rem);
  font-weight: 800;
  margin-bottom: 20px;
  display: flex;
  justify-content: center;
  flex-wrap: wrap;
  gap: 8px;
}

.title-word {
  display: inline-block;
  background: linear-gradient(135deg, #fff 0%, #fe8301 100%);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
  animation: flipIn 0.8s cubic-bezier(0.19, 1, 0.22, 1) forwards;
  opacity: 0;
}

.cta-subtitle {
  font-size: 1.2rem;
  color: rgba(255, 255, 255, 0.7);
  margin-bottom: 40px;
  animation: fadeInUp 0.8s ease-out 0.4s forwards;
  opacity: 0;
}

/* 按钮 */
.cta-buttons {
  display: flex;
  justify-content: center;
  gap: 20px;
  margin-bottom: 60px;
  flex-wrap: wrap;
  animation: fadeInUp 0.8s ease-out 0.5s forwards;
  opacity: 0;
}

.cta-btn {
  position: relative;
  display: flex;
  align-items: center;
  gap: 12px;
  padding: 18px 40px;
  border-radius: 50px;
  font-size: 1.1rem;
  font-weight: 600;
  text-decoration: none;
  overflow: hidden;
  transition: all 0.4s cubic-bezier(0.68, -0.6, 0.32, 1.6);
}

.cta-btn.primary {
  background: linear-gradient(135deg, #fe8301 0%, #ff6b00 100%);
  color: white;
  box-shadow: 0 10px 40px rgba(254, 131, 1, 0.4);
}

.cta-btn.primary:hover {
  box-shadow: 0 15px 50px rgba(254, 131, 1, 0.5);
}

.btn-shine {
  position: absolute;
  top: 0;
  left: -100%;
  width: 100%;
  height: 100%;
  background: linear-gradient(
    90deg,
    transparent,
    rgba(255, 255, 255, 0.3),
    transparent
  );
  transition: left 0.5s ease;
}

.cta-btn.primary:hover .btn-shine {
  left: 100%;
}

.cta-btn.secondary {
  background: rgba(255, 255, 255, 0.1);
  color: white;
  border: 2px solid rgba(255, 255, 255, 0.2);
  backdrop-filter: blur(10px);
}

.cta-btn.secondary:hover {
  background: rgba(255, 255, 255, 0.2);
  border-color: rgba(255, 255, 255, 0.4);
  transform: scale(1.05);
}

.btn-icon {
  font-size: 1.3rem;
}

/* 学习路径 */
.learning-path {
  display: flex;
  justify-content: center;
  align-items: flex-start;
  gap: 20px;
  flex-wrap: wrap;
}

.path-item {
  display: flex;
  align-items: center;
  gap: 12px;
  animation: slideInUp 0.6s ease-out forwards;
  opacity: 0;
}

.path-number {
  width: 40px;
  height: 40px;
  background: rgba(254, 131, 1, 0.2);
  border: 2px solid #fe8301;
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  font-weight: 700;
  color: #fe8301;
  font-size: 1rem;
}

.path-content {
  text-align: left;
}

.path-content h4 {
  color: white;
  font-size: 0.95rem;
  font-weight: 600;
  margin-bottom: 4px;
}

.path-content p {
  color: rgba(255, 255, 255, 0.6);
  font-size: 0.8rem;
}

.path-arrow {
  color: #fe8301;
  font-size: 1.5rem;
  font-weight: bold;
  animation: bounce 1s ease-in-out infinite;
}

/* 浮动形状 */
.floating-shapes {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  pointer-events: none;
  overflow: hidden;
}

.shape {
  position: absolute;
  opacity: 0.1;
  animation: float 8s ease-in-out infinite;
}

.shape-1 {
  width: 60px;
  height: 60px;
  border: 3px solid #fe8301;
  border-radius: 12px;
  top: 20%;
  left: 10%;
  animation-delay: 0s;
}

.shape-2 {
  width: 40px;
  height: 40px;
  background: #42b883;
  border-radius: 50%;
  top: 60%;
  right: 15%;
  animation-delay: 2s;
}

.shape-3 {
  width: 80px;
  height: 4px;
  background: linear-gradient(90deg, #fe8301, transparent);
  top: 30%;
  right: 20%;
  animation-delay: 4s;
}

.shape-4 {
  width: 30px;
  height: 30px;
  border: 2px solid #667eea;
  transform: rotate(45deg);
  bottom: 20%;
  left: 15%;
  animation-delay: 1s;
}

.shape-5 {
  width: 50px;
  height: 50px;
  border-radius: 50%;
  border: 2px dashed #fe8301;
  top: 70%;
  left: 25%;
  animation: rotate 20s linear infinite;
}

.shape-6 {
  width: 20px;
  height: 20px;
  background: #ff6b6b;
  clip-path: polygon(50% 0%, 100% 50%, 50% 100%, 0% 50%);
  top: 15%;
  right: 30%;
  animation-delay: 3s;
}

/* 响应式 */
@media (max-width: 768px) {
  .cta-section {
    padding: 80px 20px;
  }
  
  .cta-container {
    padding: 50px 30px;
  }
  
  .learning-path {
    flex-direction: column;
    align-items: center;
  }
  
  .path-arrow {
    display: none;
  }
  
  .path-item {
    width: 100%;
    max-width: 250px;
  }
}
</style>