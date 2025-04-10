<script setup lang="ts">
import { RouterView } from 'vue-router'
</script>

<template>
  <RouterView />
</template>

<style>
/* Global styles */
:root {
  --color-text: #24292e;
  --color-background: #f9f9f9;
  --color-primary: #0366d6;
}

body {
  margin: 0;
  padding: 0;
  font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;
  background-color: var(--color-background);
  color: var(--color-text);
}

* {
  box-sizing: border-box;
}
</style>
