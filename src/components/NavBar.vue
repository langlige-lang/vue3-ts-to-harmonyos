<template>
  <nav class="navbar" :class="{ 'scrolled': isScrolled }">
    <div class="nav-container">
      <a href="#" class="logo">
        <span class="logo-icon">V→H</span>
        <span class="logo-text">Vue2Harmony</span>
      </a>
      
      <ul class="nav-links">
        <li><a href="#concepts" class="nav-link">概念对照</a></li>
        <li><a href="#code" class="nav-link">代码对比</a></li>
        <li><a href="#cheatsheet" class="nav-link">速查表</a></li>
      </ul>
      
      <a href="#start" class="nav-cta">开始学习</a>
    </div>
  </nav>
</template>

<script setup lang="ts">
import { ref, onMounted, onUnmounted } from 'vue'

const isScrolled = ref(false)

const handleScroll = () => {
  isScrolled.value = window.scrollY > 50
}

onMounted(() => {
  window.addEventListener('scroll', handleScroll)
})

onUnmounted(() => {
  window.removeEventListener('scroll', handleScroll)
})
</script>

<style scoped>
.navbar {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  z-index: 1000;
  padding: 20px 0;
  transition: all 0.4s cubic-bezier(0.19, 1, 0.22, 1);
}

.navbar.scrolled {
  padding: 12px 0;
  background: rgba(239, 239, 239, 0.9);
  backdrop-filter: blur(20px);
  -webkit-backdrop-filter: blur(20px);
  box-shadow: 0 4px 30px rgba(0, 0, 0, 0.1);
}

.nav-container {
  max-width: 1400px;
  margin: 0 auto;
  padding: 0 40px;
  display: flex;
  align-items: center;
  justify-content: space-between;
}

.logo {
  display: flex;
  align-items: center;
  gap: 12px;
  text-decoration: none;
}

.logo-icon {
  width: 44px;
  height: 44px;
  background: linear-gradient(135deg, #42b883 0%, #fe8301 100%);
  border-radius: 12px;
  display: flex;
  align-items: center;
  justify-content: center;
  color: white;
  font-weight: 700;
  font-size: 0.9rem;
  font-family: 'Poppins', sans-serif;
  animation: glow 3s ease-in-out infinite;
}

.logo-text {
  font-family: 'Poppins', sans-serif;
  font-weight: 700;
  font-size: 1.3rem;
  color: var(--title);
}

.nav-links {
  display: flex;
  gap: 40px;
  list-style: none;
}

.nav-link {
  text-decoration: none;
  color: var(--body);
  font-weight: 600;
  font-size: 0.95rem;
  position: relative;
  transition: color 0.3s ease;
}

.nav-link::after {
  content: '';
  position: absolute;
  bottom: -4px;
  left: 0;
  width: 0;
  height: 2px;
  background: var(--primary);
  transition: width 0.3s cubic-bezier(0.19, 1, 0.22, 1);
}

.nav-link:hover {
  color: var(--primary);
}

.nav-link:hover::after {
  width: 100%;
}

.nav-cta {
  background: var(--primary);
  color: white;
  padding: 10px 24px;
  border-radius: 25px;
  text-decoration: none;
  font-weight: 600;
  font-size: 0.9rem;
  transition: all 0.3s cubic-bezier(0.68, -0.6, 0.32, 1.6);
}

.nav-cta:hover {
  transform: scale(1.05);
  box-shadow: 0 10px 30px rgba(254, 131, 1, 0.4);
}

@media (max-width: 768px) {
  .nav-links {
    display: none;
  }
  
  .nav-container {
    padding: 0 20px;
  }
}
</style>