<script setup lang="ts">
// Cabeçalho padrão de cada serviço: ícone oficial animado + nome + slogan
defineProps<{
  icon: string
  name: string
  full: string
  tagline: string
}>()
</script>

<template>
  <div class="flex items-center gap-6 mb-6">
    <div
      v-motion
      :initial="{ scale: 0, rotate: -90, opacity: 0 }"
      :enter="{ scale: 1, rotate: 0, opacity: 1, transition: { type: 'spring', stiffness: 180, damping: 14 } }"
      class="aws-icon-wrap"
    >
      <AwsIcon :name="icon" class="text-7xl" />
    </div>
    <div
      v-motion
      :initial="{ x: 60, opacity: 0 }"
      :enter="{ x: 0, opacity: 1, transition: { delay: 200 } }"
    >
      <h1 class="!mb-0 !text-4xl">{{ name }}</h1>
      <div class="text-sm opacity-60 font-mono">{{ full }}</div>
      <div class="text-lg mt-1 text-aws">{{ tagline }}</div>
    </div>
  </div>
</template>
