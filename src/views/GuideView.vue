<script setup lang="ts">
import { ref } from 'vue';
import MarkdownRenderer from '@/components/MarkdownRenderer.vue';
import guideContent from '@/assets/mcp-guide.md?raw';

const markdownContent = ref(guideContent);
</script>

<template>
  <div class="guide-container">
    <header class="header">
      <div class="header-content">
        <h1>MCP Setup Guide</h1>
        <p>A comprehensive guide to set up Model Context Protocol in Cursor</p>
      </div>
    </header>
    <main>
      <MarkdownRenderer :content="markdownContent" />
    </main>
    <footer>
      <p>Model Context Protocol (MCP) Documentation - Designed with Vue.js</p>
    </footer>
  </div>
</template>

<style scoped>
.guide-container {
  display: flex;
  flex-direction: column;
  min-height: 100vh;
}

.header {
  background-color: #1a1a1a;
  color: white;
  padding: 2rem 1rem;
}

.header-content {
  max-width: 900px;
  margin: 0 auto;
}

.header h1 {
  font-size: 2.5rem;
  margin: 0;
  font-weight: 700;
}

.header p {
  margin-top: 0.5rem;
  font-size: 1.2rem;
  opacity: 0.8;
}

main {
  flex: 1;
  background-color: #fff;
  padding: 1rem;
}

footer {
  background-color: #f6f8fa;
  padding: 1.5rem;
  text-align: center;
  color: #586069;
  font-size: 0.9rem;
}
</style> 