<template>
  <div class="app">
    <!-- 动态背景 -->
    <DynamicBackground />
    
    <!-- 导航 -->
    <NavBar />
    
    <!-- 主内容 -->
    <main>
      <HeroSection />
      <ConceptCards />
      <CodeComparison />
      <CheatsheetSection />
      <CTASection />
    </main>
    
    <!-- 页脚 -->
    <FooterSection />
  </div>
</template>

<script setup lang="ts">
import DynamicBackground from './components/DynamicBackground.vue'
import NavBar from './components/NavBar.vue'
import HeroSection from './views/HeroSection.vue'
import ConceptCards from './views/ConceptCards.vue'
import CodeComparison from './views/CodeComparison.vue'
import CheatsheetSection from './views/CheatsheetSection.vue'
import CTASection from './views/CTASection.vue'
import FooterSection from './views/FooterSection.vue'
</script>

<style scoped>
.app {
  min-height: 100vh;
  position: relative;
}

main {
  position: relative;
  z-index: 1;
}
</style>