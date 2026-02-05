<template>
  <footer class="footer">
    <div class="footer-container">
      <!-- 顶部装饰线 -->
      <div class="footer-line"></div>
      
      <!-- 主要内容 -->
      <div class="footer-content">
        <!-- Logo区域 -->
        <div class="footer-brand">
          <a href="#" class="footer-logo">
            <span class="logo-icon">V→H</span>
            <span class="logo-text">Vue2Harmony</span>
          </a>
          <p class="footer-desc">
            为Vue3开发者打造的鸿蒙学习指南，<br>
            让技术转型更加顺畅。
          </p>
          <div class="footer-social">
            <a href="#" class="social-link" title="GitHub">
              <svg viewBox="0 0 24 24" fill="currentColor">
                <path d="M12 0c-6.626 0-12 5.373-12 12 0 5.302 3.438 9.8 8.207 11.387.599.111.793-.261.793-.577v-2.234c-3.338.726-4.033-1.416-4.033-1.416-.546-1.387-1.333-1.756-1.333-1.756-1.089-.745.083-.729.083-.729 1.205.084 1.839 1.237 1.839 1.237 1.07 1.834 2.807 1.304 3.492.997.107-.775.418-1.305.762-1.604-2.665-.305-5.467-1.334-5.467-5.931 0-1.311.469-2.381 1.236-3.221-.124-.303-.535-1.524.117-3.176 0 0 1.008-.322 3.301 1.23.957-.266 1.983-.399 3.003-.404 1.02.005 2.047.138 3.006.404 2.291-1.552 3.297-1.23 3.297-1.23.653 1.653.242 2.874.118 3.176.77.84 1.235 1.911 1.235 3.221 0 4.609-2.807 5.624-5.479 5.921.43.372.823 1.102.823 2.222v3.293c0 .319.192.694.801.576 4.765-1.589 8.199-6.086 8.199-11.386 0-6.627-5.373-12-12-12z"/>
              </svg>
            </a>
            <a href="#" class="social-link" title="Twitter">
              <svg viewBox="0 0 24 24" fill="currentColor">
                <path d="M23.953 4.57a10 10 0 01-2.825.775 4.958 4.958 0 002.163-2.723c-.951.555-2.005.959-3.127 1.184a4.92 4.92 0 00-8.384 4.482C7.69 8.095 4.067 6.13 1.64 3.162a4.822 4.822 0 00-.666 2.475c0 1.71.87 3.213 2.188 4.096a4.904 4.904 0 01-2.228-.616v.06a4.923 4.923 0 003.946 4.827 4.996 4.996 0 01-2.212.085 4.936 4.936 0 004.604 3.417 9.867 9.867 0 01-6.102 2.105c-.39 0-.779-.023-1.17-.067a13.995 13.995 0 007.557 2.209c9.053 0 13.998-7.496 13.998-13.985 0-.21 0-.42-.015-.63A9.935 9.935 0 0024 4.59z"/>
              </svg>
            </a>
            <a href="#" class="social-link" title="Discord">
              <svg viewBox="0 0 24 24" fill="currentColor">
                <path d="M20.317 4.3698a19.7913 19.7913 0 00-4.8851-1.5152.0741.0741 0 00-.0785.0371c-.211.3753-.4447.8648-.6083 1.2495-1.8447-.2762-3.68-.2762-5.4868 0-.1636-.3933-.4058-.8742-.6177-1.2495a.077.077 0 00-.0785-.037 19.7363 19.7363 0 00-4.8852 1.515.0699.0699 0 00-.0321.0277C.5334 9.0458-.319 13.5799.0992 18.0578a.0824.0824 0 00.0312.0561c2.0528 1.5076 4.0413 2.4228 5.9929 3.0294a.0777.0777 0 00.0842-.0276c.4616-.6304.8731-1.2952 1.226-1.9942a.076.076 0 00-.0416-.1057c-.6528-.2476-1.2743-.5495-1.8722-.8923a.077.077 0 01-.0076-.1277c.1258-.0943.2517-.1923.3718-.2914a.0743.0743 0 01.0776-.0105c3.9278 1.7933 8.18 1.7933 12.0614 0a.0739.0739 0 01.0785.0095c.1202.099.246.1981.3728.2924a.077.077 0 01-.0066.1276 12.2986 12.2986 0 01-1.873.8914.0766.0766 0 00-.0407.1067c.3604.698.7719 1.3628 1.225 1.9932a.076.076 0 00.0842.0286c1.961-.6067 3.9495-1.5219 6.0023-3.0294a.077.077 0 00.0313-.0552c.5004-5.177-.8382-9.6739-3.5485-13.6604a.061.061 0 00-.0312-.0286zM8.02 15.3312c-1.1825 0-2.1569-1.0857-2.1569-2.419 0-1.3332.9555-2.4189 2.157-2.4189 1.2108 0 2.1757 1.0952 2.1568 2.419 0 1.3332-.9555 2.4189-2.1569 2.4189zm7.9748 0c-1.1825 0-2.1569-1.0857-2.1569-2.419 0-1.3332.9554-2.4189 2.1569-2.4189 1.2108 0 2.1757 1.0952 2.1568 2.419 0 1.3332-.946 2.4189-2.1568 2.4189Z"/>
              </svg>
            </a>
          </div>
        </div>
        
        <!-- 链接区域 -->
        <div class="footer-links">
          <div class="link-group">
            <h4>学习资源</h4>
            <ul>
              <li><a href="#concepts">概念对照</a></li>
              <li><a href="#code">代码对比</a></li>
              <li><a href="#cheatsheet">速查表</a></li>
            </ul>
          </div>
          
          <div class="link-group">
            <h4>官方链接</h4>
            <ul>
              <li><a href="https://developer.harmonyos.com" target="_blank">鸿蒙开发者</a></li>
              <li><a href="https://vuejs.org" target="_blank">Vue.js</a></li>
              <li><a href="https://www.typescriptlang.org" target="_blank">TypeScript</a></li>
            </ul>
          </div>
          
          <div class="link-group">
            <h4>社区</h4>
            <ul>
              <li><a href="#">GitHub</a></li>
              <li><a href="#">讨论区</a></li>
              <li><a href="#">贡献指南</a></li>
            </ul>
          </div>
        </div>
      </div>
      
      <!-- 底部版权 -->
      <div class="footer-bottom">
        <p>© 2026 Vue2Harmony. Made with ❤️ for Vue developers.</p>
        <div class="tech-stack">
          <span class="tech-badge">Vue3</span>
          <span class="tech-badge">TypeScript</span>
          <span class="tech-badge">Vite</span>
        </div>
      </div>
    </div>
  </footer>
</template>

<style scoped>
.footer {
  padding: 80px 40px 40px;
  background: linear-gradient(180deg, transparent 0%, rgba(0,0,0,0.02) 100%);
}

.footer-container {
  max-width: 1200px;
  margin: 0 auto;
}

.footer-line {
  height: 1px;
  background: linear-gradient(90deg, transparent, rgba(254, 131, 1, 0.3), transparent);
  margin-bottom: 60px;
}

.footer-content {
  display: grid;
  grid-template-columns: 1fr 2fr;
  gap: 80px;
  margin-bottom: 60px;
}

/* Logo区域 */
.footer-brand {
  display: flex;
  flex-direction: column;
  gap: 20px;
}

.footer-logo {
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
}

.logo-text {
  font-family: 'Poppins', sans-serif;
  font-weight: 700;
  font-size: 1.3rem;
  color: var(--title);
}

.footer-desc {
  font-size: 0.95rem;
  color: var(--body);
  opacity: 0.8;
  line-height: 1.8;
}

.footer-social {
  display: flex;
  gap: 12px;
}

.social-link {
  width: 40px;
  height: 40px;
  background: rgba(0, 0, 0, 0.05);
  border-radius: 10px;
  display: flex;
  align-items: center;
  justify-content: center;
  color: var(--body);
  transition: all 0.3s ease;
}

.social-link:hover {
  background: var(--primary);
  color: white;
  transform: translateY(-3px);
}

.social-link svg {
  width: 20px;
  height: 20px;
}

/* 链接区域 */
.footer-links {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 40px;
}

.link-group h4 {
  font-size: 1rem;
  font-weight: 700;
  color: var(--title);
  margin-bottom: 20px;
}

.link-group ul {
  list-style: none;
  display: flex;
  flex-direction: column;
  gap: 12px;
}

.link-group a {
  color: var(--body);
  text-decoration: none;
  font-size: 0.9rem;
  opacity: 0.8;
  transition: all 0.3s ease;
  position: relative;
}

.link-group a::after {
  content: '';
  position: absolute;
  bottom: -2px;
  left: 0;
  width: 0;
  height: 2px;
  background: var(--primary);
  transition: width 0.3s ease;
}

.link-group a:hover {
  opacity: 1;
  color: var(--primary);
}

.link-group a:hover::after {
  width: 100%;
}

/* 底部版权 */
.footer-bottom {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding-top: 40px;
  border-top: 1px solid rgba(0, 0, 0, 0.05);
}

.footer-bottom p {
  font-size: 0.85rem;
  color: var(--body);
  opacity: 0.6;
}

.tech-stack {
  display: flex;
  gap: 8px;
}

.tech-badge {
  padding: 4px 12px;
  background: rgba(254, 131, 1, 0.1);
  border-radius: 20px;
  font-size: 0.75rem;
  font-weight: 600;
  color: var(--primary);
}

/* 响应式 */
@media (max-width: 768px) {
  .footer {
    padding: 60px 20px 30px;
  }
  
  .footer-content {
    grid-template-columns: 1fr;
    gap: 40px;
  }
  
  .footer-links {
    grid-template-columns: repeat(2, 1fr);
    gap: 30px;
  }
  
  .footer-bottom {
    flex-direction: column;
    gap: 20px;
    text-align: center;
  }
}
</style>