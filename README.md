<!doctype html>
<html lang="es">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>Sohersa BIM | Dashboard - Diseño Ingenierías Colón GDL</title>

  <style>
    /* ====== Modern enterprise tokens ====== */
    :root {
      --sohersa-green: #69B23C;
      --sohersa-green-700: #2F8A2E;
      --sohersa-blue-950: #07162B;
      --sohersa-blue-900: #0B1F3B;
      --sohersa-blue-700: #123A6B;
      --sohersa-blue-200: #CFE0FF;

      --bg0: #060B12;
      --bg1: #0B1220;
      --panel: rgba(255,255,255,0.06);
      --panel-strong: rgba(255,255,255,0.10);
      --stroke: rgba(255,255,255,0.10);
      --stroke2: rgba(255,255,255,0.14);

      --card: rgba(255,255,255,0.06);
      --card2: rgba(255,255,255,0.08);
      --text: rgba(255,255,255,0.92);
      --muted: rgba(255,255,255,0.68);
      --muted2: rgba(255,255,255,0.56);

      --ok: var(--sohersa-green);
      --warn: #F59E0B;
      --bad: #EF4444;
      --info: #60A5FA;

      --radius: 18px;
      --shadow: 0 18px 60px rgba(0,0,0,0.45);
      --shadow2: 0 10px 40px rgba(0,0,0,0.32);
      --maxw: 1280px;

      --font: ui-sans-serif, system-ui, -apple-system, Segoe UI, Roboto, Inter, Helvetica, Arial;
    }

    /* Light mode tokens (optional) */
    :root[data-theme="light"] {
      --bg0: #F6F8FC;
      --bg1: #EEF3FA;
      --panel: rgba(11,31,59,0.04);
      --panel-strong: rgba(11,31,59,0.06);
      --stroke: rgba(11,31,59,0.10);
      --stroke2: rgba(11,31,59,0.14);

      --card: #FFFFFF;
      --card2: #FFFFFF;
      --text: #0F172A;
      --muted: #556070;
      --muted2: #6B7280;

      --shadow: 0 10px 28px rgba(15, 23, 42, 0.10);
      --shadow2: 0 8px 22px rgba(15, 23, 42, 0.08);
    }

    * { box-sizing: border-box; }
    html, body { height: 100%; }
    body {
      margin: 0;
      font-family: var(--font);
      color: var(--text);
      background:
        radial-gradient(900px 500px at 18% -10%, rgba(105,178,60,0.22), transparent 55%),
        radial-gradient(900px 600px at 90% 0%, rgba(18,58,107,0.26), transparent 54%),
        linear-gradient(180deg, var(--bg0), var(--bg1));
    }

    a { color: inherit; }
    .container {
      max-width: var(--maxw);
      margin: 0 auto;
      padding: 18px 18px 56px;
    }

    /* ====== Top app bar ====== */
    .appbar {
      position: sticky;
      top: 0;
      z-index: 60;
      backdrop-filter: blur(14px);
      background: linear-gradient(180deg, rgba(0,0,0,0.45), rgba(0,0,0,0.18));
      border-bottom: 1px solid var(--stroke);
    }
    :root[data-theme="light"] .appbar {
      background: linear-gradient(180deg, rgba(255,255,255,0.78), rgba(255,255,255,0.56));
    }
    .appbar-inner {
      max-width: var(--maxw);
      margin: 0 auto;
      padding: 14px 18px;
      display: flex;
      align-items: center;
      gap: 14px;
    }
    .logo {
      display: flex; align-items: center; gap: 12px;
      min-width: 220px;
    }
    .logo img { height: 34px; width: auto; display:block; }
    .meta {
      flex: 1;
      display: grid;
      gap: 3px;
      min-width: 260px;
    }
    .meta .title {
      font-weight: 850;
      letter-spacing: 0.2px;
      font-size: 14px;
      line-height: 1.15;
    }
    .meta .sub {
      font-size: 12px;
      color: var(--muted);
      line-height: 1.25;
    }
    .actions {
      display: flex;
      gap: 10px;
      align-items: center;
      justify-content: flex-end;
      flex-wrap: wrap;
    }
    .chip {
      display: inline-flex;
      align-items: center;
      gap: 8px;
      padding: 8px 10px;
      border-radius: 999px;
      background: var(--panel);
      border: 1px solid var(--stroke);
      color: var(--muted);
      font-size: 12px;
      white-space: nowrap;
    }
    .chip .dot {
      width: 8px; height: 8px; border-radius: 999px;
      background: var(--sohersa-green);
      box-shadow: 0 0 0 4px rgba(105,178,60,0.18);
    }
    .btn {
      border: 1px solid var(--stroke2);
      background: var(--panel-strong);
      color: var(--text);
      border-radius: 999px;
      padding: 8px 12px;
      font-size: 12px;
      cursor: pointer;
    }
    .btn:hover { border-color: var(--sohersa-blue-200); }

    /* ====== Layout: sidebar + content ====== */
    .layout {
      display: grid;
      grid-template-columns: 280px 1fr;
      gap: 14px;
      margin-top: 16px;
      align-items: start;
    }
    @media (max-width: 980px) {
      .layout { grid-template-columns: 1fr; }
    }

    .sidebar {
      position: sticky;
      top: 74px;
      border-radius: var(--radius);
      background: var(--panel);
      border: 1px solid var(--stroke);
      box-shadow: var(--shadow2);
      overflow: hidden;
    }
    @media (max-width: 980px) {
      .sidebar { position: relative; top: 0; }
    }
    .side-head {
      padding: 14px 14px;
      border-bottom: 1px solid var(--stroke);
      background: linear-gradient(180deg, rgba(18,58,107,0.18), transparent);
    }
    .side-head .h {
      font-weight: 850;
      font-size: 13px;
      letter-spacing: 0.2px;
    }
    .side-head .p {
      margin-top: 4px;
      font-size: 12px;
      color: var(--muted);
      line-height: 1.35;
    }
    .nav {
      padding: 10px;
      display: grid;
      gap: 6px;
    }
    .nav a {
      display: flex;
      align-items: center;
      justify-content: space-between;
      gap: 10px;
      padding: 10px 10px;
      border-radius: 12px;
      color: var(--text);
      text-decoration: none;
      border: 1px solid transparent;
    }
    .nav a:hover {
      background: rgba(105,178,60,0.10);
      border-color: rgba(105,178,60,0.22);
    }
    .nav .k {
      font-size: 12px;
      color: var(--muted);
      border: 1px solid var(--stroke);
      background: var(--panel);
      padding: 3px 8px;
      border-radius: 999px;
    }

    .content {
      display: grid;
      gap: 14px;
    }

    /* ====== Cards ====== */
    .card {
      border-radius: var(--radius);
      background: var(--card);
      border: 1px solid var(--stroke);
      box-shadow: var(--shadow2);
      overflow: hidden;
    }
    :root[data-theme="light"] .card {
      background: var(--card);
    }
    .card-head {
      padding: 14px 16px;
      border-bottom: 1px solid var(--stroke);
      display: flex;
      align-items: center;
      justify-content: space-between;
      gap: 10px;
      background: linear-gradient(180deg, rgba(18,58,107,0.14), transparent);
    }
    .card-head .t {
      display: flex;
      align-items: center;
      gap: 10px;
      font-weight: 900;
      font-size: 13px;
      letter-spacing: 0.2px;
    }
    .badge {
      font-size: 12px;
      color: var(--muted);
      border: 1px solid var(--stroke);
      background: var(--panel);
      padding: 5px 10px;
      border-radius: 999px;
      white-space: nowrap;
    }
    .card-body {
      padding: 14px 16px 16px;
    }

    /* ====== KPI ====== */
    .kpis {
      display: grid;
      grid-template-columns: repeat(4, 1fr);
      gap: 12px;
    }
    @media (max-width: 1060px) {
      .kpis { grid-template-columns: repeat(2, 1fr); }
    }
    @media (max-width: 560px) {
      .kpis { grid-template-columns: 1fr; }
    }
    .kpi {
      border: 1px solid var(--stroke);
      border-radius: 16px;
      padding: 12px 12px;
      background: linear-gradient(180deg, rgba(255,255,255,0.05), transparent);
    }
    :root[data-theme="light"] .kpi {
      background: linear-gradient(180deg, rgba(105,178,60,0.06), transparent);
    }
    .kpi .l {
      font-size: 12px;
      color: var(--muted);
    }
    .kpi .v {
      margin-top: 6px;
      font-size: 24px;
      font-weight: 950;
      letter-spacing: -0.3px;
    }
    .kpi .h {
      margin-top: 6px;
      font-size: 12px;
      color: var(--muted);
      line-height: 1.35;
    }

    /* ====== Split grids ====== */
    .grid2 {
      display: grid;
      grid-template-columns: 1fr 1fr;
      gap: 14px;
    }
    @media (max-width: 980px) {
      .grid2 { grid-template-columns: 1fr; }
    }

    /* ====== Pills / tags ====== */
    .tag {
      display: inline-flex;
      align-items: center;
      padding: 6px 10px;
      border-radius: 999px;
      font-size: 12px;
      color: var(--muted);
      border: 1px solid var(--stroke);
      background: var(--panel);
    }

    /* ====== Gantt ====== */
    .gantt-wrap {
      overflow: auto;
      border-radius: 16px;
      border: 1px solid var(--stroke);
      background: linear-gradient(180deg, rgba(255,255,255,0.04), transparent);
    }
    :root[data-theme="light"] .gantt-wrap {
      background: #fff;
    }
    .gantt {
      min-width: 980px;
      padding: 12px;
    }
    .g-header {
      display: grid;
      grid-template-columns: 280px 1fr 260px;
      gap: 10px;
      align-items: center;
      margin-bottom: 10px;
    }
    .g-header .left {
      font-size: 12px;
      color: var(--muted);
      font-weight: 700;
    }
    .weeks {
      display: grid;
      grid-template-columns: repeat(26, 1fr);
      gap: 0;
      border: 1px solid var(--stroke);
      border-radius: 12px;
      overflow: hidden;
      background: rgba(255,255,255,0.04);
    }
    .wk {
      font-size: 11px;
      color: var(--muted2);
      padding: 6px 0;
      text-align: center;
      border-right: 1px solid var(--stroke);
      background: rgba(18,58,107,0.08);
    }
    .wk:last-child { border-right: none; }

    .g-row {
      display: grid;
      grid-template-columns: 280px 1fr 260px;
      gap: 10px;
      align-items: stretch;
      padding: 10px 0;
      border-top: 1px solid var(--stroke);
    }
    .g-row:first-of-type { border-top: none; }
    .g-label {
      padding: 10px 12px;
      border: 1px solid var(--stroke);
      border-radius: 14px;
      background: var(--panel);
    }
    .g-name {
      font-weight: 900;
      font-size: 12px;
      line-height: 1.2;
    }
    .g-meta {
      margin-top: 6px;
      font-size: 12px;
      color: var(--muted);
    }
    .g-track {
      display: grid;
      grid-template-columns: repeat(26, 1fr);
      border: 1px solid var(--stroke);
      border-radius: 14px;
      overflow: hidden;
      background:
        repeating-linear-gradient(
          90deg,
          rgba(255,255,255,0.04),
          rgba(255,255,255,0.04) calc((100% / 26) - 1px),
          rgba(255,255,255,0.00) calc((100% / 26) - 1px),
          rgba(255,255,255,0.00) calc(100% / 26)
        );
      position: relative;
    }
    :root[data-theme="light"] .g-track {
      background:
        repeating-linear-gradient(
          90deg,
          rgba(11,31,59,0.06),
          rgba(11,31,59,0.06) calc((100% / 26) - 1px),
          rgba(11,31,59,0.00) calc((100% / 26) - 1px),
          rgba(11,31,59,0.00) calc(100% / 26)
        );
    }
    .g-bar {
      margin: 10px 6px;
      border-radius: 999px;
      display: flex;
      align-items: center;
      justify-content: flex-end;
      padding-right: 10px;
      color: rgba(255,255,255,0.92);
      font-size: 11px;
      font-weight: 800;
      letter-spacing: 0.15px;
      border: 1px solid rgba(255,255,255,0.16);
      box-shadow: 0 10px 22px rgba(0,0,0,0.28);
      min-height: 28px;
    }
    :root[data-theme="light"] .g-bar {
      color: #0F172A;
      border-color: rgba(11,31,59,0.12);
      box-shadow: 0 8px 18px rgba(15,23,42,0.12);
    }
    .g-bar.green {
      background: linear-gradient(90deg, rgba(47,138,46,0.95), rgba(105,178,60,0.95));
    }
    .g-bar.blue {
      background: linear-gradient(90deg, rgba(11,31,59,0.92), rgba(18,58,107,0.92));
    }
    .g-bar-text {
      opacity: 0.92;
    }
    .g-deliverables {
      display: flex;
      flex-wrap: wrap;
      align-content: start;
      gap: 8px;
      padding: 8px;
      border-radius: 14px;
      border: 1px solid var(--stroke);
      background: var(--panel);
    }


    /* ====== Org chart (explicit) ====== */
    .orgchart { display: grid; gap: 12px; }
    .org-level { display: grid; gap: 10px; justify-items: center; }
    .org-level.cols-3 { grid-template-columns: repeat(3, 1fr); justify-items: stretch; }
    .org-level.cols-2 { grid-template-columns: repeat(2, 1fr); justify-items: stretch; }
    @media (max-width: 980px) { .org-level.cols-3, .org-level.cols-2 { grid-template-columns: 1fr; } }

    .org-connector { height: 14px; border-left: 2px solid rgba(105,178,60,0.55); margin: 0 auto; width: 0; filter: drop-shadow(0 6px 10px rgba(0,0,0,0.25)); }
    :root[data-theme="light"] .org-connector { border-left-color: rgba(47,138,46,0.55); filter: none; }

    .node { border-radius: 18px; padding: 14px; border: 1px solid var(--stroke); background: linear-gradient(180deg, rgba(255,255,255,0.06), transparent); box-shadow: var(--shadow2); min-height: 112px; }
    :root[data-theme="light"] .node { background: #fff; }
    .node.primary { border-color: rgba(105,178,60,0.35); background: linear-gradient(180deg, rgba(105,178,60,0.16), rgba(255,255,255,0.04)); }
    :root[data-theme="light"] .node.primary { background: linear-gradient(180deg, rgba(105,178,60,0.10), #fff); }
    .node.emphasis { border-color: rgba(105,178,60,0.30); background: linear-gradient(180deg, rgba(18,58,107,0.14), transparent); }

    .node-title { font-weight: 950; font-size: 13px; letter-spacing: 0.15px; line-height: 1.25; }
    .node-sub { margin-top: 6px; font-size: 12px; color: var(--muted); line-height: 1.45; }
    .node-meta { margin-top: 10px; font-size: 12px; color: var(--muted2); line-height: 1.45; }

    .note { margin-top: 10px; font-size: 12px; color: var(--muted); line-height: 1.55; }

    /* ====== Lists ====== */
    .list {
      display: grid;
      gap: 10px;
    }
    .item {
      display: flex;
      align-items: flex-start;
      justify-content: space-between;
      gap: 12px;
      padding: 12px;
      border-radius: 16px;
      border: 1px solid var(--stroke);
      background: var(--panel);
    }
    :root[data-theme="light"] .item {
      background: #fff;
    }
    .item .tt {
      font-weight: 900;
      font-size: 13px;
    }
    .item .ss {
      margin-top: 4px;
      font-size: 12px;
      color: var(--muted);
      line-height: 1.45;
    }
    .status {
      display: inline-flex;
      align-items: center;
      gap: 8px;
      border: 1px solid var(--stroke2);
      background: var(--panel-strong);
      padding: 6px 10px;
      border-radius: 999px;
      font-size: 12px;
      color: var(--muted);
      white-space: nowrap;
    }
    .status::before {
      content: "";
      width: 9px; height: 9px;
      border-radius: 999px;
      display: inline-block;
      background: var(--info);
      box-shadow: 0 0 0 4px rgba(96,165,250,0.16);
    }
    .ok::before { background: var(--ok); box-shadow: 0 0 0 4px rgba(105,178,60,0.18); }
    .warn::before { background: var(--warn); box-shadow: 0 0 0 4px rgba(245,158,11,0.16); }
    .bad::before { background: var(--bad); box-shadow: 0 0 0 4px rgba(239,68,68,0.14); }

    /* ====== Footer ====== */
    .footer {
      max-width: var(--maxw);
      margin: 24px auto 44px;
      padding: 0 18px;
      display: flex;
      align-items: center;
      justify-content: space-between;
      gap: 12px;
      flex-wrap: wrap;
      color: var(--muted);
      font-size: 12px;
    }
    .footmark {
      display: inline-flex;
      gap: 10px;
      align-items: center;
    }
    .footmark img { height: 20px; width: auto; opacity: 0.95; }

    /* smooth anchor */
    html { scroll-behavior: smooth; }
  </style>
</head>

<body>
  <header class="appbar">
    <div class="appbar-inner">
      <div class="logo">
        <img src="data:image/png;base64,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QICgA0CAoANAgKADQICgA0CAoANAgKADQICgA0CAoANAgKADQICgA0CAoANAgKADQICgA0CAoANAgKADQICgA0CAoANAgKADQICgA0CAoANAgKADQICgA0CAoANAgKADQICgA0CAoANAgKADQICgA0CAoANAgKADQICgA0CAoANAgKADQICgA0CAoANAgKADQICgA0CAoANAgKADQICgA0CAoANAgKADQICgA0CAoANAgKADQICgA0CAoANAgKADQICgA0CAoANAgKADQICgA0CAoANAgKADQICgA0CAoANAgKADQICgA0CAoANAgKADQICgA0CAoANAgKADQICgA0CAoANAgKADQICgA0CAoANAgKADQICgA0CAoANAgKADQICgA0CAoANAgKADQICgA0CAoANAgKADQICgA0CAoANAgKADQICgA0CAoANAgKADQICgA0CAoANAgKADQICgA0CAoANAgKADQICgA0CAoANAgKADQICgA0CAoANAgKADQICgA0CAoANAgKADQICgA0CAoANAgKADQICgA0CAoANAgKADQICgA0CAoANAgKADQICgA0CAoANAgKADQICgA0CAoANAgKADQICgA0CAoANAgKADQICgA0CAoANAgKADQICgA0CAoANAgKADQICgA0CAoANAgKADQICgA0CAoANAgKADQICgA0CAoANAgKADQICgA0CAoANAgKADQICgA0CAoANAgKADQICgA0CAoANAgKADQICgA0CAoANAgKADQICgA0CAoANAgKADQICgA0DAH8lzlwysNDYDAAAAAElFTkSuQmCC" alt="Sohersa BIM logo" />
      </div>

      <div class="meta">
        <div class="title">DISEÑO INGENIERÍAS COLÓN GDL · Dashboard BIM (26 semanas)</div>
        <div class="sub">Cliente: CAABSA · 24,258.12 m² · LOD 300 · ISO 19650 · CDE: Autodesk Construction Cloud (o equivalente)</div>
      </div>

      <div class="actions">
        <span class="chip"><span class="dot"></span>Estado: Planeación</span>
        <span class="chip">Código: CBA_PEJ_26026_DEC</span>
        <button class="btn" id="themeBtn" type="button">Cambiar tema</button>
      </div>
    </div>
  </header>

  <div class="container">
    <div class="layout">
      <!-- Sidebar -->
      <aside class="sidebar">
        <div class="side-head">
          <div class="h">Control del proyecto</div>
          <div class="p">Estructura BIM, cronograma, gobierno ISO 19650, QA/QC, coordinación y entregables.</div>
        </div>
        <nav class="nav">
          <a href="#overview"><span>Resumen</span><span class="k">KPI</span></a>
          <a href="#gantt"><span>Gantt 26 semanas</span><span class="k">Plan</span></a>
          <a href="#org"><span>Organigrama</span><span class="k">Roles</span></a>
          <a href="#governance"><span>Gobierno BIM</span><span class="k">ISO</span></a>
          <a href="#qaqc"><span>QA/QC + Clash</span><span class="k">IFC</span></a>
          <a href="#deliverables"><span>Entregables</span><span class="k">LOD300</span></a>
        </nav>
      </aside>

      <!-- Content -->
      <main class="content">
        <!-- Overview -->
        <section class="card" id="overview">
          <div class="card-head">
            <div class="t">
              <svg width="18" height="18" viewBox="0 0 24 24" fill="none" aria-hidden="true">
                <path d="M12 21s-7-4.5-7-11a7 7 0 0 1 14 0c0 6.5-7 11-7 11Z" stroke="currentColor" stroke-width="2"/>
                <path d="M9.5 10.5 11 12l3.5-4" stroke="currentColor" stroke-width="2"/>
              </svg>
              Resumen ejecutivo
            </div>
            <span class="badge">Dashboard · Modern enterprise UI</span>
          </div>
          <div class="card-body">
            <div class="kpis">
              <div class="kpi">
                <div class="l">Disciplinas</div>
                <div class="v">7</div>
                <div class="h">HVAC · Hidráulico · Sanitario · Pluvial · Eléctrico · PCI · Voz & Datos</div>
              </div>
              <div class="kpi">
                <div class="l">Equipo estimado</div>
                <div class="v">20–22</div>
                <div class="h">1 BIM Manager, 7 líderes, 12–14 modeladores</div>
              </div>
              <div class="kpi">
                <div class="l">Modelo objetivo</div>
                <div class="v">LOD 300</div>
                <div class="h">Revit por especialidad, coordinado</div>
              </div>
              <div class="kpi">
                <div class="l">Emisión final</div>
                <div class="v">IFC</div>
                <div class="h">Solo tras QA/QC + coordinación</div>
              </div>
            </div>

            <div style="margin-top: 12px; color: var(--muted); font-size: 12px; line-height: 1.6;">
              Sohersa BIM desarrolla el proyecto con un enfoque <strong>nativamente BIM</strong>: el modelo es el eje del diseño, coordinación y documentación.
              La gestión documental se realiza en un <strong>CDE</strong> (preferentemente Autodesk Construction Cloud) y los flujos se alinean a <strong>ISO 19650</strong>
              (WIP → Shared → Published). Se ejecuta <strong>clash detection</strong> y coordinación BIM dentro del alcance, con consolidación en <strong>modelo federado</strong>, además de un proceso de <strong>QA/QC</strong> previo a cualquier emisión para construcción.
            </div>
          </div>
        </section>

        <!-- Gantt -->
        <section class="card" id="gantt">
          <div class="card-head">
            <div class="t">
              <svg width="18" height="18" viewBox="0 0 24 24" fill="none" aria-hidden="true">
                <path d="M7 3v4M17 3v4M4 9h16M6 13h4M6 17h10" stroke="currentColor" stroke-width="2" stroke-linecap="round"/>
                <path d="M5 6h14a2 2 0 0 1 2 2v13a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2V8a2 2 0 0 1 2-2Z" stroke="currentColor" stroke-width="2"/>
              </svg>
              Gantt del proyecto (26 semanas)
            </div>
            <span class="badge">Plan macro · Editable</span>
          </div>
          <div class="card-body">
            <div class="gantt-wrap">
              <div class="gantt">
                <div class="g-header">
                  <div class="left">Fases</div>
                  <div class="weeks" aria-label="Semanas 1 a 26"><div class="wk">1</div>
<div class="wk">2</div>
<div class="wk">3</div>
<div class="wk">4</div>
<div class="wk">5</div>
<div class="wk">6</div>
<div class="wk">7</div>
<div class="wk">8</div>
<div class="wk">9</div>
<div class="wk">10</div>
<div class="wk">11</div>
<div class="wk">12</div>
<div class="wk">13</div>
<div class="wk">14</div>
<div class="wk">15</div>
<div class="wk">16</div>
<div class="wk">17</div>
<div class="wk">18</div>
<div class="wk">19</div>
<div class="wk">20</div>
<div class="wk">21</div>
<div class="wk">22</div>
<div class="wk">23</div>
<div class="wk">24</div>
<div class="wk">25</div>
<div class="wk">26</div></div>
                  <div class="left">Entregables principales</div>
                </div>

                
      <div class="g-row">
        <div class="g-label">
          <div class="g-name">Fase 1 · Arranque y planeación</div>
          <div class="g-meta">Semanas 1–2</div>
        </div>
        <div class="g-track" role="img" aria-label="Fase 1 · Arranque y planeación, semanas 1 a 2">
          <div class="g-bar green" style="grid-column: 1 / 3;">
            <span class="g-bar-text">Sem 1–2</span>
          </div>
        </div>
        <div class="g-deliverables"><span class="tag">Contrato + anticipo</span><span class="tag">Configuración CDE</span><span class="tag">BEP ISO 19650</span><span class="tag">Plan de trabajo</span></div>
      </div>
    

      <div class="g-row">
        <div class="g-label">
          <div class="g-name">Fase 2 · Ingeniería básica</div>
          <div class="g-meta">Semanas 3–6</div>
        </div>
        <div class="g-track" role="img" aria-label="Fase 2 · Ingeniería básica, semanas 3 a 6">
          <div class="g-bar blue" style="grid-column: 3 / 7;">
            <span class="g-bar-text">Sem 3–6</span>
          </div>
        </div>
        <div class="g-deliverables"><span class="tag">Bases de diseño</span><span class="tag">Criterios por disciplina</span><span class="tag">Esquemas</span><span class="tag">1ª coordinación</span></div>
      </div>
    

      <div class="g-row">
        <div class="g-label">
          <div class="g-name">Fase 3 · Ing. de detalle + Modelado LOD 300</div>
          <div class="g-meta">Semanas 7–16</div>
        </div>
        <div class="g-track" role="img" aria-label="Fase 3 · Ing. de detalle + Modelado LOD 300, semanas 7 a 16">
          <div class="g-bar green" style="grid-column: 7 / 17;">
            <span class="g-bar-text">Sem 7–16</span>
          </div>
        </div>
        <div class="g-deliverables"><span class="tag">Diseño técnico</span><span class="tag">Modelos LOD 300</span><span class="tag">Memorias de cálculo</span><span class="tag">Clash detection</span></div>
      </div>
    

      <div class="g-row">
        <div class="g-label">
          <div class="g-name">Fase 4 · Documentación para construcción</div>
          <div class="g-meta">Semanas 17–22</div>
        </div>
        <div class="g-track" role="img" aria-label="Fase 4 · Documentación para construcción, semanas 17 a 22">
          <div class="g-bar blue" style="grid-column: 17 / 23;">
            <span class="g-bar-text">Sem 17–22</span>
          </div>
        </div>
        <div class="g-deliverables"><span class="tag">Planos ejecutivos</span><span class="tag">Ajustes finales</span><span class="tag">QA/QC</span><span class="tag">Pre-IFC</span></div>
      </div>
    

      <div class="g-row">
        <div class="g-label">
          <div class="g-name">Fase 5 · Entrega final y cierre</div>
          <div class="g-meta">Semanas 23–26</div>
        </div>
        <div class="g-track" role="img" aria-label="Fase 5 · Entrega final y cierre, semanas 23 a 26">
          <div class="g-bar green" style="grid-column: 23 / 27;">
            <span class="g-bar-text">Sem 23–26</span>
          </div>
        </div>
        <div class="g-deliverables"><span class="tag">Modelos finales</span><span class="tag">Planos IFC</span><span class="tag">Memorias finales</span><span class="tag">Cierre técnico</span></div>
      </div>
    
              </div>
            </div>

            <div style="margin-top: 10px; color: var(--muted); font-size: 12px; line-height: 1.55;">
              Nota: el gantt es una base de planeación. Las fechas definitivas dependen de la entrega oportuna de información base (arquitectura/estructura) y de ventanas de revisión/validación del cliente.
            </div>
          </div>
        </section>

        <!-- Org + Governance -->
        <section class="grid2">
          
          <section class="card" id="org">
            <div class="card-head">
              <div class="t">
                <svg width="18" height="18" viewBox="0 0 24 24" fill="none" aria-hidden="true">
                  <path d="M16 11c1.66 0 3-1.34 3-3S17.66 5 16 5s-3 1.34-3 3 1.34 3 3 3Z" stroke="currentColor" stroke-width="2"/>
                  <path d="M8 11c1.66 0 3-1.34 3-3S9.66 5 8 5 5 6.34 5 8s1.34 3 3 3Z" stroke="currentColor" stroke-width="2"/>
                  <path d="M12 20c2.2 0 4-1.8 4-4s-1.8-4-4-4-4 1.8-4 4 1.8 4 4 4Z" stroke="currentColor" stroke-width="2"/>
                </svg>
                Organigrama de ejecución
              </div>
              <span class="badge">Roles + capacidad instalada</span>
            </div>

            <div class="card-body">
              <div class="orgchart" aria-label="Organigrama Sohersa BIM">
                <div class="org-level">
                  <div class="node primary">
                    <div class="node-title">BIM Manager / Coordinador General del Proyecto</div>
                    <div class="node-sub">Gobierno BIM · ISO 19650 · CDE (ACC o equivalente) · Emisiones y control de versiones</div>
                    <div class="node-meta">Responsable final de coordinación, cronograma, reportes y publicación de información</div>
                  </div>
                </div>

                <div class="org-connector"></div>

                <div class="org-level cols-3">
                  <div class="node">
                    <div class="node-title">Líder de Ingeniería Eléctrica</div>
                    <div class="node-sub">Diseño técnico + memorias + validación del modelo</div>
                    <div class="node-meta"><strong>Modeladores BIM:</strong> 3–4</div>
                  </div>

                  <div class="node">
                    <div class="node-title">Líder de Ingeniería HVAC</div>
                    <div class="node-sub">Diseño técnico + memorias + validación del modelo</div>
                    <div class="node-meta"><strong>Modeladores BIM:</strong> 2</div>
                  </div>

                  <div class="node">
                    <div class="node-title">Líder de Especiales</div>
                    <div class="node-sub">PCI + Voz & Datos (diseño técnico + memorias + validación del modelo)</div>
                    <div class="node-meta"><strong>Modeladores BIM:</strong> 2 (1 PCI, 1 Voz & Datos)</div>
                  </div>
                </div>

                <div class="org-connector"></div>

                <div class="org-level cols-2">
                  <div class="node emphasis">
                    <div class="node-title">Líder Hidrosanitario (Hidráulico + Sanitario + Pluvial)</div>
                    <div class="node-sub">Un solo liderazgo técnico para coherencia de criterios, trayectorias y compatibilidad hidráulica</div>
                    <div class="node-meta"><strong>Equipo de modelado BIM:</strong> 4 modeladores (total para las 3 disciplinas)</div>
                  </div>

                  <div class="node">
                    <div class="node-title">Equipo de Soporte BIM</div>
                    <div class="node-sub">Plantillas, estándares, auditorías y soporte de coordinación</div>
                    <div class="node-meta">Control de calidad previo a emisión (QA/QC)</div>
                  </div>
                </div>
              </div>

              <div class="note">
                Nota: La asignación de recursos puede variar ligeramente en función de la complejidad, ventanas de revisión del cliente, disponibilidad de información base y ritmo de coordinación del proyecto.
              </div>
            </div>
          </section>


          <section class="card" id="governance">
            <div class="card-head">
              <div class="t">
                <svg width="18" height="18" viewBox="0 0 24 24" fill="none" aria-hidden="true">
                  <path d="M12 2 2 7l10 5 10-5-10-5Z" stroke="currentColor" stroke-width="2"/>
                  <path d="M2 17l10 5 10-5" stroke="currentColor" stroke-width="2"/>
                  <path d="M2 12l10 5 10-5" stroke="currentColor" stroke-width="2"/>
                </svg>
                Gobierno BIM (ISO 19650)
              </div>
              <span class="badge">CDE + trazabilidad</span>
            </div>
            <div class="card-body">
              <div class="list">
                <div class="item">
                  <div>
                    <div class="tt">CDE (ACC o equivalente)</div>
                    <div class="ss">Estructura documental y control de versiones. Una sola fuente de verdad para el proyecto.</div>
                  </div>
                  <span class="status ok">CDE</span>
                </div>

                <div class="item">
                  <div>
                    <div class="tt">Flujo ISO: WIP → Shared → Published</div>
                    <div class="ss">Revisión técnica interna, coordinación interdisciplinaria y emisión controlada.</div>
                  </div>
                  <span class="status">ISO</span>
                </div>

                <div class="item">
                  <div>
                    <div class="tt">Comité técnico</div>
                    <div class="ss">BIM Manager + líderes para resolver interferencias críticas y decisiones transversales.</div>
                  </div>
                  <span class="status warn">Control</span>
                </div>
              
                <div class="item">
                  <div>
                    <div class="tt">Modelo federado</div>
                    <div class="ss">Consolidación de modelos por disciplina para coordinación: detección de interferencias, revisión de trayectorias y compatibilidad entre sistemas dentro del alcance contratado.</div>
                  </div>
                  <span class="status warn">Federado</span>
                </div>

                <div class="item">
                  <div>
                    <div class="tt">Proceso de coordinación BIM (alcance Sohersa)</div>
                    <div class="ss">Corridas de coordinación y cierre de observaciones para HVAC, Eléctrico, Hidrosanitario (Hidráulico + Sanitario + Pluvial), PCI y Voz & Datos. Reportes y evidencia en el CDE.</div>
                  </div>
                  <span class="status">BIM</span>
                </div>

                <div class="item">
                  <div>
                    <div class="tt">Licencias genuinas</div>
                    <div class="ss">Operación con software y licenciamiento legítimo. Flujo nativo Revit/ACC y cumplimiento de buenas prácticas para entornos Autodesk.</div>
                  </div>
                  <span class="status ok">Compliance</span>
                </div>

                <div class="item">
                  <div>
                    <div class="tt">Aliado directo de Autodesk</div>
                    <div class="ss">Relación directa como aliado de Autodesk para fortalecer adopción, mejores prácticas y soporte en entornos de colaboración en la nube.</div>
                  </div>
                  <span class="status ok">Autodesk</span>
                </div>
</div>
            </div>
          </section>
        </section>

        <!-- QAQC -->
        <section class="card" id="qaqc">
          <div class="card-head">
            <div class="t">
              <svg width="18" height="18" viewBox="0 0 24 24" fill="none" aria-hidden="true">
                <path d="M9 11 12 14 22 4" stroke="currentColor" stroke-width="2" stroke-linecap="round"/>
                <path d="M21 12v7a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2V5a2 2 0 0 1 2-2h11" stroke="currentColor" stroke-width="2" stroke-linecap="round"/>
              </svg>
              QA/QC + Coordinación (Clash)
            </div>
            <span class="badge">Previo a IFC</span>
          </div>
          <div class="card-body">
            <div class="grid2">
              <div class="list">
                <div class="item">
                  <div>
                    <div class="tt">Revisión técnica por disciplina</div>
                    <div class="ss">Validación de criterios, dimensionamiento y coherencia del modelo con memorias.</div>
                  </div>
                  <span class="status">QA</span>
                </div>
                <div class="item">
                  <div>
                    <div class="tt">Clash detection interdisciplinario</div>
                    <div class="ss">Corridas de interferencias y cierre con evidencia gráfica y trazabilidad.</div>
                  </div>
                  <span class="status warn">Coord.</span>
                </div>
              </div>
              <div class="list">
                <div class="item">
                  <div>
                    <div class="tt">Consistencia modelo · planos · memorias</div>
                    <div class="ss">Planos generados desde el modelo. Validación para evitar discrepancias.</div>
                  </div>
                  <span class="status">QC</span>
                </div>
                <div class="item">
                  <div>
                    <div class="tt">Emisión IFC</div>
                    <div class="ss">Solo se publica información aprobada tras QA/QC + coordinación del alcance contratado.</div>
                  </div>
                  <span class="status ok">IFC</span>
                </div>
              </div>
            </div>
          </div>
        </section>

        <!-- Deliverables -->
        <section class="card" id="deliverables">
          <div class="card-head">
            <div class="t">
              <svg width="18" height="18" viewBox="0 0 24 24" fill="none" aria-hidden="true">
                <path d="M14 2H6a2 2 0 0 0-2 2v16a2 2 0 0 0 2 2h12a2 2 0 0 0 2-2V8l-8-6Z" stroke="currentColor" stroke-width="2"/>
                <path d="M14 2v6h8" stroke="currentColor" stroke-width="2"/>
                <path d="M8 13h8M8 17h8" stroke="currentColor" stroke-width="2" stroke-linecap="round"/>
              </svg>
              Entregables del proyecto
            </div>
            <span class="badge">LOD 300</span>
          </div>
          <div class="card-body">
            <div class="grid2">
              <div class="list">
                <div class="item">
                  <div>
                    <div class="tt">Modelos BIM (Revit) por disciplina</div>
                    <div class="ss">HVAC · Hidráulico · Sanitario · Pluvial · Eléctrico · PCI · Voz & Datos (LOD 300).</div>
                  </div>
                  <span class="status ok">LOD 300</span>
                </div>
                <div class="item">
                  <div>
                    <div class="tt">Planos ejecutivos por especialidad</div>
                    <div class="ss">Paquetes listos para construcción, alineados con el modelo y validados por QA/QC.</div>
                  </div>
                  <span class="status warn">IFC</span>
                </div>
              </div>
              <div class="list">
                <div class="item">
                  <div>
                    <div class="tt">Memorias de cálculo</div>
                    <div class="ss">Documentación técnica completa por disciplina para sustentar el diseño.</div>
                  </div>
                  <span class="status">Incluido</span>
                </div>
                <div class="item">
                  <div>
                    <div class="tt">Reporte de coordinación</div>
                    <div class="ss">Registro de interferencias, acuerdos y estatus de cierre.</div>
                  </div>
                  <span class="status">Incluido</span>
                </div>
              </div>
            </div>

            <div style="margin-top: 10px; color: var(--muted); font-size: 12px; line-height: 1.55;">
              Exclusiones: arquitectura, estructura, trámites/firmas ante autoridades, presupuestos/APU, supervisión de obra o levantamientos en sitio (salvo cotización adicional).
            </div>
          </div>
        </section>
      </main>
    </div>
  </div>

  <footer class="footer">
    <div class="footmark">
      <img src="data:image/png;base64,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QICgA0CAoANAgKADQICgA0CAoANAgKADQICgA0CAoANAgKADQICgA0CAoANAgKADQICgA0CAoANAgKADQICgA0CAoANAgKADQICgA0CAoANAgKADQICgA0CAoANAgKADQICgA0CAoANAgKADQICgA0CAoANAgKADQICgA0CAoANAgKADQICgA0CAoANAgKADQICgA0CAoANAgKADQICgA0CAoANAgKADQICgA0CAoANAgKADQICgA0CAoANAgKADQICgA0CAoANAgKADQICgA0CAoANAgKADQICgA0CAoANAgKADQICgA0CAoANAgKADQICgA0CAoANAgKADQICgA0CAoANAgKADQICgA0CAoANAgKADQICgA0CAoANAgKADQICgA0CAoANAgKADQICgA0CAoANAgKADQICgA0CAoANAgKADQICgA0CAoANAgKADQICgA0CAoANAgKADQICgA0CAoANAgKADQICgA0CAoANAgKADQICgA0CAoANAgKADQICgA0CAoANAgKADQICgA0CAoANAgKADQICgA0CAoANAgKADQICgA0CAoANAgKADQICgA0CAoANAgKADQICgA0CAoANAgKADQICgA0CAoANAgKADQICgA0CAoANAgKADQICgA0CAoANAgKADQICgA0CAoANAgKADQICgA0CAoANAgKADQICgA0CAoANAgKADQICgA0CAoANAgKADQICgA0CAoANAgKADQICgA0CAoANAgKADQICgA0CAoANAgKADQICgA0CAoANAgKADQICgA0DAH8lzlwysNDYDAAAAAElFTkSuQmCC" alt="Sohersa BIM logo" />
      <span>© Sohersa BIM · Dashboard de seguimiento · ISO 19650</span>
    </div>
    <div>Versión: 0.2 · Diseño moderno + Gantt</div>
  </footer>

  <script>
    (function() {
      const root = document.documentElement;
      const btn = document.getElementById('themeBtn');

      function setTheme(t) {
        root.setAttribute('data-theme', t);
        localStorage.setItem('sohersa_theme', t);
      }

      // Default: dark, unless stored preference
      const saved = localStorage.getItem('sohersa_theme');
      if (saved === 'light' || saved === 'dark') {
        setTheme(saved);
      } else {
        setTheme('dark');
      }

      btn.addEventListener('click', () => {
        const current = root.getAttribute('data-theme') || 'dark';
        setTheme(current === 'dark' ? 'light' : 'dark');
      });
    })();
  </script>
</body>
</html>
