---
theme: default
title: AWS na Prática
info: |
  ## AWS na Prática
  Os serviços que sustentam aplicações na nuvem: EC2, ECS, Load Balancer,
  S3, CloudFront, CloudWatch e API Gateway.

  Isaac de Sousa — Tech Lead · Arquiteto de Software
colorSchema: auto
fonts:
  sans: Inter
  mono: Fira Code
drawings:
  persist: false
transition: slide-left
comark: true
duration: 40min
layout: center
class: text-center
---

<div class="relative">
  <!-- ícones flutuando ao fundo -->
  <AwsIcon name="ec2" class="floating absolute text-5xl op-30" style="left:-60px; top:-90px; animation-delay:0s" />
  <AwsIcon name="s3" class="floating absolute text-5xl op-30" style="right:-50px; top:-110px; animation-delay:.6s" />
  <AwsIcon name="cloudfront" class="floating absolute text-5xl op-30" style="left:-110px; bottom:-70px; animation-delay:1.2s" />
  <AwsIcon name="ecs" class="floating absolute text-5xl op-30" style="right:-100px; bottom:-60px; animation-delay:1.8s" />
  <AwsIcon name="cloudwatch" class="floating absolute text-4xl op-30" style="left:40%; top:-120px; animation-delay:2.4s" />
  <AwsIcon name="api-gateway" class="floating absolute text-4xl op-30" style="left:45%; bottom:-110px; animation-delay:3s" />

  <AwsIcon name="aws" class="aws-logo text-8xl mx-auto mb-6" v-motion
    :initial="{ scale: 0.4, opacity: 0 }"
    :enter="{ scale: 1, opacity: 1, transition: { type: 'spring', stiffness: 120 } }" />

  <h1
    v-motion
    :initial="{ y: 40, opacity: 0 }"
    :enter="{ y: 0, opacity: 1, transition: { delay: 300 } }"
    class="!text-6xl"
  >
    AWS na <span class="text-aws">Prática</span>
  </h1>

  <p
    v-motion
    :initial="{ opacity: 0 }"
    :enter="{ opacity: 1, transition: { delay: 700 } }"
    class="text-xl op-80"
  >
    Os serviços que sustentam aplicações na nuvem
  </p>

  <div
    v-motion
    :initial="{ opacity: 0 }"
    :enter="{ opacity: 1, transition: { delay: 1100 } }"
    class="mt-10 text-sm op-60"
  >
    Isaac de Sousa · Tech Lead – Arquiteto de Software · 04/11/2026
  </div>
</div>

<style>
.floating { animation: float 6s ease-in-out infinite; }
@keyframes float {
  0%, 100% { transform: translateY(0) rotate(0deg); }
  50% { transform: translateY(-18px) rotate(6deg); }
}
</style>

<!--
Boas-vindas. Apresentar o tema: vamos ver 7 serviços da AWS que aparecem em praticamente toda aplicação web moderna.
-->

---
layout: default
---

# Quem sou eu

<div class="grid grid-cols-[220px_1fr] gap-10 mt-6 items-start">

<div class="text-center">
  <img
    v-motion
    :initial="{ scale: 0, rotate: -20 }"
    :enter="{ scale: 1, rotate: 0, transition: { type: 'spring', stiffness: 140, damping: 12 } }"
    src="/isaac.png"
    class="w-48 h-48 rounded-full mx-auto border-4 border-[#ff9900] shadow-xl"
  >
  <div class="mt-4 text-2xl font-bold">Isaac de Sousa</div>
  <div class="text-aws">Tech Lead · Arquiteto de Software</div>
</div>

<div>

<v-clicks>

- 🎓 **Engenheiro da Computação** <span class="op-60">(2015)</span>
- 🏗️ **Especialista em Arquitetura de Software Distribuído** <span class="op-60">(2025)</span>
- 💻 Na área de TI **desde 2007**

</v-clicks>

<div v-click class="flex gap-6 mt-6">
  <div class="text-center">
    <img src="/qr-github.svg" class="w-28 h-28 rounded-lg bg-white p-1">
    <div class="text-xs mt-1 flex items-center justify-center gap-1"><carbon-logo-github /> isaacslima</div>
  </div>
  <div class="text-center">
    <img src="/qr-linkedin.svg" class="w-28 h-28 rounded-lg bg-white p-1">
    <div class="text-xs mt-1 flex items-center justify-center gap-1"><carbon-logo-linkedin /> in/isaacslima</div>
  </div>
</div>

</div>
</div>

<!--
Apresentação pessoal. Convidar a turma a escanear os QR codes do GitHub e LinkedIn.
-->

---

# Minha trajetória

<div class="relative mt-8 ml-4">
  <div class="absolute left-[11px] top-2 bottom-2 w-[2px] bg-[#ff9900] op-40" />

  <div v-click class="timeline-item">
    <div class="dot" />
    <div><span class="year">2007</span> <b>Suporte técnico</b> — primeiro contato com TI, resolvendo problemas reais de usuários</div>
  </div>
  <div v-click class="timeline-item">
    <div class="dot" />
    <div><b>Implantação de sistemas</b> — colocando software para rodar em clientes</div>
  </div>
  <div v-click class="timeline-item">
    <div class="dot" />
    <div><b>DBA</b> — banco de dados, performance e disponibilidade</div>
  </div>
  <div v-click class="timeline-item">
    <div class="dot" />
    <div><span class="year">2015</span> <b>Engenharia da Computação</b></div>
  </div>
  <div v-click class="timeline-item">
    <div class="dot" />
    <div><span class="year">2025</span> <b>Especialização em Arquitetura de Software Distribuído</b></div>
  </div>
  <div v-click class="timeline-item">
    <div class="dot pulse" />
    <div><span class="year">Hoje</span> <b class="text-aws">Tech Lead · Arquiteto de Software</b></div>
  </div>
</div>

<div v-click class="mt-6 w-3/4">
  <GithubChart user="isaacslima" />
</div>

<style>
.timeline-item {
  display: flex;
  align-items: center;
  gap: 16px;
  margin-bottom: 12px;
}
.timeline-item .dot {
  flex-shrink: 0;
  width: 24px;
  height: 24px;
  border-radius: 9999px;
  background: var(--aws-orange);
  border: 4px solid var(--card-bg);
  box-shadow: 0 0 0 2px var(--aws-orange);
}
.timeline-item .year {
  font-family: 'Fira Code', monospace;
  color: var(--aws-orange);
  margin-right: 6px;
}
.pulse { animation: pulse 1.6s ease-in-out infinite; }
@keyframes pulse {
  0%, 100% { box-shadow: 0 0 0 2px var(--aws-orange); }
  50% { box-shadow: 0 0 0 10px rgba(255, 153, 0, 0); }
}
</style>

<!--
Do suporte à arquitetura: cada etapa me ensinou um pedaço do que hoje a nuvem resolve (infra, deploy, dados).
Mostrar o gráfico de contribuições do GitHub.
-->

---
layout: center
---

# O que vamos ver hoje

<div class="grid grid-cols-4 gap-6 mt-8">
  <div
    v-for="(s, i) in [
      { icon: 'ec2', name: 'EC2', desc: 'Servidores' },
      { icon: 'ecs', name: 'ECS', desc: 'Containers' },
      { icon: 'elb', name: 'Load Balancer', desc: 'Distribuição' },
      { icon: 's3', name: 'S3', desc: 'Arquivos' },
      { icon: 'cloudfront', name: 'CloudFront', desc: 'CDN' },
      { icon: 'cloudwatch', name: 'CloudWatch', desc: 'Monitoramento' },
      { icon: 'api-gateway', name: 'API Gateway', desc: 'Porta de entrada' },
    ]"
    :key="s.name"
    v-motion
    :initial="{ y: 50, opacity: 0 }"
    :enter="{ y: 0, opacity: 1, transition: { delay: i * 120 } }"
    class="card flex flex-col items-center gap-2 hover:scale-110 transition"
  >
    <AwsIcon :name="s.icon" class="text-5xl" />
    <div class="font-bold">{{ s.name }}</div>
    <div class="text-xs op-60">{{ s.desc }}</div>
  </div>
</div>

<!--
Agenda. 7 serviços, do servidor ao monitoramento. No final, juntamos tudo numa arquitetura.
-->

---

# Antes de tudo: o que é a nuvem?

<div class="grid grid-cols-2 gap-8 mt-6">

<div v-click class="card">

### 🏢 On-premise
- Comprar servidores
- Montar data center, energia, refrigeração
- Semanas para provisionar
- Paga mesmo sem usar

</div>

<div v-click class="card !border-[#ff9900]">

### ☁️ Nuvem (AWS)
- Recursos **sob demanda**
- Criados em **minutos**
- Paga **pelo que usa**
- Escala para cima e para baixo

</div>

</div>

<div v-click class="analogy mt-8">
💡 <b>Analogia:</b> é como trocar ter um gerador de energia em casa por usar a rede elétrica — você só liga na tomada e paga a conta do que consumiu.
</div>

<div v-click class="mt-4 text-sm op-70">
🌎 A AWS organiza sua infraestrutura em <b>Regiões</b> (ex.: <code>sa-east-1</code> São Paulo) e cada região tem várias <b>Zonas de Disponibilidade (AZs)</b> — data centers isolados entre si.
</div>

<!--
Nivelar a turma: on-premise vs nuvem, regiões e AZs. Importante para entender alta disponibilidade depois (ELB entre AZs).
-->

---

<AwsService icon="ec2" name="EC2" full="Elastic Compute Cloud" tagline="Servidores virtuais sob demanda" />

<div class="grid grid-cols-2 gap-8">
<div>

<v-clicks>

- 🖥️ Uma **máquina virtual** (Linux ou Windows) na AWS
- 📦 **AMI** — a "imagem" do sistema operacional
- 📏 **Tipos de instância** — CPU/memória sob medida (`t3.micro`, `m7g.large`…)
- 💾 **EBS** — o "HD" da instância
- 🔒 **Security Group** — o firewall da máquina

</v-clicks>

</div>
<div>

<div v-click class="analogy">
💡 <b>Analogia:</b> alugar um computador num data center — você escolhe o tamanho, liga, usa e desliga quando quiser.
</div>

<div v-click class="card mt-4">
<div class="font-bold mb-2">💰 Modelos de cobrança</div>
<div class="text-sm">
<b>On-Demand</b> — por segundo/hora, sem compromisso<br>
<b>Spot</b> — sobra de capacidade, até ~90% mais barato<br>
<b>Savings Plans / Reservadas</b> — compromisso de 1 ou 3 anos
</div>
</div>

</div>
</div>

<!--
EC2 é a base de quase tudo na AWS. Mostrar no console como seria criar uma instância (opcional).
Spot pode ser interrompida — bom para processamento em lote, ruim para banco de dados.
-->

---

# EC2 — escalando automaticamente

<div class="flex items-end justify-center gap-4 h-48 mt-6">
  <div class="text-center">
    <AwsIcon name="ec2" class="text-5xl" />
    <div class="text-xs op-60">sempre ligada</div>
  </div>
  <div v-click class="text-center">
    <AwsIcon name="ec2" class="text-5xl" />
    <div class="text-xs op-60">pico</div>
  </div>
  <div v-click class="text-center">
    <AwsIcon name="ec2" class="text-5xl" />
    <div class="text-xs op-60">Black Friday 🛒</div>
  </div>
</div>

<div v-click class="card mt-8 text-center">
<b>Auto Scaling Group</b>: adiciona instâncias quando a carga sobe e remove quando cai.<br>
<span class="op-70 text-sm">Você define mínimo, máximo e a regra (ex.: CPU acima de 70%).</span>
</div>

```bash {all|1|2-4|all}
aws ec2 run-instances \
  --image-id ami-0abc1234 \
  --instance-type t3.micro \
  --count 1
```

<!--
Elasticidade é o "E" do EC2. Auto Scaling + CloudWatch (veremos depois) trabalham juntos.
O comando é só ilustrativo: criar uma instância pela CLI.
-->

---

<AwsService icon="ecs" name="ECS" full="Elastic Container Service" tagline="Rodando containers sem dor de cabeça" />

<div class="grid grid-cols-2 gap-8">
<div>

<v-clicks>

- 🐳 Orquestra **containers Docker**
- 📝 **Task Definition** — a "receita": imagem, CPU, memória, portas
- 🔁 **Service** — mantém N cópias rodando e substitui as que caem
- 🗂️ **Cluster** — agrupamento lógico onde as tasks rodam
- 📦 Imagens ficam no **ECR** (registro de containers da AWS)

</v-clicks>

</div>
<div>

<div v-click class="analogy">
💡 <b>Analogia:</b> o container é uma marmita pronta; o ECS é o restaurante que garante que sempre haja marmitas sendo servidas.
</div>

<div v-click class="grid grid-cols-2 gap-3 mt-4">
  <div class="card text-center">
    <AwsIcon name="ec2" class="text-3xl mx-auto" />
    <div class="font-bold mt-1">EC2</div>
    <div class="text-xs op-70">você gerencia as máquinas</div>
  </div>
  <div class="card text-center !border-[#ff9900]">
    <AwsIcon name="fargate" class="text-3xl mx-auto" />
    <div class="font-bold mt-1">Fargate</div>
    <div class="text-xs op-70">serverless: só o container</div>
  </div>
</div>

</div>
</div>

<!--
Dois modos de execução (launch types): EC2 e Fargate. Para iniciantes, Fargate é o caminho mais simples.
Comparar com Kubernetes (EKS) só se perguntarem.
-->

---

<AwsService icon="elb" name="Elastic Load Balancing" full="ALB · NLB · GWLB" tagline="Distribuindo o tráfego entre servidores" />

<div class="flex items-center justify-center gap-6 mt-2">
  <div v-click class="text-center">
    <carbon-user-multiple class="text-5xl" />
    <div class="text-xs">usuários</div>
  </div>
  <div v-after class="flow-line max-w-24" />
  <div v-after class="text-center">
    <AwsIcon name="elb" class="text-6xl" />
    <div class="text-xs">Load Balancer</div>
  </div>
  <div v-click class="flex flex-col gap-3">
    <div v-for="n in 3" :key="n" class="flex items-center gap-2">
      <div class="flow-line w-20" />
      <AwsIcon name="ec2" class="text-3xl" />
      <span class="text-xs op-60">AZ {{ ['a','b','c'][n-1] }}</span>
    </div>
  </div>
</div>

<div class="grid grid-cols-3 gap-4 mt-8">
  <div v-click class="card"><b>ALB</b> <span class="text-xs op-60">camada 7</span><br><span class="text-sm">HTTP/HTTPS, roteia por caminho (<code>/api</code>) ou domínio</span></div>
  <div v-click class="card"><b>NLB</b> <span class="text-xs op-60">camada 4</span><br><span class="text-sm">TCP/UDP, altíssima performance e IP fixo</span></div>
  <div v-click class="card"><b>Health check</b><br><span class="text-sm">Servidor doente? Para de receber tráfego automaticamente</span></div>
</div>

<!--
Analogia: o recepcionista do restaurante que distribui clientes entre os garçons livres.
Distribuir entre AZs = se um data center cair, a aplicação continua no ar.
-->

---

# ALB vs NLB: quando usar cada um?

<div class="grid grid-cols-2 gap-6 mt-2">
  <div class="card !py-2 flex items-center gap-3">
    <AwsIcon name="elb" class="text-3xl" />
    <div><b class="text-sky-500">ALB</b> <span class="text-xs op-60">camada 7 · HTTP/HTTPS</span><br><span class="text-sm">Lê a requisição: URL, domínio, cabeçalhos</span></div>
  </div>
  <div class="card !py-2 flex items-center gap-3">
    <AwsIcon name="elb" class="text-3xl" />
    <div><b class="text-emerald-500">NLB</b> <span class="text-xs op-60">camada 4 · TCP/UDP</span><br><span class="text-sm">Só olha IP e porta: mais rápido</span></div>
  </div>
</div>

<div class="lb-examples mt-3">
  <div v-click class="lb-row">
    <span>🛒 E-commerce: <code>/api/pedidos</code> vai para o serviço de pedidos e <code>/imagens</code> para o de imagens</span>
    <span class="badge alb">ALB</span>
  </div>
  <div v-click class="lb-row">
    <span>🌐 Dois sites no mesmo balanceador: <code>loja.com</code> e <code>admin.loja.com</code></span>
    <span class="badge alb">ALB</span>
  </div>
  <div v-click class="lb-row">
    <span>🔐 Exigir login (Cognito/OIDC) antes de a requisição chegar na aplicação</span>
    <span class="badge alb">ALB</span>
  </div>
  <div v-click class="lb-row">
    <span>🎮 Servidor de jogo multiplayer, que usa <b>UDP</b> e não HTTP</span>
    <span class="badge nlb">NLB</span>
  </div>
  <div v-click class="lb-row">
    <span>🏦 O banco parceiro só libera no firewall um <b>IP fixo</b></span>
    <span class="badge nlb">NLB</span>
  </div>
  <div v-click class="lb-row">
    <span>📡 IoT: milhões de conexões TCP com latência mínima</span>
    <span class="badge nlb">NLB</span>
  </div>
</div>

<div v-click class="analogy mt-3 text-sm !py-2">
💡 <b>ALB</b> é o recepcionista que <b>lê o pedido</b> e manda ao setor certo. <b>NLB</b> é o guarda de trânsito que direciona os carros <b>sem abrir o porta-malas</b>.
</div>

<style>
.lb-examples { display: flex; flex-direction: column; gap: 6px; }
.lb-row {
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 16px;
  font-size: 0.85rem;
  padding: 3px 14px;
  border-radius: 10px;
  background: var(--card-bg);
  border: 1px solid var(--card-border);
}
.badge {
  flex-shrink: 0;
  font-weight: 700;
  font-size: 0.75rem;
  padding: 2px 10px;
  border-radius: 9999px;
  color: #fff;
}
.badge.alb { background: #0ea5e9; }
.badge.nlb { background: #10b981; }
</style>

<!--
Regra prática: se a decisão depende do CONTEÚDO da requisição HTTP (URL, domínio, login), use ALB.
Se é outro protocolo (TCP/UDP), precisa de IP fixo ou de performance extrema, use NLB.
-->

---

<AwsService icon="s3" name="S3" full="Simple Storage Service" tagline="Armazenamento de objetos praticamente ilimitado" />

<div class="grid grid-cols-2 gap-8">
<div>

<v-clicks>

- 🪣 **Bucket** — o "container" dos arquivos (nome único global)
- 📄 **Objeto** — qualquer arquivo + metadados, até 5 TB
- 🛡️ Durabilidade de **99,999999999%** (11 noves)
- 🕓 **Versionamento** — recupere versões antigas
- 🌐 Pode hospedar **sites estáticos**

</v-clicks>

</div>
<div>

<div v-click class="analogy">
💡 <b>Analogia:</b> um Google Drive infinito, acessado por código via URL/API.
</div>

<div v-click class="card mt-4">
<div class="font-bold mb-2">🧊 Classes de armazenamento</div>
<div class="flex items-center gap-2 text-sm">
  <span class="px-2 py-1 rounded bg-[#ff9900] text-black">Standard</span>
  <carbon-arrow-right />
  <span class="px-2 py-1 rounded bg-[#ff9900]/60 text-black">Infrequent Access</span>
  <carbon-arrow-right />
  <span class="px-2 py-1 rounded bg-sky-400/70 text-black">Glacier</span>
</div>
<div class="text-xs op-70 mt-2">quanto menos acesso, mais barato guardar — e mais lento/caro para ler</div>
</div>

</div>
</div>

```bash {hide|1|2|all}
aws s3 cp foto.png s3://meu-bucket-aula/imagens/
aws s3 ls s3://meu-bucket-aula/imagens/
```

<!--
S3 não é um disco: não se "monta" como HD, acessa-se por API.
Cuidado com buckets públicos — vazamentos famosos vieram de configuração errada.
-->

---

# Exemplo: o nosso próprio "Drive" com 100 GB

<div class="text-sm op-60 -mt-2 mb-4">Rascunho didático: sem IAM, criptografia ou outras camadas de segurança</div>

<div class="flex items-center justify-center gap-4">
  <div v-click class="drive-node"><carbon-user-multiple class="text-4xl" /><span>Usuários</span></div>
  <div v-after class="flow-line max-w-20" />
  <div v-after class="drive-node"><AwsIcon name="ec2" class="text-4xl" /><span>App de upload (EC2)</span></div>
  <div v-click class="flow-line max-w-20" />
  <div v-after class="drive-node !border-[#ff9900]"><AwsIcon name="s3" class="text-4xl" /><span>Bucket <code>meu-drive</code></span></div>
</div>

<div v-click class="mt-8">
  <div class="text-center font-bold mb-3">♻️ Regra de ciclo de vida (Lifecycle): o próprio S3 move os arquivos com o tempo</div>
  <div class="grid grid-cols-3 gap-0 text-center">
    <div class="tier" style="--c:#ff9900">
      <div class="font-bold">Standard</div>
      <div class="text-xs op-80">dia 0 a 30 · arquivos recentes</div>
      <div class="text-2xl font-bold mt-1">20 GB</div>
    </div>
    <div class="tier" style="--c:#0ea5e9">
      <div class="font-bold">Standard-IA</div>
      <div class="text-xs op-80">dia 30 a 90 · abertos às vezes</div>
      <div class="text-2xl font-bold mt-1">30 GB</div>
    </div>
    <div class="tier" style="--c:#6366f1">
      <div class="font-bold">Glacier Instant Retrieval</div>
      <div class="text-xs op-80">após 90 dias · quase nunca abertos</div>
      <div class="text-2xl font-bold mt-1">50 GB</div>
    </div>
  </div>
  <div class="flow-line mt-3 !flex-none w-full" />
  <div class="flex justify-between text-xs op-60 mt-1"><span>upload</span><span>30 dias</span><span>90 dias</span><span>anos…</span></div>
</div>

<style>
.drive-node {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 4px;
  font-size: 0.8rem;
  padding: 10px 14px;
  border-radius: 12px;
  background: var(--card-bg);
  border: 1px solid var(--card-border);
}
.tier {
  padding: 10px;
  border-top: 6px solid var(--c);
  background: var(--card-bg);
}
</style>

<!--
Contar a história: usuário sobe um arquivo, ele é muito acessado na primeira semana e depois quase ninguém abre.
Por que pagar preço de "prateleira da frente" por um arquivo esquecido? A regra de Lifecycle muda a classe sozinha.
Distribuição de 20/30/50 é uma suposição didática.
-->

---

# Quanto custa guardar 100 GB por mês?

<div class="flex flex-col gap-3 mt-4">
  <div v-click class="cost-row">
    <span class="label">Tudo em Standard</span>
    <div class="bar"><div class="fill" style="--w:100%; --c:#ff9900" /></div>
    <span class="value">US$ 2,30</span>
  </div>
  <div v-click class="cost-row">
    <span class="label">Tudo em Standard-IA</span>
    <div class="bar"><div class="fill" style="--w:54%; --c:#0ea5e9" /></div>
    <span class="value">US$ 1,25 <span class="extra">+ US$ 0,01/GB lido</span></span>
  </div>
  <div v-click class="cost-row">
    <span class="label">Tudo em Glacier IR</span>
    <div class="bar"><div class="fill" style="--w:17%; --c:#6366f1" /></div>
    <span class="value">US$ 0,40 <span class="extra">+ US$ 0,03/GB lido</span></span>
  </div>
  <div v-click class="cost-row">
    <span class="label font-bold text-aws">Mesclado (Lifecycle)</span>
    <div class="bar"><div class="fill" style="--w:45%; --c:#10b981" /></div>
    <span class="value font-bold">US$ 1,04 <span class="extra text-emerald-500 !op-100">−55%</span></span>
  </div>
</div>

<div v-click class="card mt-4 text-sm font-mono">
20 GB × 0,023 + 30 GB × 0,0125 + 50 GB × 0,004 = 0,46 + 0,375 + 0,20 ≈ <b class="text-aws">US$ 1,04/mês</b>
</div>

<div class="grid grid-cols-2 gap-4 mt-4">
  <div v-click class="analogy text-sm">
    📈 <b>E com 10 TB?</b> Tudo em Standard ≈ <b>US$ 235/mês</b>; mesclado ≈ <b>US$ 106/mês</b>.
    Economia de cerca de <b class="text-aws">US$ 1.550 por ano</b>.
  </div>
  <div v-click class="analogy text-sm">
    ⚖️ <b>Por que não tudo no Glacier?</b> Guardar é barato, mas <b>ler</b> custa caro, e há tempo mínimo cobrado (30 dias no IA e 90 no Glacier).
  </div>
</div>

<div class="text-xs op-50 mt-3">Preços de armazenamento em us-east-1 (nov/2026), sem requisições nem transferência. A região de São Paulo é mais cara.</div>

<style>
.cost-row {
  display: grid;
  grid-template-columns: 200px 1fr 230px;
  align-items: center;
  gap: 12px;
}
.cost-row .label { font-size: 0.9rem; }
.cost-row .value { font-family: 'Fira Code', monospace; font-size: 0.9rem; }
.cost-row .extra { font-size: 0.7rem; opacity: 0.6; }
.cost-row .bar {
  height: 22px;
  border-radius: 9999px;
  background: var(--card-bg);
  border: 1px solid var(--card-border);
  overflow: hidden;
}
/* A barra "cresce" quando o v-click revela a linha */
.cost-row .fill {
  height: 100%;
  width: 0;
  background: var(--c);
  border-radius: 9999px;
  transition: width 1s ease-out;
}
.cost-row:not(.slidev-vclick-hidden) .fill { width: var(--w); }
</style>

<!--
Cada barra é proporcional ao custo de "tudo em Standard".
Mensagem principal: escolher a classe certa é decisão de arquitetura e impacta direto na fatura.
Para backup que quase nunca é lido existe ainda o Glacier Deep Archive (~US$ 0,001/GB), com recuperação em horas.
-->

---

<AwsService icon="cloudfront" name="CloudFront" full="Content Delivery Network (CDN)" tagline="Conteúdo perto do usuário, no mundo todo" />

<div class="grid grid-cols-2 gap-8">
<div>

<v-clicks>

- 🌍 Centenas de **edge locations** espalhadas pelo mundo
- ⚡ Faz **cache** do conteúdo perto do usuário → menos latência
- 🔐 HTTPS, proteção contra DDoS (AWS Shield) e WAF
- 🪣 Origem comum: **S3** (site estático) ou **Load Balancer** (API)

</v-clicks>

</div>
<div>

<div v-click class="analogy">
💡 <b>Analogia:</b> em vez de todo mundo buscar o produto na fábrica, ele fica em mercadinhos de bairro.
</div>

<div v-click class="card mt-4 text-sm">
<div class="flex items-center gap-2 mb-2">
  <span>👤 Fortaleza</span><div class="flow-line" /><span>📍 Edge Fortaleza</span>
</div>
<div class="flex items-center gap-2">
  <span class="op-60">cache miss?</span><div class="flow-line" /><span>🪣 Origem (S3)</span>
</div>
<div class="text-xs op-70 mt-2">a 1ª requisição vai à origem; as seguintes saem do cache</div>
</div>

</div>
</div>

<!--
Explicar cache hit vs cache miss e TTL de forma simples.
Ex.: imagens de um e-commerce, vídeos, o próprio front-end React/Angular.
-->

---

# Como uma CDN funciona na prática

<div class="grid grid-cols-2 gap-6">
  <div v-click class="card !p-2">
    <div class="text-center font-bold text-red-500">❌ Sem CDN</div>
    <CdnMap />
    <div class="text-xs text-center op-70">todo mundo atravessa o planeta até a origem</div>
  </div>
  <div v-click class="card !p-2 !border-[#10b981]">
    <div class="text-center font-bold text-emerald-500">✅ Com CloudFront</div>
    <CdnMap cdn />
    <div class="text-xs text-center op-70"><span class="inline-block w-2.5 h-2.5 rounded-full bg-[#8c4fff]" /> edge location perto de cada usuário</div>
  </div>
</div>

<div class="grid grid-cols-4 gap-3 mt-4 text-sm">
  <div v-click class="cdn-step">
    <div class="step-n">1</div>
    👤 <b>Ana</b> (BH) pede <code>foto.png</code><br>
    📍 Edge SP: <span class="tag miss">MISS</span> "não tenho"
  </div>
  <div v-click class="cdn-step">
    <div class="step-n">2</div>
    📍 Edge busca na 🪣 <b>origem</b> (~120 ms) e <b>guarda uma cópia</b>
  </div>
  <div v-click class="cdn-step">
    <div class="step-n">3</div>
    👤 <b>Bruno</b> (RJ) pede a mesma foto<br>
    📍 Edge SP: <span class="tag hit">HIT</span> ⚡ ~15 ms
  </div>
  <div v-click class="cdn-step">
    <div class="step-n">4</div>
    ⏱️ Venceu o <b>TTL</b> ou houve <b>invalidação</b>? A próxima busca volta à origem
  </div>
</div>

<div class="text-xs op-50 mt-2">Latências aproximadas, só para ilustrar.</div>

<style>
.cdn-step {
  position: relative;
  padding: 10px 12px 10px 14px;
  border-radius: 12px;
  background: var(--card-bg);
  border: 1px solid var(--card-border);
  line-height: 1.5;
}
.step-n {
  position: absolute;
  top: -10px;
  left: -8px;
  width: 22px;
  height: 22px;
  border-radius: 9999px;
  background: var(--aws-orange);
  color: #000;
  font-weight: 700;
  font-size: 12px;
  display: flex;
  align-items: center;
  justify-content: center;
}
.tag {
  font-size: 0.7rem;
  font-weight: 700;
  padding: 1px 8px;
  border-radius: 9999px;
  color: #fff;
}
.tag.miss { background: #ef4444; }
.tag.hit { background: #10b981; }
</style>

<!--
Mostrar primeiro o mapa sem CDN: as bolinhas vermelhas demoram para chegar (latência alta, origem sobrecarregada).
Depois com CloudFront: as bolinhas verdes só vão até a edge mais próxima.
Sequência 1→4: o primeiro usuário "paga" o MISS; todos os seguintes ganham o HIT.
TTL = quanto tempo a cópia vale. Invalidação = forçar a edge a buscar de novo (ex.: deploy de nova versão do site).
-->

---

<AwsService icon="cloudwatch" name="CloudWatch" full="Observabilidade da AWS" tagline="Os olhos e ouvidos da sua aplicação" />

<div class="grid grid-cols-4 gap-4">
  <div v-click class="card text-center">
    <carbon-chart-line class="text-4xl text-aws mx-auto" />
    <div class="font-bold mt-2">Métricas</div>
    <div class="text-xs op-70">CPU, memória, requisições, erros</div>
  </div>
  <div v-click class="card text-center">
    <carbon-document class="text-4xl text-aws mx-auto" />
    <div class="font-bold mt-2">Logs</div>
    <div class="text-xs op-70">saída das aplicações centralizada</div>
  </div>
  <div v-click class="card text-center">
    <carbon-notification class="text-4xl text-aws mx-auto" />
    <div class="font-bold mt-2">Alarmes</div>
    <div class="text-xs op-70">avisa (e-mail/SNS) ou age (Auto Scaling)</div>
  </div>
  <div v-click class="card text-center">
    <carbon-dashboard class="text-4xl text-aws mx-auto" />
    <div class="font-bold mt-2">Dashboards</div>
    <div class="text-xs op-70">visão do sistema num painel</div>
  </div>
</div>

<div v-click class="analogy mt-8">
💡 <b>Analogia:</b> o painel do carro — velocidade, combustível e a luz que acende quando algo está errado.
</div>

<div v-click class="card mt-4 font-mono text-sm">
SE <span class="text-aws">CPUUtilization &gt; 70%</span> por 5 min
→ 🔔 alarme → ➕ Auto Scaling adiciona instância EC2
</div>

<!--
Ligar com o slide de Auto Scaling do EC2: quem dispara a escala é um alarme do CloudWatch.
Billing alarm: primeira coisa a configurar numa conta pessoal!
-->

---

# Logs: o jeito errado 😱

<IncomingCall :at="6" label="📞 Sala de crise: gestor chamando…" />

<div class="grid grid-cols-[1fr_1.2fr_40px] gap-5 log-slide">
<div>

```csharp {all|6-9|all}
public class PagamentoService
{
    public async Task Processar(Pedido pedido)
    {
        try { await _gateway.Cobrar(pedido); }
        catch (Exception)
        {
            throw new Exception("Erro"); // 🙈 engoliu o motivo
        }
    }
}
```

<div v-click class="terminal mt-3">
  <div class="terminal-title"><AwsIcon name="cloudwatch" /> CloudWatch Logs · /loja/prod</div>
  <div>19:42:13 <span class="text-red-400">Erro</span></div>
  <div>19:42:15 <span class="text-red-400">Erro</span></div>
  <div>19:43:01 <span class="text-red-400">Erro</span></div>
  <div class="mt-1 op-70">Qual sistema? Qual classe? Qual pedido? Por quê? 🤷</div>
</div>

</div>
<div>

<div class="text-sm font-bold mb-2 op-80">🌙 Sexta-feira, horário de pico</div>

<div class="pain-timeline">
  <div v-click><span class="hora">19:42</span> 📉 Pagamentos começam a falhar, e o log só diz "Erro"</div>
  <div v-click><span class="hora">19:50</span> 📱 Gestor liga: "o que está acontecendo?" E <b>liga de novo a cada 5 minutos</b></div>
  <div v-click><span class="hora">20:15</span> 🚨 <b>Sala de crise</b>: dev, DBA e infra acionados, mais o gestor na call</div>
  <div v-click><span class="hora">20:40</span> 🤯 Cada um com uma teoria, todos perguntando "e aí?". O dev <b>não consegue raciocinar</b></div>
  <div v-click><span class="hora">21:15</span> 🐞 Debug remoto em produção: o breakpoint <b>trava a loja para todos</b>. Piorou!</div>
  <div v-click><span class="hora">22:30</span> 🔁 Adiciona prints, faz novo deploy às pressas e espera o erro voltar</div>
  <div v-click><span class="hora">23:10</span> 😩 Descobre: <b>timeout no gateway de pagamento</b></div>
</div>

<div v-click class="analogy mt-3 text-sm !border-red-500">
<b>~3h30</b> de loja sem vender e <b>40 ligações</b> do gestor. E a conta ainda nem chegou…
</div>

</div>

<div class="pressure">
  <div class="pressure-label">😰</div>
  <div class="pressure-tube">
    <div class="pressure-fill" :style="{ height: `${Math.min(Math.max($clicks - 3, 0), 8) / 8 * 100}%` }" />
  </div>
  <div class="pressure-label text-[0.55rem] op-70">pressão</div>
</div>
</div>

<style>
.pain-timeline { display: flex; flex-direction: column; gap: 5px; font-size: 0.74rem; }
.pain-timeline > div {
  padding: 4px 10px;
  border-radius: 8px;
  background: var(--card-bg);
  border-left: 3px solid #ef4444;
}
.hora {
  font-family: 'Fira Code', monospace;
  font-size: 0.68rem;
  color: #ef4444;
  margin-right: 6px;
}
.pressure {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 4px;
  height: 100%;
  padding-top: 28px;
}
.pressure-tube {
  position: relative;
  flex: 1;
  width: 16px;
  border-radius: 9999px;
  background: var(--card-bg);
  border: 1px solid var(--card-border);
  overflow: hidden;
}
.pressure-fill {
  position: absolute;
  bottom: 0;
  width: 100%;
  border-radius: 9999px;
  background: linear-gradient(0deg, #f59e0b, #ef4444 60%, #b91c1c);
  transition: height 0.6s ease-out;
  animation: shake 0.25s linear infinite;
}
@keyframes shake {
  0%, 100% { transform: translateX(0); }
  50% { transform: translateX(1px); }
}
</style>

<!--
Cenário real e comum: catch genérico que joga fora a exceção original.
Mostrar o termômetro subindo a cada clique: quanto mais gente cobrando, pior a capacidade de raciocinar.
Sala de crise sem informação vira um lugar de opiniões, não de dados.
Debug remoto em produção: um breakpoint pausa a thread/processo e afeta clientes reais.
-->

---

# A conta do incidente 💸

<div class="text-sm op-60 -mt-2 mb-4">Estimativa ilustrativa: ticket médio de R$ 180 e ~40 pedidos por hora no horário de pico</div>

<div class="grid grid-cols-3 gap-4">
  <div v-click class="bill-card">
    <div class="text-3xl">🛒</div>
    <div class="bill-value text-red-500">R$ 25.200</div>
    <div class="text-sm font-bold">em vendas perdidas</div>
    <div class="text-xs op-70 mt-1">~140 pedidos não concluídos em 3h30</div>
  </div>
  <div v-click class="bill-card">
    <div class="text-3xl">⏰</div>
    <div class="bill-value text-amber-500">R$ 1.800</div>
    <div class="text-sm font-bold">de hora extra</div>
    <div class="text-xs op-70 mt-1">3 profissionais × 4 h × R$ 150/h</div>
  </div>
  <div v-click class="bill-card">
    <div class="text-3xl">😞</div>
    <div class="bill-value">Ana desistiu</div>
    <div class="text-sm font-bold">e comprou no concorrente</div>
    <div class="text-xs op-70 mt-1">e talvez nunca mais volte</div>
  </div>
</div>

<div v-click class="grid grid-cols-3 gap-4 mt-4 text-sm">
  <div class="card">📢 Reclamações nas redes sociais</div>
  <div class="card">⭐ Reputação e avaliações da loja</div>
  <div class="card">😴 Time exausto no dia seguinte</div>
</div>

<div v-click class="analogy mt-5 text-center !text-lg">
≈ <b class="text-red-500">R$ 27 mil</b> em uma noite, por causa de um log que dizia só <code>"Erro"</code>.<br>
<span class="text-sm op-80">Um log bem feito custa ~5 linhas de código.</span>
</div>

<style>
.bill-card {
  text-align: center;
  padding: 16px;
  border-radius: 14px;
  background: var(--card-bg);
  border: 1px solid var(--card-border);
}
.bill-value {
  font-size: 1.7rem;
  font-weight: 800;
  margin-top: 6px;
  font-family: 'Fira Code', monospace;
}
</style>

<!--
Números ilustrativos para mostrar a ordem de grandeza: 40 pedidos/h × 3,5 h ≈ 140 pedidos × R$ 180 ≈ R$ 25.200.
Hora extra: dev, DBA e infra, 4 horas cada.
O custo invisível (reputação, cliente que não volta) costuma ser maior que o visível.
-->


---

# Logs: o jeito certo ✅

<div class="grid grid-cols-2 gap-6 log-slide">
<div>

```csharp {all|9-11|12|all}
public class PagamentoService(
    ILogger<PagamentoService> logger, IGateway gateway)
{
    public async Task Processar(Pedido pedido)
    {
        try { await gateway.Cobrar(pedido); }
        catch (Exception ex)
        {
            logger.LogError(ex,
                "Falha ao cobrar pedido {PedidoId} no {Gateway}",
                pedido.Id, "PagaFacil");
            throw; // mantém a exceção original
        }
    }
}
```

<div v-click class="text-xs op-70 mt-2">
🏷️ <b>sistema</b>, <b>ambiente</b> e <b>traceId</b> são incluídos automaticamente pela configuração do logger, e não à mão em cada linha.
</div>

</div>
<div>

<div v-click class="terminal">
  <div class="terminal-title"><AwsIcon name="cloudwatch" /> CloudWatch Logs · /loja/prod · JSON</div>
<pre class="!m-0 !p-0 !bg-transparent">{
  "timestamp": "2026-11-04T19:42:13Z",
  "level":     "<span class="text-red-400">Error</span>",
  "sistema":   "<span class="text-aws">loja-api</span>",
  "ambiente":  "prod",
  "classe":    "<span class="text-aws">PagamentoService</span>",
  "metodo":    "<span class="text-aws">Processar</span>",
  "traceId":   "7f3a9c1e",
  "pedidoId":  <span class="text-aws">4821</span>,
  "mensagem":  "Falha ao cobrar pedido 4821 no PagaFacil",
  "erro":      "<span class="text-red-400">TimeoutException: 5000ms</span>
                at PagamentoService.cs:<span class="text-aws">6</span>"
}</pre>
</div>

<div v-click class="terminal mt-3">
  <div class="terminal-title">🔎 Logs Insights</div>
<pre class="!m-0 !p-0 !bg-transparent">fields @timestamp, classe, pedidoId, erro
| filter level = "Error" and sistema = "loja-api"
| stats count() by classe</pre>
</div>

</div>
</div>

<div class="grid grid-cols-2 gap-4 mt-3">
  <div v-click class="analogy text-sm !border-emerald-500">
    ⏱️ <b>19:44</b>, 2 minutos depois: já sabemos o sistema, a classe, o pedido e o motivo.
  </div>
  <div v-click class="analogy text-sm !border-emerald-500">
    🔔 Um <b>alarme</b> com mais de 10 erros em 5 min avisa o time <b>antes</b> do cliente ligar.
  </div>
</div>

<!--
Mesmo erro, mesmo horário: com log estruturado, a investigação vira uma consulta.
Padrão mínimo de um bom log: timestamp, nível, sistema, ambiente, classe/método, ID de correlação (traceId), IDs de negócio e a exceção original.
traceId permite seguir a mesma requisição por API Gateway → ECS → outros serviços.
Nunca registrar senha, número de cartão ou dados pessoais sensíveis.
-->

---

# Dashboard: o incidente numa única tela 📊

<CloudWatchDashboard class="mt-2" />

<!--
Mesmo incidente do slide anterior, agora com dashboard:
1. KPIs: pedidos caindo, erro em pagamentos acima do limite, latência do gateway no teto (timeout).
2. Gráfico: o pico começa às 19:42, o alarme dispara às 19:44, o cupom sai às 19:50 e a correção às 19:58.
3. Logs Insights mostra que quase todo erro vem da PagamentoService.
4. Últimos erros com pedido e motivo, alarmes em vermelho e o restante saudável (CPU, 5xx): não é infraestrutura.
5. O marketing também olha o dashboard: vê os 52 pedidos com falha e envia um cupom de 10%, e 37 clientes concluem a compra.
Comparar: sem logs, Ana desistiu e foi para o concorrente; com dados, o time de negócio também age.
-->

---

<AwsService icon="api-gateway" name="API Gateway" full="Amazon API Gateway" tagline="A porta de entrada das suas APIs" />

<div class="grid grid-cols-2 gap-8">
<div>

<v-clicks>

- 🚪 Ponto único de entrada para **APIs REST, HTTP e WebSocket**
- 🔑 **Autenticação** — Cognito, IAM ou authorizer customizado
- 🚦 **Throttling** — limita requisições por segundo
- 🔀 Integra com **Lambda**, serviços HTTP e recursos privados (VPC Link)
- 🧾 Versões e estágios: `dev`, `hml`, `prod`

</v-clicks>

</div>
<div>

<div v-click class="analogy">
💡 <b>Analogia:</b> a portaria do prédio — confere quem é, limita o fluxo e indica o andar certo.
</div>

<div v-click class="card mt-4 text-sm">
<div class="flex items-center gap-2">
  <span>📱 App</span><div class="flow-line" />
  <AwsIcon name="api-gateway" class="text-2xl" /><div class="flow-line" />
  <div class="flex flex-col gap-1">
    <span class="flex items-center gap-1"><AwsIcon name="lambda" /> <code>/pedidos</code></span>
    <span class="flex items-center gap-1"><AwsIcon name="ecs" /> <code>/produtos</code></span>
  </div>
</div>
</div>

</div>
</div>

<!--
Comum em arquiteturas de microsserviços e serverless.
Diferença para o Load Balancer: o API Gateway entende "API" (auth, rate limit, versionamento); o LB só distribui tráfego.
-->

---
layout: center
---

# Juntando tudo 🧩

<div class="arch mt-6">
  <div class="arch-grid">
    <div class="node" v-click><carbon-user-multiple class="text-4xl" /><span>Usuário</span></div>
    <div class="flow-line" v-after />
    <div class="node" v-after><AwsIcon name="cloudfront" class="text-4xl" /><span>CloudFront</span></div>
    <div class="flow-line" v-click />
    <div class="node" v-after><AwsIcon name="api-gateway" class="text-4xl" /><span>API Gateway</span></div>
    <div class="flow-line" v-click />
    <div class="node" v-after><AwsIcon name="elb" class="text-4xl" /><span>Load Balancer</span></div>
    <div class="flow-line" v-click />
    <div class="node" v-after>
      <div class="flex gap-1"><AwsIcon name="ecs" class="text-4xl" /><AwsIcon name="ec2" class="text-4xl" /></div>
      <span>ECS / EC2</span>
    </div>
    <div class="flow-line-v" style="grid-column:3; grid-row:2" v-click />
    <div class="node" style="grid-column:3; grid-row:3" v-after>
      <AwsIcon name="s3" class="text-4xl" /><span>S3 <span class="op-60 text-xs">(front + imagens)</span></span>
    </div>
  </div>

  <div v-click class="card mt-6 flex items-center justify-center gap-3 !border-[#ff9900]">
    <AwsIcon name="cloudwatch" class="text-4xl" />
    <span><b>CloudWatch</b> observando tudo: métricas, logs e alarmes</span>
  </div>
</div>

<style>
.arch-grid {
  display: grid;
  grid-template-columns: auto 1fr auto 1fr auto 1fr auto 1fr auto;
  align-items: center;
  column-gap: 8px;
  width: 820px;
}
.arch-grid .flow-line { min-width: 30px; }
.arch .node {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 4px;
  font-size: 0.8rem;
  padding: 10px;
  border-radius: 12px;
  background: var(--card-bg);
  border: 1px solid var(--card-border);
  min-width: 100px;
}
.flow-line-v {
  width: 3px;
  height: 36px;
  justify-self: center;
  background-image: linear-gradient(180deg, var(--aws-orange) 50%, transparent 50%);
  background-size: 3px 14px;
  animation: flow-v 0.8s linear infinite;
}
@keyframes flow-v { to { background-position: 0 14px; } }
</style>

<!--
Contar a história de uma requisição: usuário abre o site → CloudFront entrega o front do S3 → front chama a API
→ API Gateway autentica → Load Balancer distribui → containers no ECS (rodando em EC2/Fargate) respondem
→ CloudWatch monitora cada etapa.
-->

---

# Resumo

| Serviço | Para que serve | Lembre como |
| --- | --- | --- |
| <span class="flex items-center gap-2"><AwsIcon name="ec2" /> EC2</span> | Servidores virtuais | computador alugado |
| <span class="flex items-center gap-2"><AwsIcon name="ecs" /> ECS</span> | Orquestrar containers | restaurante de marmitas |
| <span class="flex items-center gap-2"><AwsIcon name="elb" /> ELB</span> | Distribuir tráfego | recepcionista |
| <span class="flex items-center gap-2"><AwsIcon name="s3" /> S3</span> | Guardar arquivos | Drive infinito |
| <span class="flex items-center gap-2"><AwsIcon name="cloudfront" /> CloudFront</span> | Entregar rápido (CDN) | mercadinho de bairro |
| <span class="flex items-center gap-2"><AwsIcon name="cloudwatch" /> CloudWatch</span> | Monitorar | painel do carro |
| <span class="flex items-center gap-2"><AwsIcon name="api-gateway" /> API Gateway</span> | Entrada das APIs | portaria do prédio |

<!--
Revisão rápida com as analogias. Bom momento para perguntas.
-->

---

# Como começar 🚀

<v-clicks>

- 🆓 Crie uma conta e use o **Free Tier** / créditos para novas contas
- 🔔 **Primeiro passo:** configure um **alarme de billing** (AWS Budgets) — evite sustos!
- 🔐 Não use o usuário root no dia a dia; ative **MFA**
- 🎓 **AWS Skill Builder** e **AWS Educate** — cursos gratuitos
- 🏅 Certificação de entrada: **AWS Certified Cloud Practitioner**
- 🧪 Projeto prático: site estático no **S3 + CloudFront**

</v-clicks>

<!--
Reforçar: sempre desligar/apagar recursos de teste.
-->

---
layout: center
class: text-center
---

# Obrigado! 🙌

<div class="text-xl op-80 mb-8">Perguntas?</div>

<div class="flex justify-center gap-12">
  <div v-motion :initial="{ y: 40, opacity: 0 }" :enter="{ y: 0, opacity: 1, transition: { delay: 200 } }" class="text-center">
    <img src="/qr-github.svg" class="w-36 h-36 rounded-lg bg-white p-1 mx-auto">
    <div class="mt-2 flex items-center justify-center gap-1"><carbon-logo-github /> github.com/isaacslima</div>
  </div>
  <div v-motion :initial="{ y: 40, opacity: 0 }" :enter="{ y: 0, opacity: 1, transition: { delay: 400 } }" class="text-center">
    <img src="/qr-linkedin.svg" class="w-36 h-36 rounded-lg bg-white p-1 mx-auto">
    <div class="mt-2 flex items-center justify-center gap-1"><carbon-logo-linkedin /> linkedin.com/in/isaacslima</div>
  </div>
</div>

<div class="mt-8 op-60">Isaac de Sousa · Tech Lead – Arquiteto de Software</div>
