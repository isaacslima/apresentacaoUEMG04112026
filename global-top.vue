<script setup lang="ts">
import { useDarkMode } from '@slidev/client'

const { isDark, toggleDark } = useDarkMode()
</script>

<template>
  <button
    class="theme-toggle"
    :title="isDark ? 'Mudar para tema claro' : 'Mudar para tema escuro'"
    @click="toggleDark()"
  >
    <carbon-sun v-if="isDark" />
    <carbon-moon v-else />
  </button>
</template>

<style scoped>
.theme-toggle {
  position: absolute;
  top: 14px;
  right: 14px;
  z-index: 100;
  display: flex;
  align-items: center;
  justify-content: center;
  width: 36px;
  height: 36px;
  border-radius: 9999px;
  font-size: 18px;
  color: var(--aws-orange);
  background: var(--card-bg);
  border: 1px solid var(--card-border);
  cursor: pointer;
  transition: transform 0.3s ease;
}
.theme-toggle:hover {
  transform: rotate(30deg) scale(1.1);
}
@media print {
  .theme-toggle { display: none; }
}
</style>
