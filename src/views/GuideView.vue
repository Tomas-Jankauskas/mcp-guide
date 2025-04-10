<script setup lang="ts">
import { ref } from 'vue';
import MarkdownRenderer from '@/components/MarkdownRenderer.vue';
import guideContent from '@/assets/mcp-guide.md?raw';

const markdownContent = ref(guideContent);
</script>

<template>
  <div class="guide-container">
    <div class="header-wrapper">
      <header class="header">
        <div class="header-content">
          <h1>MCP Setup Guide</h1>
          <p>A comprehensive guide to set up Model Context Protocol in Cursor</p>
        </div>
      </header>
    </div>
    <main class="content-wrapper">
      <div class="content">
        <MarkdownRenderer :content="markdownContent" />
      </div>
    </main>
    <footer>
      <div class="footer-content">
        <p>Model Context Protocol (MCP) Documentation - Designed with Vue.js</p>
      </div>
    </footer>
  </div>
</template>

<style scoped>
.guide-container {
  display: flex;
  flex-direction: column;
  min-height: 100vh;
  width: 100vw;
}

.header-wrapper {
  background-color: var(--color-header-bg);
  width: 100%;
  padding: 3rem 0;
}

.header {
  width: 100%;
  max-width: 1200px;
  margin: 0 auto;
  color: var(--color-header-text);
}

.header-content {
  width: 100%;
  padding: 0 2rem;
}

.header h1 {
  font-size: 3rem;
  margin: 0;
  font-weight: 700;
  letter-spacing: -0.5px;
}

.header p {
  margin-top: 0.8rem;
  font-size: 1.4rem;
  opacity: 0.85;
  max-width: 700px;
  line-height: 1.5;
}

.content-wrapper {
  flex: 1;
  background-color: var(--color-background);
  padding: 3rem 0;
  width: 100%;
}

.content {
  width: 100%;
  max-width: 1200px;
  margin: 0 auto;
  background-color: var(--vt-c-white);
  border-radius: 8px;
  box-shadow: 0 8px 30px rgba(0, 0, 0, 0.07);
  overflow: hidden;
  padding: 2rem;
}

footer {
  background-color: var(--color-footer-bg);
  padding: 2rem 0;
  text-align: center;
  color: var(--color-footer-text);
  font-size: 1rem;
  border-top: 1px solid var(--color-border);
  width: 100%;
}

.footer-content {
  width: 100%;
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 2rem;
}

@media (max-width: 768px) {
  .header-wrapper {
    padding: 2rem 0;
  }
  
  .header-content {
    padding: 0 1.5rem;
  }
  
  .header h1 {
    font-size: 2.5rem;
  }
  
  .header p {
    font-size: 1.2rem;
  }
  
  .content-wrapper {
    padding: 1.5rem 0;
  }
  
  .content {
    border-radius: 0;
    box-shadow: none;
    padding: 1.5rem;
  }
  
  .footer-content {
    padding: 0 1.5rem;
  }
}
</style> 