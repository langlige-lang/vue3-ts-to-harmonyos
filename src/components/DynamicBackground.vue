<template>
  <div class="dynamic-bg">
    <!-- 渐变层 -->
    <div class="gradient-layer"></div>
    
    <!-- 粒子画布 -->
    <canvas ref="particleCanvas" class="particle-canvas"></canvas>
    
    <!-- 浮动代码符号 -->
    <div class="floating-symbols">
      <span v-for="(symbol, index) in symbols" :key="index" 
            class="symbol"
            :style="getSymbolStyle(index)">
        {{ symbol }}
      </span>
    </div>
    
    <!-- 网格线 -->
    <div class="grid-lines"></div>
  </div>
</template>

<script setup lang="ts">
import { ref, onMounted, onUnmounted } from 'vue'

const particleCanvas = ref<HTMLCanvasElement | null>(null)
const symbols = ['{ }', '< />', '( )', '[ ]', ';', '//', '@', '#', '*', '=>']

const getSymbolStyle = (index: number) => {
  const left = Math.random() * 100
  const top = Math.random() * 100
  const delay = Math.random() * 5
  const duration = 10 + Math.random() * 10
  const opacity = 0.03 + Math.random() * 0.05
  
  return {
    left: `${left}%`,
    top: `${top}%`,
    animationDelay: `${delay}s`,
    animationDuration: `${duration}s`,
    opacity,
    fontSize: `${14 + Math.random() * 20}px`
  }
}

// 粒子系统
class ParticleSystem {
  canvas: HTMLCanvasElement
  ctx: CanvasRenderingContext2D
  particles: Array<{
    x: number
    y: number
    vx: number
    vy: number
    radius: number
    opacity: number
  }>
  animationId: number

  constructor(canvas: HTMLCanvasElement) {
    this.canvas = canvas
    this.ctx = canvas.getContext('2d')!
    this.particles = []
    this.animationId = 0
    this.resize()
    this.init()
  }

  resize() {
    this.canvas.width = window.innerWidth
    this.canvas.height = window.innerHeight
  }

  init() {
    const particleCount = Math.min(30, Math.floor(window.innerWidth / 50))
    for (let i = 0; i < particleCount; i++) {
      this.particles.push({
        x: Math.random() * this.canvas.width,
        y: Math.random() * this.canvas.height,
        vx: (Math.random() - 0.5) * 0.3,
        vy: (Math.random() - 0.5) * 0.3,
        radius: Math.random() * 2 + 1,
        opacity: Math.random() * 0.3 + 0.1
      })
    }
  }

  draw() {
    this.ctx.clearRect(0, 0, this.canvas.width, this.canvas.height)
    
    // 绘制粒子
    this.particles.forEach((p, i) => {
      // 更新位置
      p.x += p.vx
      p.y += p.vy
      
      // 边界检测
      if (p.x < 0 || p.x > this.canvas.width) p.vx *= -1
      if (p.y < 0 || p.y > this.canvas.height) p.vy *= -1
      
      // 绘制粒子
      this.ctx.beginPath()
      this.ctx.arc(p.x, p.y, p.radius, 0, Math.PI * 2)
      this.ctx.fillStyle = `rgba(254, 131, 1, ${p.opacity})`
      this.ctx.fill()
      
      // 绘制连线
      this.particles.slice(i + 1).forEach((p2) => {
        const dx = p.x - p2.x
        const dy = p.y - p2.y
        const dist = Math.sqrt(dx * dx + dy * dy)
        
        if (dist < 150) {
          this.ctx.beginPath()
          this.ctx.moveTo(p.x, p.y)
          this.ctx.lineTo(p2.x, p2.y)
          this.ctx.strokeStyle = `rgba(254, 131, 1, ${0.1 * (1 - dist / 150)})`
          this.ctx.lineWidth = 0.5
          this.ctx.stroke()
        }
      })
    })
    
    this.animationId = requestAnimationFrame(() => this.draw())
  }

  destroy() {
    cancelAnimationFrame(this.animationId)
  }
}

let particleSystem: ParticleSystem | null = null

onMounted(() => {
  if (particleCanvas.value) {
    particleSystem = new ParticleSystem(particleCanvas.value)
    particleSystem.draw()
  }
  
  window.addEventListener('resize', handleResize)
})

onUnmounted(() => {
  particleSystem?.destroy()
  window.removeEventListener('resize', handleResize)
})

const handleResize = () => {
  particleSystem?.resize()
}
</script>

<style scoped>
.dynamic-bg {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  z-index: 0;
  overflow: hidden;
  pointer-events: none;
}

.gradient-layer {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: 
    radial-gradient(ellipse at 20% 20%, rgba(254, 131, 1, 0.08) 0%, transparent 50%),
    radial-gradient(ellipse at 80% 80%, rgba(254, 131, 1, 0.05) 0%, transparent 50%),
    radial-gradient(ellipse at 50% 50%, rgba(255, 255, 255, 0.5) 0%, transparent 70%);
  animation: gradientPulse 15s ease-in-out infinite;
}

@keyframes gradientPulse {
  0%, 100% {
    transform: scale(1);
    opacity: 1;
  }
  50% {
    transform: scale(1.1);
    opacity: 0.8;
  }
}

.particle-canvas {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
}

.floating-symbols {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  pointer-events: none;
}

.symbol {
  position: absolute;
  font-family: 'Fira Code', monospace;
  color: #fe8301;
  animation: floatSymbol linear infinite;
  pointer-events: none;
}

@keyframes floatSymbol {
  0% {
    transform: translateY(0) rotate(0deg);
  }
  50% {
    transform: translateY(-30px) rotate(5deg);
  }
  100% {
    transform: translateY(0) rotate(0deg);
  }
}

.grid-lines {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-image: 
    linear-gradient(rgba(254, 131, 1, 0.03) 1px, transparent 1px),
    linear-gradient(90deg, rgba(254, 131, 1, 0.03) 1px, transparent 1px);
  background-size: 50px 50px;
}
</style>