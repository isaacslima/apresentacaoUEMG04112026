<script setup lang="ts">
// Mapa ilustrativo: usuários pelo mundo acessando uma origem nos EUA,
// com ou sem edge locations (CDN) no caminho. Latências aproximadas.
const props = defineProps<{ cdn?: boolean }>()

const origin = { x: 95, y: 70 }
const users = [
  { name: 'São Paulo', x: 150, y: 200, edge: { x: 184, y: 196 }, ms: 120 },
  { name: 'Lisboa', x: 250, y: 45, edge: { x: 214, y: 52 }, ms: 90 },
  { name: 'Tóquio', x: 378, y: 125, edge: { x: 338, y: 140 }, ms: 170 },
]

const line = (a: { x: number, y: number }, b: { x: number, y: number }) => `M${a.x},${a.y} L${b.x},${b.y}`
</script>

<template>
  <svg viewBox="0 0 420 235" class="w-full cdn-map">
    <!-- "continentes" estilizados -->
    <ellipse cx="100" cy="80" rx="70" ry="45" class="land" />
    <ellipse cx="160" cy="185" rx="38" ry="45" class="land" />
    <ellipse cx="260" cy="70" rx="45" ry="40" class="land" />
    <ellipse cx="355" cy="110" rx="55" ry="50" class="land" />

    <!-- origem -->
    <g>
      <rect :x="origin.x - 13" :y="origin.y - 13" width="26" height="26" rx="5" class="origin" />
      <text :x="origin.x" :y="origin.y + 4" text-anchor="middle" class="origin-txt">S3</text>
      <text :x="origin.x" :y="origin.y - 22" text-anchor="middle" class="lbl">Origem (EUA)</text>
    </g>

    <g v-for="(u, i) in users" :key="u.name">
      <template v-if="!props.cdn">
        <path :id="`p-far-${i}`" :d="line(u, origin)" class="link far" />
        <circle r="4" class="packet slow">
          <animateMotion :dur="`${u.ms / 60}s`" repeatCount="indefinite">
            <mpath :href="`#p-far-${i}`" />
          </animateMotion>
        </circle>
      </template>
      <template v-else>
        <path :d="line(u.edge, origin)" class="link miss" />
        <path :id="`p-near-${i}`" :d="line(u, u.edge)" class="link near" />
        <circle r="4" class="packet fast">
          <animateMotion dur="0.5s" repeatCount="indefinite">
            <mpath :href="`#p-near-${i}`" />
          </animateMotion>
        </circle>
        <circle :cx="u.edge.x" :cy="u.edge.y" r="7" class="edge" />
      </template>

      <circle :cx="u.x" :cy="u.y" r="6" class="user" />
      <text :x="u.x" :y="u.y + 18" text-anchor="middle" class="lbl">{{ u.name }}</text>
      <text :x="u.x" :y="u.y - 12" text-anchor="middle" class="ms" :class="props.cdn ? 'good' : 'bad'">
        ~{{ props.cdn ? 15 : u.ms }} ms
      </text>
    </g>
  </svg>
</template>

<style scoped>
.land { fill: var(--card-bg); stroke: var(--card-border); }
.origin { fill: #3f8624; }
.origin-txt { font-size: 10px; font-weight: 700; fill: #fff; }
.user { fill: currentColor; opacity: 0.85; }
.edge { fill: #8c4fff; stroke: #fff; stroke-width: 2; }
.lbl { font-size: 9px; fill: currentColor; opacity: 0.75; }
.ms { font-size: 10px; font-weight: 700; font-family: 'Fira Code', monospace; }
.ms.bad { fill: #ef4444; }
.ms.good { fill: #10b981; }
.link { fill: none; stroke-width: 2; }
.link.far { stroke: #ef4444; stroke-dasharray: 6 5; opacity: 0.7; }
.link.near { stroke: #10b981; stroke-width: 3; }
.link.miss { stroke: currentColor; stroke-dasharray: 2 5; opacity: 0.25; }
.packet.slow { fill: #ef4444; }
.packet.fast { fill: #10b981; }
</style>
