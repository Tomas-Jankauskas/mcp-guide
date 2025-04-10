<script setup lang="ts">
import { ref, onMounted } from 'vue';
import MarkdownIt from 'markdown-it';
import hljs from 'highlight.js';
import 'highlight.js/styles/github.css';

const props = defineProps<{
  content: string;
}>();

const renderedContent = ref('');

onMounted(() => {
  const md = new MarkdownIt({
    html: true,
    linkify: true,
    typographer: true,
    highlight: function (str, lang) {
      if (lang && hljs.getLanguage(lang)) {
        try {
          return hljs.highlight(str, { language: lang }).value;
        } catch {
          // Silently handle highlighting errors
        }
      }
      return ''; // use external default escaping
    }
  });
  
  renderedContent.value = md.render(props.content);
});
</script>

<template>
  <div class="markdown-body" v-html="renderedContent"></div>
</template>

<style scoped>
.markdown-body {
  font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;
  line-height: 1.7;
  color: #24292e;
  padding: 2rem 0;
  width: 100%;
}

.markdown-body :deep(h1) {
  padding-bottom: 0.4em;
  font-size: 2.2em;
  border-bottom: 1px solid #eaecef;
  margin-top: 32px;
  margin-bottom: 20px;
  font-weight: 600;
  line-height: 1.25;
  letter-spacing: -0.5px;
}

.markdown-body :deep(h1:first-child) {
  margin-top: 0;
}

.markdown-body :deep(h2) {
  padding-bottom: 0.3em;
  font-size: 1.65em;
  border-bottom: 1px solid #eaecef;
  margin-top: 32px;
  margin-bottom: 20px;
  font-weight: 600;
  line-height: 1.25;
  letter-spacing: -0.3px;
}

.markdown-body :deep(h3) {
  font-size: 1.35em;
  margin-top: 28px;
  margin-bottom: 18px;
  font-weight: 600;
  line-height: 1.25;
}

.markdown-body :deep(p) {
  margin-top: 0;
  margin-bottom: 18px;
  font-size: 1.05em;
}

.markdown-body :deep(a) {
  color: #0366d6;
  text-decoration: none;
  transition: color 0.2s ease;
}

.markdown-body :deep(a:hover) {
  text-decoration: underline;
  color: #0078ff;
}

.markdown-body :deep(ul), 
.markdown-body :deep(ol) {
  padding-left: 2em;
  margin-top: 0;
  margin-bottom: 20px;
}

.markdown-body :deep(li) {
  margin-top: 0.35em;
  margin-bottom: 0.35em;
}

.markdown-body :deep(li p) {
  margin-top: 10px;
  margin-bottom: 10px;
}

.markdown-body :deep(pre) {
  padding: 18px;
  overflow: auto;
  font-size: 90%;
  line-height: 1.5;
  background-color: #f6f8fa;
  border-radius: 6px;
  margin-top: 0;
  margin-bottom: 20px;
}

.markdown-body :deep(code) {
  padding: 0.2em 0.4em;
  margin: 0;
  font-size: 90%;
  background-color: rgba(27, 31, 35, 0.05);
  border-radius: 4px;
  font-family: SFMono-Regular, Consolas, 'Liberation Mono', Menlo, monospace;
}

.markdown-body :deep(pre code) {
  padding: 0;
  margin: 0;
  background-color: transparent;
  border: 0;
  display: inline;
  overflow: visible;
  line-height: inherit;
  word-wrap: normal;
}

.markdown-body :deep(blockquote) {
  padding: 0 1.2em;
  color: #6a737d;
  border-left: 0.3em solid #dfe2e5;
  margin: 0 0 20px 0;
}

.markdown-body :deep(hr) {
  height: 1px;
  padding: 0;
  margin: 30px 0;
  background-color: #e1e4e8;
  border: 0;
}

.markdown-body :deep(table) {
  display: block;
  width: 100%;
  overflow: auto;
  margin-top: 0;
  margin-bottom: 20px;
  border-collapse: collapse;
  border-spacing: 0;
}

.markdown-body :deep(table th) {
  font-weight: 600;
  padding: 10px 16px;
  background-color: #f6f8fa;
  border: 1px solid #dfe2e5;
  text-align: left;
}

.markdown-body :deep(table td) {
  padding: 10px 16px;
  border: 1px solid #dfe2e5;
}

.markdown-body :deep(table tr:nth-child(2n)) {
  background-color: #f8f8f8;
}

@media (max-width: 768px) {
  .markdown-body {
    padding: 1.5rem 0;
  }
}
</style> 