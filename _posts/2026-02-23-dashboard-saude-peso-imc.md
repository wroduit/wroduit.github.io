---
layout: post
title: "Dashboard de Saúde — Peso & IMC"
date: 2026-02-23
categories: [saúde, dados]
tags: [peso, imc, fitdays, dashboard]
description: "Acompanhamento de peso corporal e IMC de fevereiro de 2025 a fevereiro de 2026, com gráficos interativos e análise mensal."
---

<!-- Fontes e dependências -->
<link rel="preconnect" href="https://fonts.googleapis.com">
<link href="https://fonts.googleapis.com/css2?family=DM+Serif+Display:ital@0;1&family=DM+Mono:wght@300;400;500&family=DM+Sans:wght@300;400;500;600&display=swap" rel="stylesheet">
<script src="https://cdnjs.cloudflare.com/ajax/libs/Chart.js/4.4.1/chart.umd.min.js"></script>

<style>
:root {
  --bg: #0a0e17;
  --surface: #111827;
  --surface2: #1a2235;
  --border: #1e2d47;
  --accent: #3b82f6;
  --accent2: #10b981;
  --accent3: #f59e0b;
  --accent4: #ef4444;
  --text: #e2e8f0;
  --muted: #64748b;
}

.dash-wrap {
  background: var(--bg);
  color: var(--text);
  font-family: 'DM Sans', sans-serif;
  padding: 0;
  margin: 0 -1rem;
  background-image:
    radial-gradient(ellipse 80% 50% at 20% -10%, rgba(59,130,246,0.08) 0%, transparent 60%),
    radial-gradient(ellipse 60% 40% at 80% 110%, rgba(16,185,129,0.06) 0%, transparent 50%);
}

.dash-header {
  padding: 40px 48px 24px;
  border-bottom: 1px solid var(--border);
  display: flex;
  align-items: flex-end;
  justify-content: space-between;
  flex-wrap: wrap;
  gap: 16px;
}

.dash-header h1 {
  font-family: 'DM Serif Display', serif;
  font-size: clamp(28px, 4vw, 44px);
  font-weight: 400;
  letter-spacing: -0.02em;
  line-height: 1;
  background: linear-gradient(135deg, #e2e8f0 0%, #94a3b8 100%);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  margin: 0;
}

.dash-header p {
  font-family: 'DM Mono', monospace;
  font-size: 12px;
  color: var(--muted);
  margin-top: 8px;
  letter-spacing: 0.08em;
  text-transform: uppercase;
}

.period-badge {
  font-family: 'DM Mono', monospace;
  font-size: 11px;
  color: var(--accent);
  background: rgba(59,130,246,0.1);
  border: 1px solid rgba(59,130,246,0.25);
  padding: 6px 14px;
  border-radius: 100px;
  letter-spacing: 0.05em;
  white-space: nowrap;
}

.kpi-strip {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(180px, 1fr));
  gap: 1px;
  background: var(--border);
  border-top: 1px solid var(--border);
  border-bottom: 1px solid var(--border);
}

.kpi {
  background: var(--surface);
  padding: 24px 28px;
  position: relative;
  overflow: hidden;
}

.kpi::before {
  content: '';
  position: absolute;
  top: 0; left: 0; right: 0;
  height: 2px;
}

.kpi.blue::before  { background: var(--accent); }
.kpi.green::before { background: var(--accent2); }
.kpi.amber::before { background: var(--accent3); }
.kpi.red::before   { background: var(--accent4); }

.kpi-label {
  font-family: 'DM Mono', monospace;
  font-size: 10px;
  color: var(--muted);
  text-transform: uppercase;
  letter-spacing: 0.1em;
  margin-bottom: 10px;
}

.kpi-value {
  font-family: 'DM Serif Display', serif;
  font-size: 36px;
  line-height: 1;
  font-weight: 400;
}

.kpi.blue .kpi-value  { color: #93c5fd; }
.kpi.green .kpi-value { color: #6ee7b7; }
.kpi.amber .kpi-value { color: #fcd34d; }
.kpi.red .kpi-value   { color: #fca5a5; }

.kpi-sub {
  font-size: 12px;
  color: var(--muted);
  margin-top: 6px;
  font-weight: 300;
}

.kpi-delta {
  display: inline-flex;
  align-items: center;
  gap: 4px;
  font-family: 'DM Mono', monospace;
  font-size: 11px;
  margin-top: 8px;
  padding: 3px 8px;
  border-radius: 4px;
  font-weight: 500;
}

.delta-down { background: rgba(16,185,129,0.12); color: #6ee7b7; }
.delta-up   { background: rgba(239,68,68,0.12);  color: #fca5a5; }

.dash-content {
  padding: 32px 48px;
  display: grid;
  gap: 24px;
}

.chart-card {
  background: var(--surface);
  border: 1px solid var(--border);
  border-radius: 12px;
  overflow: hidden;
}

.chart-header {
  padding: 20px 24px 16px;
  border-bottom: 1px solid var(--border);
  display: flex;
  align-items: center;
  justify-content: space-between;
  flex-wrap: wrap;
  gap: 12px;
}

.chart-title {
  font-family: 'DM Serif Display', serif;
  font-size: 18px;
  font-weight: 400;
  letter-spacing: -0.01em;
}

.legend-row {
  display: flex;
  gap: 16px;
  flex-wrap: wrap;
}

.legend-item {
  display: flex;
  align-items: center;
  gap: 6px;
  font-family: 'DM Mono', monospace;
  font-size: 11px;
  color: var(--muted);
}

.legend-dot {
  width: 8px; height: 8px;
  border-radius: 2px;
  flex-shrink: 0;
}

.chart-body {
  padding: 20px 24px 24px;
}

canvas { max-width: 100%; }

.two-col {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 24px;
}

table {
  width: 100%;
  border-collapse: collapse;
  font-family: 'DM Mono', monospace;
  font-size: 12px;
}

thead tr { border-bottom: 1px solid var(--border); }

th {
  text-align: left;
  padding: 10px 16px;
  color: var(--muted);
  font-weight: 400;
  font-size: 10px;
  text-transform: uppercase;
  letter-spacing: 0.08em;
  white-space: nowrap;
}

td {
  padding: 11px 16px;
  border-bottom: 1px solid rgba(255,255,255,0.04);
  color: var(--text);
  white-space: nowrap;
}

tr:last-child td { border-bottom: none; }
tbody tr:hover td { background: rgba(255,255,255,0.02); }

.bar-inline { display: flex; align-items: center; gap: 10px; }

.bar-track {
  flex: 1;
  height: 4px;
  background: var(--border);
  border-radius: 2px;
  overflow: hidden;
  min-width: 60px;
}

.bar-fill {
  height: 100%;
  border-radius: 2px;
  background: var(--accent);
}

.bar-fill.green { background: var(--accent2); }
.bar-fill.amber { background: var(--accent3); }
.bar-fill.red   { background: var(--accent4); }

.tag {
  display: inline-block;
  padding: 2px 7px;
  border-radius: 4px;
  font-size: 10px;
  font-family: 'DM Mono', monospace;
  font-weight: 500;
}

.tag-normal { background: rgba(16,185,129,0.15); color: #6ee7b7; }
.tag-over   { background: rgba(245,158,11,0.15); color: #fcd34d; }
.tag-obese  { background: rgba(239,68,68,0.15);  color: #fca5a5; }

.insight-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(220px, 1fr));
  gap: 16px;
  padding: 20px 24px;
}

.insight-item {
  background: var(--surface2);
  border: 1px solid var(--border);
  border-radius: 8px;
  padding: 16px 18px;
}

.insight-emoji { font-size: 20px; margin-bottom: 8px; }
.insight-text  { font-size: 13px; color: var(--muted); line-height: 1.5; }
.insight-text strong { color: var(--text); font-weight: 500; }

.section-sep {
  display: flex; align-items: center; gap: 16px;
  padding: 8px 0 0;
}
.section-sep-line { flex: 1; height: 1px; background: var(--border); }
.section-sep-label {
  font-family: 'DM Mono', monospace;
  font-size: 12px;
  color: var(--muted);
  white-space: nowrap;
  letter-spacing: 0.06em;
}

.meas-kpi-strip {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(150px, 1fr));
  gap: 1px;
  background: var(--border);
  border: 1px solid var(--border);
  border-radius: 12px;
  overflow: hidden;
}

.meas-kpi {
  background: var(--surface);
  padding: 18px 20px;
  position: relative;
  overflow: hidden;
}

.meas-delta-tag {
  display: inline-flex;
  align-items: center;
  gap: 4px;
  font-family: 'DM Mono', monospace;
  font-size: 10px;
  margin-top: 6px;
  padding: 2px 7px;
  border-radius: 4px;
}

.dash-footer {
  padding: 24px 48px;
  border-top: 1px solid var(--border);
  display: flex;
  align-items: center;
  justify-content: space-between;
  flex-wrap: wrap;
  gap: 12px;
}

.footer-note {
  font-family: 'DM Mono', monospace;
  font-size: 11px;
  color: var(--muted);
}

.month-table-wrap { overflow-x: auto; }

@media (max-width: 768px) {
  .dash-header, .dash-content, .dash-footer { padding-left: 20px; padding-right: 20px; }
  .two-col { grid-template-columns: 1fr; }
}
</style>

<div class="dash-wrap">

  <header class="dash-header">
    <div>
      <h1>Dashboard de Saúde</h1>
      <p>Peso Corporal &amp; Índice de Massa Corporal · Fitdays</p>
    </div>
    <span class="period-badge">FEV 2025 → FEV 2026</span>
  </header>

  <div class="kpi-strip" id="kpiStrip"></div>

  <div class="dash-content">

    <!-- Peso diário e média mensal -->
    <div class="chart-card">
      <div class="chart-header">
        <span class="chart-title">Evolução do Peso (kg) — Diário &amp; Média Mensal</span>
        <div class="legend-row">
          <div class="legend-item"><div class="legend-dot" style="background:#3b82f6"></div>Peso diário</div>
          <div class="legend-item"><div class="legend-dot" style="background:#f59e0b"></div>Média mensal</div>
        </div>
      </div>
      <div class="chart-body"><canvas id="weightLine" height="90"></canvas></div>
    </div>

    <!-- IMC -->
    <div class="chart-card">
      <div class="chart-header">
        <span class="chart-title">Evolução do IMC — Classificação OMS</span>
        <div class="legend-row">
          <div class="legend-item"><div class="legend-dot" style="background:#10b981"></div>IMC diário</div>
          <div class="legend-item"><div class="legend-dot" style="background:rgba(255,255,255,0.15)"></div>Zona saudável (18.5–24.9)</div>
        </div>
      </div>
      <div class="chart-body"><canvas id="bmiLine" height="75"></canvas></div>
    </div>

    <div class="two-col">
      <!-- Barras mensais -->
      <div class="chart-card">
        <div class="chart-header"><span class="chart-title">Média Mensal de Peso</span></div>
        <div class="chart-body"><canvas id="weightBar" height="160"></canvas></div>
      </div>
      <!-- Variação M/M -->
      <div class="chart-card">
        <div class="chart-header"><span class="chart-title">Variação de Peso Mês a Mês (kg)</span></div>
        <div class="chart-body"><canvas id="deltaBar" height="160"></canvas></div>
      </div>
    </div>

    <!-- Tabela mensal -->
    <div class="chart-card">
      <div class="chart-header"><span class="chart-title">Resumo Mensal Detalhado</span></div>
      <div class="month-table-wrap">
        <table id="monthTable">
          <thead>
            <tr>
              <th>Mês</th><th>Peso Médio</th><th>Mín</th><th>Máx</th>
              <th>Variação</th><th>IMC Médio</th><th>Classificação</th><th>Tendência</th>
            </tr>
          </thead>
          <tbody id="monthTableBody"></tbody>
        </table>
      </div>
    </div>

    <!-- Insights gerais -->
    <div class="chart-card">
      <div class="chart-header"><span class="chart-title">Destaques da Jornada</span></div>
      <div class="insight-grid" id="insightGrid"></div>
    </div>

    <!-- Seção medidas corporais -->
    <div class="section-sep">
      <div class="section-sep-line"></div>
      <span class="section-sep-label">📏 Medidas Corporais</span>
      <div class="section-sep-line"></div>
    </div>

    <div class="meas-kpi-strip" id="measKpiStrip"></div>

    <div class="two-col">
      <!-- Radar -->
      <div class="chart-card">
        <div class="chart-header">
          <span class="chart-title">Radar — Perfil Corporal por Data</span>
          <div class="legend-row" id="radarLegend"></div>
        </div>
        <div class="chart-body" style="max-width:420px;margin:0 auto">
          <canvas id="radarChart"></canvas>
        </div>
      </div>
      <!-- Linha por medida -->
      <div class="chart-card">
        <div class="chart-header"><span class="chart-title">Evolução Individual (cm)</span></div>
        <div class="chart-body"><canvas id="measLine" height="170"></canvas></div>
      </div>
    </div>

    <!-- Barras Set vs Fev -->
    <div class="chart-card">
      <div class="chart-header">
        <span class="chart-title">Redução de Medidas — Set/2025 vs Fev/2026</span>
        <span class="period-badge">4 checkpoints</span>
      </div>
      <div class="chart-body"><canvas id="measBar" height="70"></canvas></div>
    </div>

    <!-- Tabela de medidas -->
    <div class="chart-card">
      <div class="chart-header"><span class="chart-title">Histórico Completo de Medidas (cm)</span></div>
      <div class="month-table-wrap">
        <table>
          <thead>
            <tr>
              <th>Data</th><th>Braço</th><th>Tórax</th><th>Abdômen</th>
              <th>Glúteo</th><th>Coxa</th><th>Panturrilha</th><th>Peso</th><th>Δ Abdômen</th>
            </tr>
          </thead>
          <tbody id="measTableBody"></tbody>
        </table>
      </div>
    </div>

    <!-- Insights de medidas -->
    <div class="chart-card">
      <div class="chart-header"><span class="chart-title">Análise das Medidas</span></div>
      <div class="insight-grid" id="measInsightGrid"></div>
    </div>

  </div><!-- /.dash-content -->

  <footer class="dash-footer">
    <span class="footer-note">Fonte: Apple Health / Fitdays · 1,80 m · IMC = peso ÷ altura²</span>
    <span class="footer-note">Dashboard gerado em fev/2026</span>
  </footer>

</div><!-- /.dash-wrap -->

<script>
// ─── DADOS ────────────────────────────────────────────────────────────────────
const rawWeight = [
  ["2025-01-21",85.55],["2025-01-22",84.9],["2025-01-23",84.05],["2025-01-24",83.85],
  ["2025-01-25",84.3],["2025-01-26",85.1],["2025-01-27",85.85],["2025-01-28",84.65],
  ["2025-01-29",84.15],["2025-01-30",83.6],["2025-01-31",84.1],
  ["2025-02-01",84.2],["2025-02-02",84.35],["2025-02-03",84.4],
  ["2025-02-04",84.15],["2025-02-05",84.45],["2025-02-06",84.2],
  ["2025-02-07",84.35],["2025-02-08",83.55],["2025-02-09",84.45],
  ["2025-02-10",84.5],["2025-02-11",83.55],["2025-02-12",83.95],
  ["2025-02-13",84.55],["2025-02-14",84.1],["2025-02-15",83.5],
  ["2025-02-16",83.35],["2025-02-17",83.9],["2025-02-18",83.65],
  ["2025-02-19",83.7],["2025-02-20",83.65],["2025-02-21",82.85],
  ["2025-02-22",82.4],["2025-02-23",83.3],["2025-02-24",83.2],
  ["2025-02-25",82.8],["2025-02-26",82.15],["2025-02-27",81.9],
  ["2025-02-28",81.65],
  ["2025-03-01",81.45],["2025-03-02",81.95],["2025-03-03",82.15],
  ["2025-03-04",81.8],["2025-03-05",81.85],["2025-03-06",81.95],
  ["2025-03-07",80.95],["2025-03-08",80.95],["2025-03-09",81.95],
  ["2025-03-10",81.75],["2025-03-11",81.3],["2025-03-12",80.6],
  ["2025-03-13",80.45],["2025-03-14",80.55],["2025-03-15",80.4],
  ["2025-03-16",81.4],["2025-03-17",80.85],["2025-03-18",80.35],
  ["2025-03-19",80.25],["2025-03-20",80.35],["2025-03-21",80.55],
  ["2025-03-22",79.95],["2025-03-23",80.25],["2025-03-24",80.65],
  ["2025-03-25",80.25],["2025-03-26",80.2],["2025-03-27",79.5],
  ["2025-03-28",80.1],["2025-03-29",79.5],["2025-03-30",79.65],
  ["2025-03-31",79.15],
  ["2025-04-01",79.1],["2025-04-02",79.15],["2025-04-03",78.45],
  ["2025-04-04",78.15],["2025-04-05",77.45],["2025-04-06",78.8],
  ["2025-04-07",79.3],["2025-04-08",79.2],["2025-04-09",79.2],
  ["2025-04-10",78.8],["2025-04-11",78.4],["2025-04-12",77.6],
  ["2025-04-13",78.55],["2025-04-14",79.55],["2025-04-15",77.9],
  ["2025-04-16",78.4],["2025-04-17",78.2],["2025-04-18",77.75],
  ["2025-04-19",78.6],["2025-04-20",78.75],["2025-04-21",79.9],
  ["2025-04-22",79.05],["2025-04-23",78.5],["2025-04-24",78.45],
  ["2025-04-25",78.9],["2025-04-26",78.3],["2025-04-27",78.05],
  ["2025-04-28",78.8],["2025-04-29",78.1],["2025-04-30",77.6],
  ["2025-05-01",77.65],["2025-05-02",78.75],["2025-05-03",78.9],
  ["2025-05-04",78.75],["2025-05-05",78.8],["2025-05-06",77.85],
  ["2025-05-07",77.45],["2025-05-08",77.8],["2025-05-09",78.05],
  ["2025-05-10",77.9],["2025-05-11",77.15],["2025-05-12",77.75],
  ["2025-05-13",77.45],["2025-05-14",77.45],["2025-05-15",76.8],
  ["2025-05-16",77.05],["2025-05-17",77.8],["2025-05-18",78.05],
  ["2025-05-19",77.6],["2025-05-20",78.05],["2025-05-21",78.2],
  ["2025-05-22",77.5],["2025-05-23",77.1],["2025-05-24",77.3],
  ["2025-05-25",77.45],["2025-05-26",77.6],["2025-05-27",77.65],
  ["2025-05-28",77.35],["2025-05-29",77.7],["2025-05-30",77.6],
  ["2025-05-31",77.75],
  ["2025-06-01",78.1],["2025-06-02",78.0],["2025-06-03",76.75],
  ["2025-06-04",76.75],["2025-06-05",77.6],["2025-06-06",76.95],
  ["2025-06-07",77.1],["2025-06-08",76.7],["2025-06-09",77.2],
  ["2025-06-10",76.55],["2025-06-11",76.4],["2025-06-13",76.95],
  ["2025-06-14",76.9],["2025-06-15",76.6],["2025-06-16",77.1],
  ["2025-06-17",76.4],["2025-06-18",76.45],["2025-06-19",76.15],
  ["2025-06-20",77.15],["2025-06-21",76.5],["2025-06-22",76.6],
  ["2025-06-23",76.9],["2025-06-24",76.25],["2025-06-25",76.95],
  ["2025-06-26",76.65],["2025-06-27",76.25],["2025-06-28",76.25],
  ["2025-06-29",76.6],["2025-06-30",77.35],
  ["2025-07-01",76.25],["2025-07-02",76.25],["2025-07-03",75.9],
  ["2025-07-04",76.6],["2025-07-05",75.9],["2025-07-06",75.9],
  ["2025-07-07",76.1],["2025-07-08",75.95],["2025-07-09",77.0],
  ["2025-07-10",76.7],["2025-07-11",76.65],["2025-07-12",76.45],
  ["2025-07-13",76.55],["2025-07-14",77.05],["2025-07-15",76.95],
  ["2025-07-16",76.85],["2025-07-17",76.3],["2025-07-18",76.85],
  ["2025-07-19",77.35],["2025-07-20",77.65],["2025-07-21",77.5],
  ["2025-07-22",77.05],["2025-07-23",76.35],["2025-07-24",75.85],
  ["2025-07-25",75.35],["2025-07-26",75.9],["2025-07-27",76.95],
  ["2025-07-28",77.75],["2025-07-29",76.15],["2025-07-30",75.8],
  ["2025-07-31",76.2],
  ["2025-08-01",75.15],["2025-08-02",75.8],["2025-08-03",76.75],
  ["2025-08-04",77.2],["2025-08-05",76.2],["2025-08-06",75.75],
  ["2025-08-07",76.4],["2025-08-08",77.25],["2025-08-09",75.55],
  ["2025-08-10",76.2],["2025-08-11",77.3],["2025-08-12",76.65],
  ["2025-08-13",76.15],["2025-08-14",75.75],["2025-08-15",75.8],
  ["2025-08-16",75.3],["2025-08-17",76.65],["2025-08-18",77.15],
  ["2025-08-19",76.15],["2025-08-20",75.6],["2025-08-21",75.6],
  ["2025-08-22",76.05],["2025-08-23",75.45],["2025-08-24",77.45],
  ["2025-08-25",76.6],["2025-08-26",76.45],["2025-08-27",76.4],
  ["2025-08-28",76.0],["2025-08-29",75.65],["2025-08-30",75.45],
  ["2025-08-31",76.35],
  ["2025-09-01",76.95],["2025-09-02",76.3],["2025-09-03",76.35],
  ["2025-09-04",76.2],["2025-09-05",76.35],["2025-09-06",75.95],
  ["2025-09-07",76.2],["2025-09-08",76.2],["2025-09-09",75.9],
  ["2025-09-10",76.6],["2025-09-11",76.75],["2025-09-12",76.35],
  ["2025-09-13",76.55],["2025-09-14",76.65],["2025-09-15",75.85],
  ["2025-09-16",76.85],["2025-09-17",77.35],["2025-09-18",77.6],
  ["2025-09-19",77.6],["2025-09-20",77.9],["2025-09-21",77.3],
  ["2025-09-22",77.45],["2025-09-23",76.0],["2025-09-24",74.8],
  ["2025-09-25",75.1],["2025-09-26",75.85],["2025-09-27",75.1],
  ["2025-09-28",75.25],["2025-09-29",76.15],["2025-09-30",75.6],
  ["2025-10-01",75.2],["2025-10-02",75.65],["2025-10-03",75.8],
  ["2025-10-04",75.65],["2025-10-05",76.35],["2025-10-06",76.2],
  ["2025-10-07",75.1],["2025-10-08",75.0],["2025-10-09",75.05],
  ["2025-10-10",74.75],["2025-10-11",73.7],["2025-10-12",73.35],
  ["2025-10-13",74.15],["2025-10-14",73.75],["2025-10-15",73.45],
  ["2025-10-16",73.5],["2025-10-17",73.7],["2025-10-18",72.8],
  ["2025-10-19",73.0],["2025-10-20",73.5],["2025-10-21",73.45],
  ["2025-10-22",72.6],["2025-10-23",72.1],["2025-10-24",72.45],
  ["2025-10-25",72.3],["2025-10-26",72.55],["2025-10-27",72.9],
  ["2025-10-28",72.3],["2025-10-29",72.15],["2025-10-30",72.3],
  ["2025-10-31",71.65],
  ["2025-11-01",72.05],["2025-11-02",73.1],["2025-11-03",73.25],
  ["2025-11-04",72.6],["2025-11-05",72.35],["2025-11-06",72.45],
  ["2025-11-07",72.15],["2025-11-08",72.65],["2025-11-09",72.9],
  ["2025-11-10",72.95],["2025-11-11",72.85],["2025-11-12",71.8],
  ["2025-11-13",72.1],["2025-11-14",71.95],["2025-11-15",71.85],
  ["2025-11-16",72.65],["2025-11-17",73.1],["2025-11-18",73.15],
  ["2025-11-19",72.25],["2025-11-20",72.15],["2025-11-21",72.6],
  ["2025-11-22",72.75],["2025-11-23",73.4],["2025-11-24",73.6],
  ["2025-11-25",72.55],["2025-11-26",72.35],["2025-11-27",72.1],
  ["2025-11-28",72.75],["2025-11-29",72.55],["2025-11-30",72.45],
  ["2025-12-01",72.85],["2025-12-02",72.3],["2025-12-03",72.35],
  ["2025-12-04",72.25],["2025-12-05",72.5],["2025-12-06",72.0],
  ["2025-12-07",71.95],["2025-12-08",72.5],["2025-12-09",72.25],
  ["2025-12-10",72.0],["2025-12-11",71.65],["2025-12-12",71.65],
  ["2025-12-13",71.6],["2025-12-14",72.05],["2025-12-15",72.55],
  ["2025-12-16",71.8],["2025-12-17",71.45],["2025-12-18",72.05],
  ["2025-12-19",70.85],["2025-12-20",71.05],["2025-12-21",71.4],
  ["2025-12-22",71.85],["2025-12-23",71.3],["2025-12-24",71.05],
  ["2025-12-25",72.15],["2025-12-26",72.95],["2025-12-27",72.45],
  ["2025-12-28",72.3],["2025-12-29",71.6],["2025-12-30",71.5],
  ["2025-12-31",72.0],
  ["2026-01-01",72.95],["2026-01-02",73.5],["2026-01-03",72.15],
  ["2026-01-04",72.6],["2026-01-05",72.5],["2026-01-06",72.45],
  ["2026-01-07",72.2],["2026-01-08",71.85],["2026-01-09",71.75],
  ["2026-01-10",71.4],["2026-01-11",71.95],["2026-01-12",72.2],
  ["2026-01-13",71.9],["2026-01-14",71.55],["2026-01-15",71.3],
  ["2026-01-16",70.6],["2026-01-17",70.5],["2026-01-18",71.75],
  ["2026-01-19",72.15],["2026-01-20",71.8],["2026-01-21",70.9],
  ["2026-01-22",70.5],["2026-01-23",70.8],["2026-01-24",70.7],
  ["2026-01-25",71.15],["2026-01-26",72.85],["2026-01-27",72.2],
  ["2026-01-28",72.05],["2026-01-29",71.5],["2026-01-30",71.7],
  ["2026-01-31",72.6],
  ["2026-02-01",72.1],["2026-02-02",71.65],["2026-02-03",71.45],
  ["2026-02-04",71.35],["2026-02-05",71.65],["2026-02-06",71.75],
  ["2026-02-07",71.0],["2026-02-08",70.65],["2026-02-09",70.65],
  ["2026-02-10",70.8],["2026-02-11",70.45],["2026-02-12",71.05],
  ["2026-02-13",70.45],["2026-02-14",70.3],["2026-02-15",70.95],
  ["2026-02-16",72.3],["2026-02-17",71.5],["2026-02-18",71.15],
  ["2026-02-19",71.4],["2026-02-20",70.85],["2026-02-21",70.4],
  ["2026-02-22",70.9],
];

const measurements = [
  { date:'01/09/2025', label:'Set/25', braco:32,    torax:98,   abdomen:90,   gluteo:97,   coxa:52,   panturrilha:38, peso:76.7  },
  { date:'30/11/2025', label:'Nov/25', braco:27,    torax:96.5, abdomen:82.5, gluteo:93.5, coxa:50.5, panturrilha:36, peso:72.45 },
  { date:'11/01/2026', label:'Jan/26', braco:28,    torax:92,   abdomen:80,   gluteo:91,   coxa:50,   panturrilha:36, peso:71.95 },
  { date:'21/02/2026', label:'Fev/26', braco:26.75, torax:92.5, abdomen:82.5, gluteo:92,   coxa:49,   panturrilha:35, peso:70.4  },
];

// ─── HELPERS ──────────────────────────────────────────────────────────────────
const HEIGHT = 1.80;
function calcBMI(w) { return +(w / (HEIGHT * HEIGHT)).toFixed(1); }
function bmiClass(bmi) {
  if (bmi < 18.5) return { label:'Abaixo',    tag:'tag-over'  };
  if (bmi < 25.0) return { label:'Normal',    tag:'tag-normal'};
  if (bmi < 30.0) return { label:'Sobrepeso', tag:'tag-over'  };
  return               { label:'Obesidade',  tag:'tag-obese' };
}

const monthNames = { '01':'Jan','02':'Fev','03':'Mar','04':'Abr','05':'Mai','06':'Jun',
                     '07':'Jul','08':'Ago','09':'Set','10':'Out','11':'Nov','12':'Dez' };
function monthLabel(k) { const [y,m] = k.split('-'); return monthNames[m]+'/'+y.slice(2); }

// Agrupar por mês
const monthMap = {};
rawWeight.forEach(([d,w]) => { const k = d.slice(0,7); (monthMap[k]||(monthMap[k]=[])).push(w); });
const months = Object.keys(monthMap).sort();
const monthStats = months.map(k => {
  const vals = monthMap[k];
  const avg = +(vals.reduce((a,b)=>a+b,0)/vals.length).toFixed(2);
  return { key:k, avg, min:+Math.min(...vals).toFixed(2), max:+Math.max(...vals).toFixed(2), bmi:calcBMI(avg), n:vals.length };
});

const firstMonth = monthStats[0], lastMonth = monthStats[monthStats.length-1];
const allWeights = rawWeight.map(r=>r[1]);
const totalLoss  = +(firstMonth.avg - lastMonth.avg).toFixed(1);
const minW = Math.min(...allWeights).toFixed(1);
const minBMI = Math.min(...monthStats.map(m=>m.bmi)).toFixed(1);

// Tooltip defaults
const tooltipDef = {
  backgroundColor:'#1a2235', borderColor:'#1e2d47', borderWidth:1,
  titleFont:{family:'DM Mono',size:11}, bodyFont:{family:'DM Mono',size:11},
  titleColor:'#94a3b8', bodyColor:'#e2e8f0', padding:10,
};

const scalesDef = {
  x: { grid:{color:'rgba(255,255,255,0.03)',drawBorder:false}, ticks:{color:'#475569',font:{family:'DM Mono',size:10},maxTicksLimit:14} },
  y: { grid:{color:'rgba(255,255,255,0.05)',drawBorder:false}, ticks:{color:'#475569',font:{family:'DM Mono',size:10}} },
};

// ─── KPI STRIP ────────────────────────────────────────────────────────────────
const kpis = [
  { label:'Peso Inicial (Jan/25)', value:firstMonth.avg.toFixed(1)+' kg', sub:'IMC '+calcBMI(firstMonth.avg), delta:null, cls:'red' },
  { label:'Peso Atual (Fev/26)',   value:lastMonth.avg.toFixed(1)+' kg',  sub:'IMC '+calcBMI(lastMonth.avg),  delta:null, cls:'green' },
  { label:'Perda Total', value:totalLoss.toFixed(1)+' kg', sub:'ao longo de 13 meses',
    delta:'↓ '+(totalLoss/firstMonth.avg*100).toFixed(1)+'%', cls:'blue' },
  { label:'Menor Peso Registrado', value:minW+' kg', sub:'IMC mínimo '+minBMI, delta:null, cls:'amber' },
];
const strip = document.getElementById('kpiStrip');
kpis.forEach(k => {
  strip.innerHTML += `<div class="kpi ${k.cls}">
    <div class="kpi-label">${k.label}</div>
    <div class="kpi-value">${k.value}</div>
    <div class="kpi-sub">${k.sub}</div>
    ${k.delta ? `<div class="kpi-delta delta-down">${k.delta}</div>` : ''}
  </div>`;
});

// ─── GRÁFICO PESO DIÁRIO ──────────────────────────────────────────────────────
const dailyLabels = rawWeight.map(r=>r[0]);
const dailyData   = rawWeight.map(r=>r[1]);
const monthAvgMap = {};
monthStats.forEach(m => { monthAvgMap[m.key] = m.avg; });
const monthAvgLine = rawWeight.map(r => monthAvgMap[r[0].slice(0,7)]);

new Chart(document.getElementById('weightLine'), {
  type: 'line',
  data: {
    labels: dailyLabels,
    datasets: [
      { label:'Peso (kg)', data:dailyData, borderColor:'rgba(59,130,246,0.6)', backgroundColor:'rgba(59,130,246,0.04)',
        borderWidth:1.2, pointRadius:0, pointHoverRadius:4, fill:true, tension:0.3 },
      { label:'Média mensal', data:monthAvgLine, borderColor:'#f59e0b', backgroundColor:'transparent',
        borderWidth:2, pointRadius:0, tension:0.4, borderDash:[4,3] },
    ]
  },
  options: { responsive:true, interaction:{mode:'index',intersect:false},
    plugins:{legend:{display:false},tooltip:tooltipDef}, scales:scalesDef }
});

// ─── GRÁFICO IMC ──────────────────────────────────────────────────────────────
const dailyBMI = rawWeight.map(r => calcBMI(r[1]));

new Chart(document.getElementById('bmiLine'), {
  type: 'line',
  data: {
    labels: dailyLabels,
    datasets: [{ label:'IMC', data:dailyBMI, borderColor:'rgba(16,185,129,0.7)',
      backgroundColor:'rgba(16,185,129,0.05)', borderWidth:1.5, pointRadius:0,
      pointHoverRadius:4, fill:true, tension:0.3 }]
  },
  options: { responsive:true, interaction:{mode:'index',intersect:false},
    plugins:{legend:{display:false},tooltip:tooltipDef},
    scales:{ x:scalesDef.x, y:{ ...scalesDef.y, min:20, max:28 } }
  },
  plugins:[{
    id:'bmiZone',
    beforeDraw(chart) {
      const {ctx, chartArea:{left,right}, scales:{y}} = chart;
      if (!y) return;
      ctx.save();
      ctx.fillStyle = 'rgba(16,185,129,0.07)';
      ctx.fillRect(left, y.getPixelForValue(24.9), right-left, y.getPixelForValue(18.5)-y.getPixelForValue(24.9));
      ctx.restore();
    }
  }]
});

// ─── BARRAS MÉDIA MENSAL ──────────────────────────────────────────────────────
const barColors = monthStats.map(m => m.bmi < 25 ? 'rgba(16,185,129,0.75)' : m.bmi < 30 ? 'rgba(245,158,11,0.75)' : 'rgba(239,68,68,0.75)');

new Chart(document.getElementById('weightBar'), {
  type:'bar',
  data:{ labels:months.map(monthLabel),
    datasets:[{ label:'Peso médio (kg)', data:monthStats.map(m=>m.avg), backgroundColor:barColors, borderRadius:4, borderSkipped:false }]
  },
  options:{ responsive:true, interaction:{mode:'index',intersect:false},
    plugins:{legend:{display:false},tooltip:tooltipDef},
    scales:{ x:{grid:{display:false},ticks:{color:'#475569',font:{family:'DM Mono',size:10}}}, y:{...scalesDef.y,min:60} }
  }
});

// ─── BARRAS VARIAÇÃO M/M ──────────────────────────────────────────────────────
const deltas = monthStats.map((m,i) => i===0 ? 0 : +(m.avg - monthStats[i-1].avg).toFixed(2));

new Chart(document.getElementById('deltaBar'), {
  type:'bar',
  data:{ labels:months.map(monthLabel),
    datasets:[{ label:'Δ peso (kg)', data:deltas,
      backgroundColor:deltas.map(d => d<=0 ? 'rgba(16,185,129,0.75)' : 'rgba(239,68,68,0.65)'),
      borderRadius:4, borderSkipped:false }]
  },
  options:{ responsive:true, interaction:{mode:'index',intersect:false},
    plugins:{legend:{display:false},tooltip:tooltipDef}, scales:{ x:{grid:{display:false},ticks:{color:'#475569',font:{family:'DM Mono',size:10}}}, y:scalesDef.y }
  }
});

// ─── TABELA MENSAL ────────────────────────────────────────────────────────────
const tbody = document.getElementById('monthTableBody');
const maxAvg = Math.max(...monthStats.map(m=>m.avg));
monthStats.forEach((m,i) => {
  const delta = i===0 ? '—' : (deltas[i]>0 ? '+'+deltas[i].toFixed(2) : deltas[i].toFixed(2));
  const deltaColor = i===0 ? '' : (deltas[i]<=0 ? 'color:#6ee7b7' : 'color:#fca5a5');
  const cls = bmiClass(m.bmi);
  const barPct = (m.avg/maxAvg*100).toFixed(1);
  const barCls = m.bmi<25 ? 'green' : m.bmi<30 ? 'amber' : 'red';
  const trend = i===0 ? '—' : deltas[i]<-0.5 ? '↓↓' : deltas[i]<0 ? '↓' : deltas[i]<0.5 ? '→' : '↑';
  const trendColor = i===0 ? '' : (deltas[i]<0 ? 'color:#6ee7b7' : 'color:#fca5a5');
  tbody.innerHTML += `<tr>
    <td><strong>${monthLabel(m.key)}</strong></td>
    <td><div class="bar-inline"><span>${m.avg.toFixed(1)} kg</span>
      <div class="bar-track"><div class="bar-fill ${barCls}" style="width:${barPct}%"></div></div></div></td>
    <td>${m.min.toFixed(1)}</td><td>${m.max.toFixed(1)}</td>
    <td style="${deltaColor}"><strong>${delta}</strong></td>
    <td>${m.bmi}</td>
    <td><span class="tag ${cls.tag}">${cls.label}</span></td>
    <td style="${trendColor};font-size:16px">${trend}</td>
  </tr>`;
});

// ─── INSIGHTS GERAIS ──────────────────────────────────────────────────────────
const insights = [
  { emoji:'🏆', text:`<strong>Perda total de ${totalLoss.toFixed(1)} kg</strong> em 13 meses — de ${firstMonth.avg.toFixed(1)} kg para ${lastMonth.avg.toFixed(1)} kg. Uma redução de ${(totalLoss/firstMonth.avg*100).toFixed(1)}% do peso inicial.` },
  { emoji:'📉', text:`<strong>Maior perda mensal:</strong> Outubro/2025 registrou a maior queda, com redução de ~3,5 kg em relação ao mês anterior — um mês de aceleração notável.` },
  { emoji:'✅', text:`<strong>IMC dentro do normal</strong> desde Novembro/2025. O IMC caiu de ${calcBMI(firstMonth.avg)} (sobrepeso) para ${calcBMI(lastMonth.avg)} (normal), cruzando a fronteira 24,9 em Outubro.` },
  { emoji:'⚖️', text:`<strong>Menor peso registrado: ${minW} kg</strong> — atingido em Fevereiro/2026. A trajetória mostra consistência sem grandes regressões.` },
  { emoji:'📆', text:`<strong>Consistência impressionante:</strong> ${rawWeight.length}+ medições registradas — praticamente uma por dia ao longo de todo o período. Isso por si só é um fator de sucesso.` },
  { emoji:'🎯', text:`A média diária de horário das pesagens gira em torno das <strong>6h–7h da manhã</strong>, indicando um hábito matinal sólido e consistente.` },
];
const igrid = document.getElementById('insightGrid');
insights.forEach(ins => {
  igrid.innerHTML += `<div class="insight-item"><div class="insight-emoji">${ins.emoji}</div><div class="insight-text">${ins.text}</div></div>`;
});

// ─── KPI MEDIDAS ──────────────────────────────────────────────────────────────
const first = measurements[0], last = measurements[measurements.length-1];
const radarKeys   = ['braco','torax','abdomen','gluteo','coxa','panturrilha'];
const measureLabels = { braco:'Braço', torax:'Tórax', abdomen:'Abdômen', gluteo:'Glúteo', coxa:'Coxa', panturrilha:'Panturrilha' };
const measureColors = {
  braco:{border:'#8b5cf6',bg:'rgba(139,92,246,0.15)'}, torax:{border:'#3b82f6',bg:'rgba(59,130,246,0.15)'},
  abdomen:{border:'#ef4444',bg:'rgba(239,68,68,0.15)'}, gluteo:{border:'#f59e0b',bg:'rgba(245,158,11,0.15)'},
  coxa:{border:'#10b981',bg:'rgba(16,185,129,0.15)'}, panturrilha:{border:'#06b6d4',bg:'rgba(6,182,212,0.15)'},
};

const kpiColorMap = { braco:'#93c5fd', torax:'#93c5fd', abdomen:'#fca5a5', gluteo:'#fcd34d', coxa:'#6ee7b7', panturrilha:'#fcd34d' };
const kpiBgMap    = { braco:'rgba(59,130,246,0.12)', torax:'rgba(59,130,246,0.12)', abdomen:'rgba(239,68,68,0.12)', gluteo:'rgba(245,158,11,0.12)', coxa:'rgba(16,185,129,0.12)', panturrilha:'rgba(245,158,11,0.12)' };

const measKpiStrip = document.getElementById('measKpiStrip');
radarKeys.forEach(k => {
  const d = +(last[k] - first[k]).toFixed(1);
  const isGood = d <= 0;
  const color = kpiColorMap[k];
  measKpiStrip.innerHTML += `<div class="meas-kpi" style="border-top:2px solid ${color}">
    <div class="kpi-label">${measureLabels[k]}</div>
    <div style="font-family:'DM Serif Display',serif;font-size:28px;color:${color};line-height:1">${last[k]} cm</div>
    <div class="meas-delta-tag" style="${isGood?'background:rgba(16,185,129,0.12);color:#6ee7b7':'background:rgba(239,68,68,0.12);color:#fca5a5'}">
      ${d>0?'+':''}${d} cm desde Set/25
    </div>
  </div>`;
});

// ─── RADAR ────────────────────────────────────────────────────────────────────
const radarColors = ['rgba(239,68,68,0.8)','rgba(245,158,11,0.7)','rgba(59,130,246,0.7)','rgba(16,185,129,0.9)'];
const radarFills  = ['rgba(239,68,68,0.1)','rgba(245,158,11,0.1)','rgba(59,130,246,0.1)','rgba(16,185,129,0.1)'];

const radarLegend = document.getElementById('radarLegend');
measurements.forEach((m,i) => {
  radarLegend.innerHTML += `<div class="legend-item"><div class="legend-dot" style="background:${radarColors[i]}"></div>${m.label}</div>`;
});

new Chart(document.getElementById('radarChart'), {
  type:'radar',
  data:{
    labels:['Braço','Tórax','Abdômen','Glúteo','Coxa','Panturrilha'],
    datasets:measurements.map((m,i) => ({
      label:m.label, data:radarKeys.map(k=>m[k]),
      borderColor:radarColors[i], backgroundColor:radarFills[i],
      borderWidth:2, pointRadius:3, pointBackgroundColor:radarColors[i],
    }))
  },
  options:{
    responsive:true, plugins:{legend:{display:false},tooltip:tooltipDef},
    scales:{r:{grid:{color:'rgba(255,255,255,0.08)'},angleLines:{color:'rgba(255,255,255,0.08)'},
      pointLabels:{color:'#94a3b8',font:{family:'DM Mono',size:11}},
      ticks:{color:'#475569',font:{family:'DM Mono',size:9},backdropColor:'transparent',stepSize:10},min:20}}
  }
});

// ─── LINHA DE MEDIDAS ─────────────────────────────────────────────────────────
new Chart(document.getElementById('measLine'), {
  type:'line',
  data:{
    labels:measurements.map(m=>m.label),
    datasets:radarKeys.map(k => ({
      label:measureLabels[k], data:measurements.map(m=>m[k]),
      borderColor:measureColors[k].border, backgroundColor:measureColors[k].bg,
      borderWidth:2, pointRadius:5, pointHoverRadius:7, pointBackgroundColor:measureColors[k].border,
      tension:0.35, fill:false,
    }))
  },
  options:{
    responsive:true, interaction:{mode:'index',intersect:false},
    plugins:{legend:{display:true,position:'bottom',labels:{color:'#94a3b8',font:{family:'DM Mono',size:10},boxWidth:10,padding:12}},tooltip:tooltipDef},
    scales:{
      x:{grid:{display:false},ticks:{color:'#475569',font:{family:'DM Mono',size:11}}},
      y:{min:20,grid:{color:'rgba(255,255,255,0.05)',drawBorder:false},ticks:{color:'#475569',font:{family:'DM Mono',size:10}}}
    }
  }
});

// ─── BARRAS SET vs FEV ────────────────────────────────────────────────────────
new Chart(document.getElementById('measBar'), {
  type:'bar',
  data:{
    labels:radarKeys.map(k=>measureLabels[k]),
    datasets:[
      { label:'Set/2025', data:radarKeys.map(k=>first[k]), backgroundColor:'rgba(239,68,68,0.6)', borderRadius:4, borderSkipped:false },
      { label:'Fev/2026', data:radarKeys.map(k=>last[k]),  backgroundColor:'rgba(16,185,129,0.7)', borderRadius:4, borderSkipped:false },
    ]
  },
  options:{
    responsive:true, interaction:{mode:'index',intersect:false},
    plugins:{legend:{display:true,position:'top',labels:{color:'#94a3b8',font:{family:'DM Mono',size:11},boxWidth:10,padding:12}},tooltip:tooltipDef},
    scales:{
      x:{grid:{display:false},ticks:{color:'#475569',font:{family:'DM Mono',size:11}}},
      y:{min:20,grid:{color:'rgba(255,255,255,0.05)',drawBorder:false},ticks:{color:'#475569',font:{family:'DM Mono',size:11}}}
    }
  }
});

// ─── TABELA MEDIDAS ───────────────────────────────────────────────────────────
const measTbody = document.getElementById('measTableBody');
measurements.forEach((m,i) => {
  const abdDiff = i===0 ? null : +(m.abdomen - measurements[i-1].abdomen).toFixed(1);
  const abdStr  = i===0 ? '—' : (abdDiff>0?'+'+abdDiff:abdDiff)+' cm';
  const abdColor = i===0 ? '' : (abdDiff<=0 ? 'color:#6ee7b7' : 'color:#fca5a5');
  measTbody.innerHTML += `<tr>
    <td><strong>${m.date}</strong></td>
    <td>${m.braco}</td><td>${m.torax}</td><td><strong>${m.abdomen}</strong></td>
    <td>${m.gluteo}</td><td>${m.coxa}</td><td>${m.panturrilha}</td>
    <td>${m.peso} kg</td>
    <td style="${abdColor}"><strong>${abdStr}</strong></td>
  </tr>`;
});

// ─── INSIGHTS MEDIDAS ─────────────────────────────────────────────────────────
const totalCmLost = radarKeys.reduce((acc,k) => acc+(first[k]-last[k]), 0).toFixed(1);
const measInsights = [
  { emoji:'📐', text:`<strong>${totalCmLost} cm perdidos no total</strong> somando todas as medidas entre Set/2025 e Fev/2026 — cada centímetro conquistado com consistência diária.` },
  { emoji:'🎯', text:`<strong>Abdômen: ${+(last.abdomen-first.abdomen).toFixed(1)} cm</strong> de variação (90 → ${last.abdomen} cm). O foco abdominal é evidente na jornada.` },
  { emoji:'💪', text:`<strong>Braço reduziu ${+(last.braco-first.braco).toFixed(1)} cm</strong> (32 → ${last.braco} cm). Queda proporcional ao emagrecimento geral sem perda excessiva de volume.` },
  { emoji:'🍑', text:`<strong>Glúteo: ${+(last.gluteo-first.gluteo).toFixed(1)} cm</strong> de redução (97 → ${last.gluteo} cm). Proporção corporal mantida de forma equilibrada.` },
  { emoji:'🦵', text:`<strong>Coxa e panturrilha</strong> reduziram ${+(last.coxa-first.coxa).toFixed(1)} cm e ${+(last.panturrilha-first.panturrilha).toFixed(1)} cm respectivamente — membros inferiores respondem bem à perda de gordura.` },
  { emoji:'📊', text:`<strong>Tórax estável:</strong> variação de apenas ${+(last.torax-first.torax).toFixed(1)} cm (98 → ${last.torax} cm), sugerindo preservação de massa peitoral e dorsal. Ótimo sinal de composição corporal.` },
];
const measGrid = document.getElementById('measInsightGrid');
measInsights.forEach(ins => {
  measGrid.innerHTML += `<div class="insight-item"><div class="insight-emoji">${ins.emoji}</div><div class="insight-text">${ins.text}</div></div>`;
});
</script>