<script setup lang="ts">
// Mock de um dashboard do CloudWatch durante o incidente do pedido 4821,
// no cenário COM logs estruturados e alarmes. Dados ilustrativos.

// Erros de pagamento por minuto, das 19:30 às 20:10 (total no incidente = 52)
const incident = [2, 4, 5, 4, 4, 3, 4, 3, 4, 3, 3, 3, 3, 3, 2, 2]
const errors = Array.from({ length: 41 }, (_, i) => (i >= 12 && i < 12 + incident.length ? incident[i - 12] : i % 9 === 0 ? 1 : 0))

const W = 400
const H = 120
const pad = { l: 22, r: 8, t: 10, b: 18 }
const maxY = 6
const x = (i: number) => pad.l + (i / (errors.length - 1)) * (W - pad.l - pad.r)
const y = (v: number) => pad.t + (1 - v / maxY) * (H - pad.t - pad.b)
const linePath = errors.map((v, i) => `${i ? 'L' : 'M'}${x(i).toFixed(1)},${y(v).toFixed(1)}`).join(' ')
const areaPath = `${linePath} L${x(errors.length - 1)},${y(0)} L${x(0)},${y(0)} Z`
const minute = (m: number) => x(m - 30)  // m = minutos depois das 19:00

const marks = [
  { at: 44, label: '🔔 alarme', cls: 'mk-alarm' },
  { at: 50, label: '📣 cupom', cls: 'mk-mkt' },
  { at: 58, label: '✅ correção', cls: 'mk-fix' },
]

const byClass = [
  { name: 'PagamentoService', v: 52 },
  { name: 'EstoqueService', v: 3 },
  { name: 'FreteService', v: 1 },
]
</script>

<template>
  <div class="cw">
    <div class="cw-header">
      <div class="flex items-center gap-2 font-bold"><AwsIcon name="cloudwatch" /> loja-prod · Dashboard</div>
      <div class="flex items-center gap-2">
        <span class="pill">⏱ 19:30 – 20:10</span>
        <span class="pill">↻ 1 min</span>
      </div>
    </div>

    <!-- KPIs -->
    <div v-click class="grid grid-cols-4 gap-2">
      <div class="widget">
        <div class="w-title">Pedidos / min</div>
        <div class="kpi">31 <span class="delta bad">▼ 23%</span></div>
      </div>
      <div class="widget">
        <div class="w-title">Erro em pagamentos</div>
        <div class="kpi">11% <span class="status critical">⛔ ALARME</span></div>
      </div>
      <div class="widget">
        <div class="w-title">Latência p95 · gateway</div>
        <div class="kpi">5.000 ms <span class="status critical">⛔ timeout</span></div>
      </div>
      <div class="widget">
        <div class="w-title">CPU · tasks ECS</div>
        <div class="kpi">42% <span class="status good">✔ OK</span></div>
      </div>
    </div>

    <div class="grid grid-cols-[1.7fr_1fr] gap-2 mt-2">
      <!-- linha do tempo de erros -->
      <div v-click class="widget">
        <div class="w-title">Erros de pagamento por minuto</div>
        <svg :viewBox="`0 0 ${W} ${H}`" class="w-full">
          <line v-for="v in [0, 3, 6]" :key="v" :x1="pad.l" :x2="W - pad.r" :y1="y(v)" :y2="y(v)" class="grid-line" />
          <text v-for="v in [0, 3, 6]" :key="`t${v}`" :x="pad.l - 4" :y="y(v) + 3" text-anchor="end" class="axis">{{ v }}</text>
          <text v-for="m in [30, 45, 60]" :key="m" :x="minute(m)" :y="H - 4" text-anchor="middle" class="axis">{{ m === 60 ? '20:00' : `19:${m}` }}</text>
          <path :d="areaPath" class="area" />
          <path :d="linePath" class="line" />
          <g v-for="(m, i) in marks" :key="m.label" :class="m.cls">
            <line :x1="minute(m.at)" :x2="minute(m.at)" :y1="pad.t" :y2="y(0)" class="mk-line" />
            <text :x="minute(m.at) + 3" :y="pad.t + 8 + i * 11" class="mk-text">{{ m.label }}</text>
          </g>
        </svg>
      </div>

      <!-- erros por classe -->
      <div v-click class="widget">
        <div class="w-title">Erros por classe (Logs Insights)</div>
        <div class="flex flex-col gap-2 mt-2">
          <div v-for="c in byClass" :key="c.name" class="bar-row" :title="`${c.name}: ${c.v} erros`">
            <div class="flex justify-between text-[0.6rem]"><span class="font-mono">{{ c.name }}</span><b>{{ c.v }}</b></div>
            <div class="bar-track"><div class="bar-fill" :style="{ width: `${(c.v / 52) * 100}%` }" /></div>
          </div>
        </div>
      </div>
    </div>

    <div class="grid grid-cols-[1.25fr_0.8fr_1.15fr] gap-2 mt-2">
      <!-- últimos logs -->
      <div v-click class="widget !bg-[#0f1724] !text-[#d1d5db]">
        <div class="w-title !text-[#d1d5db]">Últimos erros</div>
        <div class="font-mono text-[0.55rem] leading-relaxed">
          <div>19:42:13 <span class="text-red-400">Error</span> PagamentoService · pedido 4821 · Timeout</div>
          <div>19:42:15 <span class="text-red-400">Error</span> PagamentoService · pedido 4822 · Timeout</div>
          <div>19:42:31 <span class="text-red-400">Error</span> PagamentoService · pedido 4825 · Timeout</div>
        </div>
      </div>

      <!-- alarmes -->
      <div v-click class="widget">
        <div class="w-title">Alarmes</div>
        <div class="flex flex-col gap-1 text-[0.6rem]">
          <div><span class="status critical">⛔ ALARME</span> PagamentoErros</div>
          <div><span class="status critical">⛔ ALARME</span> LatenciaGateway</div>
          <div><span class="status good">✔ OK</span> CPU-ECS</div>
          <div><span class="status good">✔ OK</span> 5xx-LoadBalancer</div>
        </div>
      </div>

      <!-- recuperação de vendas pelo marketing -->
      <div v-click class="widget recover">
        <div class="w-title">📣 Recuperação de vendas · Marketing</div>
        <div class="text-[0.62rem] leading-snug">
          Viu <b>52 pedidos com falha</b> no dashboard e enviou um <b>cupom de 10%</b> às 19:50
        </div>
        <div class="flex items-end gap-2 mt-1">
          <div class="kpi !text-lg">37 / 52</div>
          <div class="text-[0.6rem] op-80 pb-1">clientes concluíram a compra (71%)</div>
        </div>
        <div class="text-[0.65rem] font-bold text-emerald-500">≈ R$ 6 mil recuperados 🎉</div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.cw { font-size: 0.7rem; }
.cw-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 8px;
}
.pill {
  font-size: 0.6rem;
  padding: 2px 8px;
  border-radius: 6px;
  background: var(--card-bg);
  border: 1px solid var(--card-border);
}
.widget {
  padding: 6px 10px;
  border-radius: 8px;
  background: var(--card-bg);
  border: 1px solid var(--card-border);
}
.w-title { font-size: 0.6rem; font-weight: 600; opacity: 0.75; margin-bottom: 2px; }
.kpi { font-size: 1.15rem; font-weight: 800; display: flex; align-items: center; gap: 6px; flex-wrap: wrap; }
.delta { font-size: 0.6rem; font-weight: 700; }
.delta.bad { color: #ef4444; }
.status { font-size: 0.55rem; font-weight: 700; padding: 1px 6px; border-radius: 9999px; color: #fff; }
.status.critical { background: #dc2626; }
.status.good { background: #16a34a; }

.grid-line { stroke: currentColor; opacity: 0.12; }
.axis { font-size: 8px; fill: currentColor; opacity: 0.6; }
.line { fill: none; stroke: #ff9900; stroke-width: 2; stroke-linejoin: round; }
.area { fill: #ff9900; opacity: 0.15; }
.mk-line { stroke-width: 1.2; stroke-dasharray: 3 3; }
.mk-text { font-size: 8px; font-weight: 700; fill: currentColor; }
.mk-alarm .mk-line { stroke: #dc2626; }
.mk-mkt .mk-line { stroke: #8c4fff; }
.mk-fix .mk-line { stroke: #16a34a; }

.bar-track { height: 10px; border-radius: 4px; background: var(--card-border); overflow: hidden; }
.bar-fill { height: 100%; border-radius: 4px; background: #ff9900; }

.recover { border-color: #10b981; }
</style>
