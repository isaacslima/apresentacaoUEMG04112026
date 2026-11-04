<script setup lang="ts">
import { useIsSlideActive, useSlideContext } from '@slidev/client'
import { computed, onBeforeUnmount, ref, watch } from 'vue'

// Toca um toque de chamada quando o slide chega no clique `at`.
// Usa public/ligacao.mp3 se existir; senão gera o toque no navegador (Web Audio).
const props = withDefaults(defineProps<{ at: number, seconds?: number, label?: string }>(), {
  seconds: 10,
  label: 'Chamada recebida',
})

const { $clicks, $renderContext } = useSlideContext()
const isActive = useIsSlideActive()
const ringing = ref(false)

// Só a janela principal toca (não o modo apresentador nem a exportação)
const canPlay = computed(() => $renderContext.value === 'slide' && isActive.value)

let audio: HTMLAudioElement | undefined
let ctx: AudioContext | undefined
let timers: number[] = []

function note(freq: number, start: number, dur: number) {
  const osc = ctx!.createOscillator()
  const gain = ctx!.createGain()
  osc.type = 'triangle'
  osc.frequency.value = freq
  gain.gain.setValueAtTime(0.0001, start)
  gain.gain.exponentialRampToValueAtTime(0.25, start + 0.02)
  gain.gain.exponentialRampToValueAtTime(0.0001, start + dur)
  osc.connect(gain).connect(ctx!.destination)
  osc.start(start)
  osc.stop(start + dur)
}

function synthRing() {
  ctx = new AudioContext()
  ctx.resume()
  // frase curta de 4 notas, repetida a cada 2 s
  const phrase = [659.25, 783.99, 987.77, 783.99]
  for (let t = 0; t < props.seconds; t += 2) {
    phrase.forEach((f, i) => note(f, ctx!.currentTime + t + i * 0.18, 0.35))
  }
}

function start() {
  stop()
  ringing.value = true
  audio = new Audio('/ligacao.mp3')
  audio.loop = true
  audio.play().catch(() => {
    audio = undefined
    synthRing()
  })
  timers.push(window.setTimeout(stop, props.seconds * 1000))
}

function stop() {
  ringing.value = false
  timers.forEach(clearTimeout)
  timers = []
  audio?.pause()
  audio = undefined
  ctx?.close()
  ctx = undefined
}

watch([$clicks, canPlay], ([clicks, ok], [prevClicks]) => {
  if (ok && clicks === props.at && prevClicks !== props.at)
    start()
  else if (!ok || clicks !== props.at)
    stop()
})

onBeforeUnmount(stop)
</script>

<template>
  <Transition name="call">
    <div v-if="ringing" class="incoming-call" @click="stop">
      <div class="call-icon"><carbon-phone-incoming /></div>
      <div>
        <div class="font-bold text-sm">{{ label }}</div>
        <div class="text-xs op-70">clique para silenciar</div>
      </div>
    </div>
  </Transition>
</template>

<style scoped>
.incoming-call {
  position: absolute;
  right: 70px;
  top: 16px;
  z-index: 50;
  display: flex;
  align-items: center;
  gap: 10px;
  padding: 8px 14px;
  border-radius: 12px;
  background: #4b53bc;
  color: #fff;
  box-shadow: 0 10px 30px rgba(75, 83, 188, 0.5);
  cursor: pointer;
}
.call-icon {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 32px;
  height: 32px;
  border-radius: 9999px;
  background: #16a34a;
  font-size: 18px;
  animation: ring 0.5s ease-in-out infinite;
}
@keyframes ring {
  0%, 100% { transform: rotate(0deg); }
  25% { transform: rotate(-15deg); }
  75% { transform: rotate(15deg); }
}
.call-enter-active, .call-leave-active { transition: all 0.3s ease; }
.call-enter-from, .call-leave-to { opacity: 0; transform: translateY(-20px); }
</style>
