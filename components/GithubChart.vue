<script setup lang="ts">
import { ref } from 'vue'

// Tenta o gráfico ao vivo; sem internet, cai para a cópia salva em public/
const props = defineProps<{ user: string }>()
const src = ref(`https://ghchart.rshah.org/FF9900/${props.user}`)
</script>

<template>
  <div class="contrib-card">
    <div class="text-xs opacity-60 mb-1 flex items-center gap-1">
      <carbon-logo-github /> contribuições no último ano
    </div>
    <img :src="src" alt="Gráfico de contribuições do GitHub" class="w-full" @error="src = '/github-contrib.svg'">
  </div>
</template>

<style scoped>
.contrib-card {
  padding: 10px 14px;
  border-radius: 12px;
  background: #fff;
  color: #232f3e;
  border: 1px solid var(--card-border);
}
</style>
