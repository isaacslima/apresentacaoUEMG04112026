<script lang="ts">
// evita registrar o listener mais de uma vez caso o layer seja montado em paralelo
let clickNavRegistered = false
</script>

<script setup lang="ts">
import { onMounted, onUnmounted } from 'vue'
import { useDarkMode, useDrawings, useNav } from '@slidev/client'

const { isDark, toggleDark } = useDarkMode()
const { next, prev, isPresenter, isPrintMode, isEmbedded } = useNav()
const { drawingEnabled } = useDrawings()

// elementos que têm comportamento próprio ao clicar
const INTERACTIVE = 'a, button, input, textarea, select, label, [role="button"], [contenteditable], .incoming-call'

// clique esquerdo no slide avança, clique direito volta
function onSlideClick(e: MouseEvent) {
  if (isPresenter.value || isPrintMode.value || isEmbedded.value || drawingEnabled.value)
    return
  const target = e.target as HTMLElement | null
  if (!target?.closest('.slidev-page') || target.closest(INTERACTIVE))
    return
  if (window.getSelection()?.toString())
    return

  if (e.type === 'contextmenu') {
    e.preventDefault()
    prev()
  }
  else if (e.button === 0) {
    next()
  }
}

let owner = false
onMounted(() => {
  if (clickNavRegistered)
    return
  clickNavRegistered = owner = true
  document.addEventListener('click', onSlideClick)
  document.addEventListener('contextmenu', onSlideClick)
})
onUnmounted(() => {
  if (!owner)
    return
  clickNavRegistered = owner = false
  document.removeEventListener('click', onSlideClick)
  document.removeEventListener('contextmenu', onSlideClick)
})
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
