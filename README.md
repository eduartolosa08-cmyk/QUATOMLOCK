<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>CyberShield — Sistema de Seguridad Web</title>
<link href="https://fonts.googleapis.com/css2?family=JetBrains+Mono:wght@400;500;700&family=Syne:wght@400;500;700;800&display=swap" rel="stylesheet">
<style>
  :root {
    --bg: #0a0e1a;
    --bg2: #0f1424;
    --bg3: #151c30;
    --border: rgba(0,255,170,0.12);
    --border2: rgba(0,255,170,0.25);
    --accent: #00ffaa;
    --accent2: #00bfff;
    --accent3: #ff4d6d;
    --accent4: #ffd166;
    --text: #e8f0fe;
    --text2: #8899bb;
    --text3: #4a5680;
    --success: #00ffaa;
    --warning: #ffd166;
    --danger: #ff4d6d;
    --info: #00bfff;
    --mono: 'JetBrains Mono', monospace;
    --sans: 'Syne', sans-serif;
  }
 
  * { box-sizing: border-box; margin: 0; padding: 0; }
 
  body {
    background: var(--bg);
    color: var(--text);
    font-family: var(--mono);
    min-height: 100vh;
    overflow-x: hidden;
  }
 
  /* GRID BG */
  body::before {
    content: '';
    position: fixed; top: 0; left: 0; width: 100%; height: 100%;
    background-image:
      linear-gradient(rgba(0,255,170,0.03) 1px, transparent 1px),
      linear-gradient(90deg, rgba(0,255,170,0.03) 1px, transparent 1px);
    background-size: 40px 40px;
    pointer-events: none; z-index: 0;
  }
 
  .container { max-width: 1200px; margin: 0 auto; padding: 0 24px; position: relative; z-index: 1; }
 
  /* HEADER */
  header {
    border-bottom: 1px solid var(--border);
    background: rgba(10,14,26,0.95);
    backdrop-filter: blur(10px);
    position: sticky; top: 0; z-index: 100;
    padding: 0;
  }
  .header-inner {
    display: flex; align-items: center; justify-content: space-between;
    padding: 16px 24px; max-width: 1200px; margin: 0 auto;
  }
  .logo {
    font-family: var(--sans); font-weight: 800; font-size: 22px;
    color: var(--accent); letter-spacing: -0.5px;
    display: flex; align-items: center; gap: 10px;
  }
  .logo-icon {
    width: 32px; height: 32px; border: 2px solid var(--accent);
    border-radius: 8px; display: flex; align-items: center; justify-content: center;
    font-size: 14px;
  }
  .status-bar {
    display: flex; gap: 20px; align-items: center;
  }
  .status-dot {
    display: flex; align-items: center; gap: 6px;
    font-size: 11px; color: var(--text2);
  }
  .dot {
    width: 7px; height: 7px; border-radius: 50%;
    animation: pulse 2s infinite;
  }
  .dot.green { background: var(--success); box-shadow: 0 0 6px var(--success); }
  .dot.yellow { background: var(--warning); box-shadow: 0 0 6px var(--warning); }
  .dot.red { background: var(--danger); box-shadow: 0 0 6px var(--danger); }
  @keyframes pulse { 0%,100% { opacity: 1; } 50% { opacity: 0.4; } }
 
  /* NAV TABS */
  nav {
    border-bottom: 1px solid var(--border);
    background: var(--bg2);
  }
  .nav-inner {
    display: flex; gap: 0;
    max-width: 1200px; margin: 0 auto; padding: 0 24px;
  }
  .nav-tab {
    padding: 14px 24px; cursor: pointer; font-family: var(--mono);
    font-size: 12px; font-weight: 500; color: var(--text3);
    border-bottom: 2px solid transparent;
    transition: all 0.2s; letter-spacing: 0.5px; text-transform: uppercase;
    background: none; border-top: none; border-left: none; border-right: none;
    white-space: nowrap;
  }
  .nav-tab:hover { color: var(--text2); }
  .nav-tab.active { color: var(--accent); border-bottom-color: var(--accent); }
 
  /* SECTIONS */
  .section { display: none; padding: 32px 24px; max-width: 1200px; margin: 0 auto; }
  .section.active { display: block; }
 
  /* CARDS */
  .card {
    background: var(--bg2);
    border: 1px solid var(--border);
    border-radius: 12px;
    padding: 24px;
    position: relative;
    overflow: hidden;
  }
  .card::before {
    content: '';
    position: absolute; top: 0; left: 0; right: 0; height: 1px;
    background: linear-gradient(90deg, transparent, var(--accent), transparent);
    opacity: 0.4;
  }
  .card-title {
    font-family: var(--sans); font-weight: 700; font-size: 14px;
    color: var(--text2); text-transform: uppercase; letter-spacing: 1.5px;
    margin-bottom: 20px;
  }
 
  /* METRIC CARDS */
  .metrics-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(180px, 1fr)); gap: 16px; margin-bottom: 24px; }
  .metric-card {
    background: var(--bg3);
    border: 1px solid var(--border);
    border-radius: 10px;
    padding: 20px;
  }
  .metric-label { font-size: 10px; color: var(--text3); text-transform: uppercase; letter-spacing: 1px; margin-bottom: 8px; }
  .metric-value { font-family: var(--sans); font-size: 32px; font-weight: 800; }
  .metric-value.green { color: var(--success); }
  .metric-value.red { color: var(--danger); }
  .metric-value.yellow { color: var(--warning); }
  .metric-value.blue { color: var(--info); }
  .metric-sub { font-size: 11px; color: var(--text3); margin-top: 6px; }
 
  /* GRID LAYOUTS */
  .grid-2 { display: grid; grid-template-columns: 1fr 1fr; gap: 20px; }
  .grid-3 { display: grid; grid-template-columns: 1fr 1fr 1fr; gap: 20px; }
  @media (max-width: 768px) {
    .grid-2, .grid-3 { grid-template-columns: 1fr; }
    .metrics-grid { grid-template-columns: 1fr 1fr; }
  }
 
  /* BUTTONS */
  .btn {
    display: inline-flex; align-items: center; gap: 8px;
    padding: 10px 20px; border-radius: 8px; cursor: pointer;
    font-family: var(--mono); font-size: 12px; font-weight: 500;
    text-transform: uppercase; letter-spacing: 0.5px;
    transition: all 0.2s; border: none;
  }
  .btn-primary {
    background: var(--accent); color: var(--bg);
  }
  .btn-primary:hover { background: #00cc88; transform: translateY(-1px); }
  .btn-outline {
    background: transparent; color: var(--accent);
    border: 1px solid var(--border2);
  }
  .btn-outline:hover { background: rgba(0,255,170,0.08); }
  .btn-danger { background: var(--danger); color: white; }
  .btn-danger:hover { background: #cc3355; }
  .btn:disabled { opacity: 0.4; cursor: not-allowed; transform: none !important; }
 
  /* INPUTS */
  .input-group { margin-bottom: 16px; }
  .input-label {
    display: block; font-size: 11px; color: var(--text2);
    text-transform: uppercase; letter-spacing: 1px; margin-bottom: 6px;
  }
  .input-field {
    width: 100%; padding: 10px 14px;
    background: var(--bg3); border: 1px solid var(--border);
    border-radius: 8px; color: var(--text); font-family: var(--mono); font-size: 13px;
    outline: none; transition: border-color 0.2s;
  }
  .input-field:focus { border-color: var(--accent); }
  .input-field::placeholder { color: var(--text3); }
 
  /* LOG / ACTIVITY */
  .log-list { list-style: none; }
  .log-item {
    display: flex; align-items: flex-start; gap: 12px;
    padding: 10px 0; border-bottom: 1px solid var(--border);
    font-size: 12px;
  }
  .log-item:last-child { border-bottom: none; }
  .log-time { color: var(--text3); white-space: nowrap; min-width: 60px; }
  .log-tag {
    padding: 2px 8px; border-radius: 4px; font-size: 10px;
    font-weight: 700; text-transform: uppercase; white-space: nowrap;
  }
  .tag-ok { background: rgba(0,255,170,0.12); color: var(--success); }
  .tag-warn { background: rgba(255,209,102,0.12); color: var(--warning); }
  .tag-err { background: rgba(255,77,109,0.12); color: var(--danger); }
  .tag-info { background: rgba(0,191,255,0.12); color: var(--info); }
  .log-msg { color: var(--text2); flex: 1; }
 
  /* PROGRESS BAR */
  .progress-bar {
    height: 4px; background: var(--bg3);
    border-radius: 2px; overflow: hidden; margin: 8px 0;
  }
  .progress-fill { height: 100%; border-radius: 2px; transition: width 1s ease; }
  .fill-green { background: var(--success); }
  .fill-yellow { background: var(--warning); }
  .fill-red { background: var(--danger); }
  .fill-blue { background: var(--info); }
 
  /* SCAN RESULT */
  .vuln-item {
    display: flex; align-items: center; gap: 12px;
    padding: 12px; border-radius: 8px;
    background: var(--bg3); border: 1px solid var(--border);
    margin-bottom: 8px;
  }
  .vuln-icon { font-size: 16px; min-width: 20px; text-align: center; }
  .vuln-name { font-size: 13px; color: var(--text); flex: 1; }
  .vuln-severity {
    padding: 3px 10px; border-radius: 4px; font-size: 10px; font-weight: 700;
  }
  .sev-critical { background: rgba(255,77,109,0.2); color: var(--danger); border: 1px solid rgba(255,77,109,0.3); }
  .sev-high { background: rgba(255,150,50,0.2); color: #ff9632; border: 1px solid rgba(255,150,50,0.3); }
  .sev-medium { background: rgba(255,209,102,0.2); color: var(--warning); border: 1px solid rgba(255,209,102,0.3); }
  .sev-low { background: rgba(0,255,170,0.1); color: var(--success); border: 1px solid rgba(0,255,170,0.2); }
 
  /* AUTH FORM */
  .auth-strength { height: 3px; background: var(--bg3); border-radius: 2px; margin-top: 6px; }
  .auth-strength-fill { height: 100%; border-radius: 2px; transition: all 0.3s; }
  .strength-label { font-size: 10px; margin-top: 4px; }
 
  /* SCAN ANIMATION */
  .scan-line {
    height: 2px; background: linear-gradient(90deg, transparent, var(--accent), transparent);
    position: relative; overflow: hidden;
  }
  .scan-line::after {
    content: '';
    position: absolute; top: 0; left: -100%;
    width: 100%; height: 100%;
    background: inherit;
    animation: scanAnim 1.5s linear infinite;
  }
  @keyframes scanAnim { to { left: 200%; } }
 
  /* CHART BARS */
  .chart-bars { display: flex; align-items: flex-end; gap: 6px; height: 80px; }
  .chart-bar {
    flex: 1; border-radius: 3px 3px 0 0;
    transition: height 1s ease;
    background: var(--accent); opacity: 0.7;
    min-height: 4px;
  }
  .chart-bar:hover { opacity: 1; }
  .chart-labels { display: flex; gap: 6px; }
  .chart-label { flex: 1; text-align: center; font-size: 9px; color: var(--text3); }
 
  /* FIREWALL TABLE */
  .fw-table { width: 100%; border-collapse: collapse; font-size: 12px; }
  .fw-table th { color: var(--text3); text-transform: uppercase; font-size: 10px;
    letter-spacing: 1px; padding: 8px 12px; text-align: left;
    border-bottom: 1px solid var(--border); }
  .fw-table td { padding: 10px 12px; border-bottom: 1px solid rgba(255,255,255,0.03);
    color: var(--text2); }
  .fw-table tr:hover td { background: rgba(0,255,170,0.03); }
 
  /* TOGGLE */
  .toggle-wrap { display: flex; align-items: center; gap: 10px; cursor: pointer; }
  .toggle {
    width: 40px; height: 20px; background: var(--bg3);
    border: 1px solid var(--border2); border-radius: 10px;
    position: relative; transition: background 0.2s; cursor: pointer;
  }
  .toggle.on { background: rgba(0,255,170,0.3); border-color: var(--accent); }
  .toggle::after {
    content: ''; position: absolute; top: 2px; left: 2px;
    width: 14px; height: 14px; background: var(--text3); border-radius: 50%;
    transition: all 0.2s;
  }
  .toggle.on::after { left: 22px; background: var(--accent); }
 
  /* TERMINAL OUTPUT */
  .terminal {
    background: var(--bg); border: 1px solid var(--border);
    border-radius: 8px; padding: 16px; font-size: 11px;
    max-height: 220px; overflow-y: auto; color: var(--accent);
    line-height: 1.7;
  }
  .terminal .t-dim { color: var(--text3); }
  .terminal .t-warn { color: var(--warning); }
  .terminal .t-err { color: var(--danger); }
  .terminal .t-info { color: var(--info); }
 
  /* SCROLL BAR */
  ::-webkit-scrollbar { width: 4px; }
  ::-webkit-scrollbar-track { background: var(--bg2); }
  ::-webkit-scrollbar-thumb { background: var(--border2); border-radius: 2px; }
 
  /* MODAL */
  .modal-overlay {
    display: none; position: fixed; inset: 0; z-index: 200;
    background: rgba(0,0,0,0.7); align-items: center; justify-content: center;
    backdrop-filter: blur(4px);
  }
  .modal-overlay.open { display: flex; }
  .modal {
    background: var(--bg2); border: 1px solid var(--border2);
    border-radius: 16px; padding: 32px; max-width: 440px; width: 90%;
    position: relative;
  }
  .modal-close {
    position: absolute; top: 16px; right: 16px;
    background: none; border: none; color: var(--text2);
    cursor: pointer; font-size: 18px;
  }
 
  /* SECTION HEADER */
  .section-header {
    display: flex; align-items: center; justify-content: space-between;
    margin-bottom: 28px;
  }
  .section-title { font-family: var(--sans); font-size: 24px; font-weight: 800; }
  .section-sub { font-size: 12px; color: var(--text3); margin-top: 4px; }
 
  /* IP BADGE */
  .ip-badge {
    background: var(--bg3); border: 1px solid var(--border); border-radius: 6px;
    padding: 4px 10px; font-size: 11px; color: var(--text2);
  }
 
  /* NOTIFICATION TOAST */
  #toast {
    position: fixed; bottom: 24px; right: 24px; z-index: 300;
    background: var(--bg2); border: 1px solid var(--border2);
    border-radius: 10px; padding: 14px 20px;
    font-size: 12px; color: var(--text);
    transform: translateY(80px); opacity: 0;
    transition: all 0.3s;
  }
  #toast.show { transform: translateY(0); opacity: 1; }
  #toast.ok { border-color: var(--success); color: var(--success); }
  #toast.err { border-color: var(--danger); color: var(--danger); }
 
  /* BLINK */
  @keyframes blink { 0%,100%{opacity:1} 50%{opacity:0} }
  .blink { animation: blink 1s step-end infinite; }
</style>
</head>
<body>
 
<header>
  <div class="header-inner">
    <div class="logo">
      <div class="logo-icon">▲</div>
      CyberShield
    </div>
    <div class="status-bar">
      <div class="status-dot"><span class="dot green"></span> Sistema activo</div>
      <div class="status-dot"><span class="dot yellow"></span> 3 alertas</div>
      <div class="ip-badge" id="clock-display">--:--:--</div>
    </div>
  </div>
</header>
 
<nav>
  <div class="nav-inner">
    <button class="nav-tab active" onclick="switchTab('dashboard')">// Dashboard</button>
    <button class="nav-tab" onclick="switchTab('auth')">// Autenticación</button>
    <button class="nav-tab" onclick="switchTab('scanner')">// Escáner</button>
    <button class="nav-tab" onclick="switchTab('firewall')">// Firewall</button>
  </div>
</nav>
 
<!-- ============ DASHBOARD ============ -->
<section class="section active" id="tab-dashboard">
  <div class="section-header">
    <div>
      <div class="section-title">Panel de Control</div>
      <div class="section-sub">Monitoreo en tiempo real del sistema</div>
    </div>
    <button class="btn btn-outline" onclick="refreshDashboard()">↻ Actualizar</button>
  </div>
 
  <div class="metrics-grid">
    <div class="metric-card">
      <div class="metric-label">Amenazas bloqueadas</div>
      <div class="metric-value red" id="m-threats">247</div>
      <div class="metric-sub">Últimas 24h</div>
    </div>
    <div class="metric-card">
      <div class="metric-label">Intentos de login</div>
      <div class="metric-value yellow" id="m-logins">1,832</div>
      <div class="metric-sub">Hoy</div>
    </div>
    <div class="metric-card">
      <div class="metric-label">IPs bloqueadas</div>
      <div class="metric-value blue" id="m-ips">64</div>
      <div class="metric-sub">Activas</div>
    </div>
    <div class="metric-card">
      <div class="metric-label">Puntuación de seguridad</div>
      <div class="metric-value green" id="m-score">87</div>
      <div class="metric-sub">/ 100 pts</div>
    </div>
  </div>
 
  <div class="grid-2" style="margin-bottom:20px;">
    <div class="card">
      <div class="card-title">Actividad de amenazas (7 días)</div>
      <div class="chart-bars" id="chart-bars">
        <div class="chart-bar" style="height:45%"></div>
        <div class="chart-bar" style="height:60%"></div>
        <div class="chart-bar" style="height:30%"></div>
        <div class="chart-bar" style="height:80%"></div>
        <div class="chart-bar" style="height:55%"></div>
        <div class="chart-bar" style="height:70%"></div>
        <div class="chart-bar" style="height:40%; background: var(--warning)"></div>
      </div>
      <div class="chart-labels">
        <div class="chart-label">Lun</div><div class="chart-label">Mar</div>
        <div class="chart-label">Mié</div><div class="chart-label">Jue</div>
        <div class="chart-label">Vie</div><div class="chart-label">Sáb</div>
        <div class="chart-label">Hoy</div>
      </div>
    </div>
 
    <div class="card">
      <div class="card-title">Salud del sistema</div>
      <div style="margin-bottom:14px;">
        <div style="display:flex;justify-content:space-between;font-size:12px;color:var(--text2);margin-bottom:4px;">
          <span>Firewall</span><span style="color:var(--success)">Activo — 98%</span>
        </div>
        <div class="progress-bar"><div class="progress-fill fill-green" style="width:98%"></div></div>
      </div>
      <div style="margin-bottom:14px;">
        <div style="display:flex;justify-content:space-between;font-size:12px;color:var(--text2);margin-bottom:4px;">
          <span>Autenticación</span><span style="color:var(--success)">Activo — 100%</span>
        </div>
        <div class="progress-bar"><div class="progress-fill fill-green" style="width:100%"></div></div>
      </div>
      <div style="margin-bottom:14px;">
        <div style="display:flex;justify-content:space-between;font-size:12px;color:var(--text2);margin-bottom:4px;">
          <span>Escáner de vuln.</span><span style="color:var(--warning)">Activo — 72%</span>
        </div>
        <div class="progress-bar"><div class="progress-fill fill-yellow" style="width:72%"></div></div>
      </div>
      <div>
        <div style="display:flex;justify-content:space-between;font-size:12px;color:var(--text2);margin-bottom:4px;">
          <span>CPU del servidor</span><span style="color:var(--info)">Normal — 43%</span>
        </div>
        <div class="progress-bar"><div class="progress-fill fill-blue" style="width:43%"></div></div>
      </div>
    </div>
  </div>
 
  <div class="card">
    <div class="card-title">Registro de actividad reciente</div>
    <ul class="log-list" id="activity-log">
      <li class="log-item"><span class="log-time">14:32:01</span><span class="log-tag tag-err">BLOQUEADO</span><span class="log-msg">Intento de SQL Injection — IP: 185.220.101.45</span></li>
      <li class="log-item"><span class="log-time">14:28:44</span><span class="log-tag tag-warn">ALERTA</span><span class="log-msg">Múltiples fallos de login — usuario: admin (5 intentos)</span></li>
      <li class="log-item"><span class="log-time">14:25:12</span><span class="log-tag tag-ok">OK</span><span class="log-msg">Login exitoso — usuario: juan.perez@empresa.com</span></li>
      <li class="log-item"><span class="log-time">14:20:33</span><span class="log-tag tag-err">BLOQUEADO</span><span class="log-msg">XSS detectado en parámetro search — IP: 91.108.4.22</span></li>
      <li class="log-item"><span class="log-time">14:18:05</span><span class="log-tag tag-info">SCAN</span><span class="log-msg">Escaneo de vulnerabilidades completado — 3 encontradas</span></li>
      <li class="log-item"><span class="log-time">14:10:19</span><span class="log-tag tag-ok">OK</span><span class="log-msg">Certificado SSL renovado — válido por 90 días</span></li>
    </ul>
  </div>
</section>
 
<!-- ============ AUTENTICACIÓN ============ -->
<section class="section" id="tab-auth">
  <div class="section-header">
    <div>
      <div class="section-title">Autenticación Segura</div>
      <div class="section-sub">Control de acceso y verificación de identidad</div>
    </div>
  </div>
 
  <div class="grid-2">
    <div>
      <!-- Login Form -->
      <div class="card" style="margin-bottom:20px;">
        <div class="card-title">Panel de Login</div>
        <div class="input-group">
          <label class="input-label">Usuario / Email</label>
          <input class="input-field" id="auth-user" type="text" placeholder="usuario@empresa.com">
        </div>
        <div class="input-group">
          <label class="input-label">Contraseña</label>
          <input class="input-field" id="auth-pass" type="password" placeholder="••••••••••" oninput="checkPassStrength(this.value)">
          <div class="auth-strength"><div class="auth-strength-fill" id="strength-bar" style="width:0%;background:var(--danger)"></div></div>
          <div class="strength-label" id="strength-label" style="color:var(--text3)">Ingresa tu contraseña</div>
        </div>
        <div class="input-group" style="display:flex;align-items:center;gap:12px;">
          <input type="checkbox" id="mfa-check" style="accent-color:var(--accent);width:14px;height:14px;">
          <label for="mfa-check" style="font-size:12px;color:var(--text2);cursor:pointer;">Habilitar autenticación de dos factores (2FA)</label>
        </div>
        <div id="mfa-field" style="display:none;" class="input-group">
          <label class="input-label">Código 2FA (6 dígitos)</label>
          <input class="input-field" id="mfa-code" type="text" maxlength="6" placeholder="000000">
        </div>
        <button class="btn btn-primary" style="width:100%;justify-content:center;margin-top:8px;" onclick="doLogin()">
          Iniciar sesión segura →
        </button>
        <div id="login-result" style="margin-top:12px;font-size:12px;text-align:center;"></div>
      </div>
 
      <!-- Password Generator -->
      <div class="card">
        <div class="card-title">Generador de contraseñas</div>
        <div id="gen-pass" style="font-family:var(--mono);font-size:15px;color:var(--accent);background:var(--bg3);padding:12px 16px;border-radius:8px;margin-bottom:14px;letter-spacing:2px;word-break:break-all;">
          Haz clic para generar<span class="blink">_</span>
        </div>
        <div style="display:flex;gap:8px;flex-wrap:wrap;">
          <label style="font-size:11px;color:var(--text2);display:flex;align-items:center;gap:4px;cursor:pointer;">
            <input type="checkbox" id="opt-upper" checked style="accent-color:var(--accent)"> Mayúsculas
          </label>
          <label style="font-size:11px;color:var(--text2);display:flex;align-items:center;gap:4px;cursor:pointer;">
            <input type="checkbox" id="opt-num" checked style="accent-color:var(--accent)"> Números
          </label>
          <label style="font-size:11px;color:var(--text2);display:flex;align-items:center;gap:4px;cursor:pointer;">
            <input type="checkbox" id="opt-sym" checked style="accent-color:var(--accent)"> Símbolos
          </label>
        </div>
        <div style="display:flex;gap:8px;margin-top:14px;">
          <button class="btn btn-primary" style="flex:1;justify-content:center;" onclick="generatePass()">⟳ Generar</button>
          <button class="btn btn-outline" onclick="copyPass()">⊙ Copiar</button>
        </div>
      </div>
    </div>
 
    <div>
      <!-- Sessions -->
      <div class="card" style="margin-bottom:20px;">
        <div class="card-title">Sesiones activas</div>
        <div id="sessions-list">
          <div class="vuln-item" style="margin-bottom:8px;">
            <div style="font-size:20px;">💻</div>
            <div style="flex:1;">
              <div style="font-size:12px;color:var(--text);">Chrome — Windows 11</div>
              <div style="font-size:11px;color:var(--text3);">192.168.1.1 · Bogotá, CO · Activa ahora</div>
            </div>
            <span class="vuln-severity sev-low">ACTUAL</span>
          </div>
          <div class="vuln-item" style="margin-bottom:8px;">
            <div style="font-size:20px;">📱</div>
            <div style="flex:1;">
              <div style="font-size:12px;color:var(--text);">Safari — iPhone</div>
              <div style="font-size:11px;color:var(--text3);">172.16.0.4 · Medellín, CO · Hace 2h</div>
            </div>
            <button class="btn btn-danger" style="padding:4px 10px;font-size:10px;" onclick="revokeSession(this)">Revocar</button>
          </div>
          <div class="vuln-item">
            <div style="font-size:20px;">🖥</div>
            <div style="flex:1;">
              <div style="font-size:12px;color:var(--text);">Firefox — Ubuntu</div>
              <div style="font-size:11px;color:var(--text3);">10.0.0.8 · Cali, CO · Hace 5h</div>
            </div>
            <button class="btn btn-danger" style="padding:4px 10px;font-size:10px;" onclick="revokeSession(this)">Revocar</button>
          </div>
        </div>
      </div>
 
      <!-- Security Checklist -->
      <div class="card">
        <div class="card-title">Lista de seguridad</div>
        <div id="checklist" style="display:flex;flex-direction:column;gap:10px;"></div>
      </div>
    </div>
  </div>
</section>
 
<!-- ============ ESCÁNER ============ -->
<section class="section" id="tab-scanner">
  <div class="section-header">
    <div>
      <div class="section-title">Escáner de Vulnerabilidades</div>
      <div class="section-sub">Detección de fallas de seguridad en tiempo real</div>
    </div>
  </div>
 
  <div class="card" style="margin-bottom:20px;">
    <div class="card-title">Objetivo del escaneo</div>
    <div style="display:flex;gap:12px;flex-wrap:wrap;align-items:flex-end;">
      <div style="flex:1;min-width:200px;">
        <label class="input-label">URL o dominio</label>
        <input class="input-field" id="scan-target" type="text" placeholder="https://miempresa.com" value="https://ejemplo.com">
      </div>
      <div>
        <label class="input-label">Tipo de escaneo</label>
        <select class="input-field" id="scan-type" style="cursor:pointer;">
          <option value="basic">Básico (rápido)</option>
          <option value="full">Completo</option>
          <option value="web">Solo web (OWASP)</option>
        </select>
      </div>
      <button class="btn btn-primary" id="scan-btn" onclick="startScan()">▶ Iniciar escaneo</button>
    </div>
 
    <!-- Progress -->
    <div id="scan-progress" style="display:none;margin-top:20px;">
      <div style="display:flex;justify-content:space-between;font-size:12px;color:var(--text2);margin-bottom:6px;">
        <span id="scan-status">Iniciando...</span>
        <span id="scan-pct">0%</span>
      </div>
      <div class="progress-bar" style="height:6px;">
        <div class="progress-fill fill-green" id="scan-bar" style="width:0%;transition:width 0.3s;"></div>
      </div>
      <div class="scan-line" style="margin-top:8px;"></div>
    </div>
  </div>
 
  <!-- Terminal -->
  <div class="card" style="margin-bottom:20px;">
    <div class="card-title">Salida del escáner</div>
    <div class="terminal" id="scan-terminal">
      <span class="t-dim">[CyberShield Scanner v2.4.1]</span><br>
      <span class="t-dim">Listo. Ingresa una URL y presiona "Iniciar escaneo"</span><br>
      <span class="t-dim">&gt;</span> <span class="blink">_</span>
    </div>
  </div>
 
  <!-- Results -->
  <div class="card" id="scan-results" style="display:none;">
    <div style="display:flex;justify-content:space-between;align-items:center;margin-bottom:20px;">
      <div class="card-title" style="margin:0;">Vulnerabilidades detectadas</div>
      <div id="scan-summary" style="font-size:12px;color:var(--text2);"></div>
    </div>
    <div id="vuln-list"></div>
  </div>
</section>
 
<!-- ============ FIREWALL ============ -->
<section class="section" id="tab-firewall">
  <div class="section-header">
    <div>
      <div class="section-title">Firewall y Reglas</div>
      <div class="section-sub">Gestión de acceso y bloqueo de IPs</div>
    </div>
    <button class="btn btn-primary" onclick="openAddRule()">+ Nueva regla</button>
  </div>
 
  <div class="metrics-grid" style="margin-bottom:24px;">
    <div class="metric-card">
      <div class="metric-label">Reglas activas</div>
      <div class="metric-value green" id="fw-rules">12</div>
    </div>
    <div class="metric-card">
      <div class="metric-label">IPs en lista negra</div>
      <div class="metric-value red" id="fw-blacklist">64</div>
    </div>
    <div class="metric-card">
      <div class="metric-label">Peticiones filtradas hoy</div>
      <div class="metric-value yellow" id="fw-filtered">3,441</div>
    </div>
    <div class="metric-card">
      <div class="metric-label">Modo WAF</div>
      <div class="metric-value blue" style="font-size:18px;margin-top:4px;">ACTIVO</div>
    </div>
  </div>
 
  <div class="grid-2" style="margin-bottom:20px;">
    <div class="card">
      <div class="card-title">Protecciones WAF</div>
      <div id="waf-toggles" style="display:flex;flex-direction:column;gap:14px;"></div>
    </div>
    <div class="card">
      <div class="card-title">Bloquear IP manualmente</div>
      <div class="input-group">
        <label class="input-label">Dirección IP</label>
        <input class="input-field" id="block-ip" type="text" placeholder="192.168.1.100">
      </div>
      <div class="input-group">
        <label class="input-label">Razón</label>
        <input class="input-field" id="block-reason" type="text" placeholder="Actividad sospechosa">
      </div>
      <button class="btn btn-danger" style="width:100%;justify-content:center;" onclick="blockIP()">⛔ Bloquear IP</button>
    </div>
  </div>
 
  <div class="card">
    <div class="card-title">Reglas activas</div>
    <div style="overflow-x:auto;">
      <table class="fw-table" id="rules-table">
        <thead>
          <tr>
            <th>Nombre</th><th>Tipo</th><th>Origen</th><th>Acción</th><th>Estado</th><th>Hits</th><th></th>
          </tr>
        </thead>
        <tbody id="rules-body"></tbody>
      </table>
    </div>
  </div>
</section>
 
<!-- MODAL: Nueva regla -->
<div class="modal-overlay" id="rule-modal">
  <div class="modal">
    <button class="modal-close" onclick="closeModal()">✕</button>
    <div style="font-family:var(--sans);font-weight:700;font-size:18px;margin-bottom:20px;">Nueva regla de firewall</div>
    <div class="input-group">
      <label class="input-label">Nombre de la regla</label>
      <input class="input-field" id="rule-name" placeholder="Bloquear bots">
    </div>
    <div class="input-group">
      <label class="input-label">Tipo</label>
      <select class="input-field" id="rule-type">
        <option>IP</option><option>País</option><option>User-Agent</option><option>Ruta URL</option>
      </select>
    </div>
    <div class="input-group">
      <label class="input-label">Valor</label>
      <input class="input-field" id="rule-value" placeholder="10.0.0.0/8">
    </div>
    <div class="input-group">
      <label class="input-label">Acción</label>
      <select class="input-field" id="rule-action">
        <option>BLOQUEAR</option><option>PERMITIR</option><option>LIMITAR</option>
      </select>
    </div>
    <button class="btn btn-primary" style="width:100%;justify-content:center;margin-top:8px;" onclick="addRule()">
      Crear regla →
    </button>
  </div>
</div>
 
<!-- TOAST -->
<div id="toast"></div>
 
<script>
// ========= UTILITIES =========
function showToast(msg, type='ok') {
  const t = document.getElementById('toast');
  t.textContent = msg;
  t.className = 'show ' + type;
  setTimeout(() => t.className = '', 3000);
}
 
function switchTab(tab) {
  document.querySelectorAll('.section').forEach(s => s.classList.remove('active'));
  document.querySelectorAll('.nav-tab').forEach(t => t.classList.remove('active'));
  document.getElementById('tab-' + tab).classList.add('active');
  event.currentTarget.classList.add('active');
}
 
// Clock
setInterval(() => {
  document.getElementById('clock-display').textContent = new Date().toLocaleTimeString('es-CO');
}, 1000);
 
// ========= DASHBOARD =========
function refreshDashboard() {
  const t = document.getElementById('m-threats');
  const l = document.getElementById('m-logins');
  t.textContent = (200 + Math.floor(Math.random()*100)).toString();
  l.textContent = (1700 + Math.floor(Math.random()*300)).toLocaleString('es-CO');
 
  const log = document.getElementById('activity-log');
  const events = [
    ['BLOQUEADO','tag-err','Ataque DDoS mitigado — 2,300 peticiones/seg'],
    ['ALERTA','tag-warn','Usuario bloqueado por fuerza bruta — admin@test.com'],
    ['OK','tag-ok','Escaneo completado — sistema sin cambios críticos'],
    ['SCAN','tag-info','Nueva vulnerabilidad registrada en base de datos CVE'],
    ['BLOQUEADO','tag-err','Path Traversal detectado — /etc/passwd'],
  ];
  const e = events[Math.floor(Math.random()*events.length)];
  const now = new Date().toLocaleTimeString('es-CO', {hour:'2-digit',minute:'2-digit',second:'2-digit'});
  const li = document.createElement('li');
  li.className = 'log-item';
  li.style.opacity = '0';
  li.innerHTML = <span class="log-time">${now}</span><span class="log-tag ${e[1]}">${e[0]}</span><span class="log-msg">${e[2]}</span>;
  log.insertBefore(li, log.firstChild);
  setTimeout(() => li.style.transition = 'opacity 0.5s', 10);
  setTimeout(() => li.style.opacity = '1', 50);
  if (log.children.length > 8) log.removeChild(log.lastChild);
  showToast('Dashboard actualizado', 'ok');
}
 
// ========= AUTH =========
function checkPassStrength(val) {
  const bar = document.getElementById('strength-bar');
  const lbl = document.getElementById('strength-label');
  if (!val) { bar.style.width='0%'; lbl.textContent='Ingresa tu contraseña'; lbl.style.color='var(--text3)'; return; }
  let score = 0;
  if (val.length >= 8) score++;
  if (val.length >= 12) score++;
  if (/[A-Z]/.test(val)) score++;
  if (/[0-9]/.test(val)) score++;
  if (/[^A-Za-z0-9]/.test(val)) score++;
  const levels = [
    {w:'20%',c:'var(--danger)',t:'Muy débil'},
    {w:'40%',c:'var(--danger)',t:'Débil'},
    {w:'60%',c:'var(--warning)',t:'Regular'},
    {w:'80%',c:'var(--info)',t:'Fuerte'},
    {w:'100%',c:'var(--success)',t:'Muy fuerte'},
  ];
  const l = levels[Math.min(score,4)];
  bar.style.width = l.w; bar.style.background = l.c;
  lbl.textContent = l.t; lbl.style.color = l.c;
}
 
document.getElementById('mfa-check').addEventListener('change', function() {
  document.getElementById('mfa-field').style.display = this.checked ? 'block' : 'none';
});
 
function doLogin() {
  const user = document.getElementById('auth-user').value.trim();
  const pass = document.getElementById('auth-pass').value;
  const mfa = document.getElementById('mfa-check').checked;
  const mfaCode = document.getElementById('mfa-code').value;
  const res = document.getElementById('login-result');
 
  if (!user || !pass) {
    res.style.color = 'var(--danger)';
    res.textContent = '⚠ Completa usuario y contraseña';
    return;
  }
  if (mfa && mfaCode.length !== 6) {
    res.style.color = 'var(--warning)';
    res.textContent = '⚠ El código 2FA debe tener 6 dígitos';
    return;
  }
  if (pass.length < 6) {
    res.style.color = 'var(--danger)';
    res.textContent = '⚠ Contraseña bloqueada — demasiado débil';
    return;
  }
  res.style.color = 'var(--success)';
  res.textContent = '✓ Autenticación exitosa — sesión iniciada';
  showToast('Login exitoso: ' + user, 'ok');
}
 
function generatePass() {
  let chars = 'abcdefghijklmnopqrstuvwxyz';
  if (document.getElementById('opt-upper').checked) chars += 'ABCDEFGHIJKLMNOPQRSTUVWXYZ';
  if (document.getElementById('opt-num').checked) chars += '0123456789';
  if (document.getElementById('opt-sym').checked) chars += '!@#$%^&*()_+-=[]{}';
  let pass = '';
  for (let i = 0; i < 16; i++) pass += chars[Math.floor(Math.random()*chars.length)];
  document.getElementById('gen-pass').innerHTML = pass + '<span class="blink">_</span>';
}
 
function copyPass() {
  const txt = document.getElementById('gen-pass').textContent.replace('_','');
  if (txt === 'Haz clic para generar') { showToast('Primero genera una contraseña', 'err'); return; }
  navigator.clipboard.writeText(txt).then(() => showToast('Contraseña copiada', 'ok'));
}
 
function revokeSession(btn) {
  const item = btn.closest('.vuln-item');
  item.style.transition = 'opacity 0.3s';
  item.style.opacity = '0';
  setTimeout(() => item.remove(), 300);
  showToast('Sesión revocada', 'ok');
}
 
// Checklist
const checks = [
  {label:'Contraseña con 12+ caracteres', ok: false},
  {label:'Autenticación 2FA habilitada', ok: true},
  {label:'Sesiones con expiración activa', ok: true},
  {label:'Inicio de sesión con HTTPS', ok: true},
  {label:'Bloqueo tras 5 intentos fallidos', ok: false},
];
const cl = document.getElementById('checklist');
checks.forEach(c => {
  const d = document.createElement('div');
  d.style.cssText = 'display:flex;align-items:center;gap:10px;font-size:12px;';
  d.innerHTML = `<span style="color:${c.ok?'var(--success)':'var(--danger)'}">${c.ok?'✓':'✗'}</span>
    <span style="color:${c.ok?'var(--text)':'var(--text2)'}">${c.label}</span>
    ${!c.ok ? '<span class="vuln-severity sev-medium" style="margin-left:auto">Pendiente</span>' : ''}`;
  cl.appendChild(d);
});
 
// ========= SCANNER =========
const vulnDB = [
  {icon:'⚠',name:'SQL Injection en /api/login', sev:'critical', cls:'sev-critical', desc:'Parámetro "user" sin sanitizar'},
  {icon:'⚠',name:'Cross-Site Scripting (XSS) reflejado', sev:'high', cls:'sev-high', desc:'Campo de búsqueda vulnerable'},
  {icon:'!',name:'Cabeceras HTTP inseguras', sev:'medium', cls:'sev-medium', desc:'Faltan Content-Security-Policy y X-Frame-Options'},
  {icon:'i',name:'Versión de servidor expuesta', sev:'low', cls:'sev-low', desc:'Header Server revela Apache 2.4.1'},
  {icon:'⚠',name:'CSRF sin protección en formularios', sev:'high', cls:'sev-high', desc:'No se detectó token CSRF'},
  {icon:'!',name:'Cookies sin flag HttpOnly', sev:'medium', cls:'sev-medium', desc:'Cookies de sesión accesibles desde JS'},
];
 
const scanSteps = [
  '[*] Iniciando conexión con objetivo...',
  '[*] Resolución DNS completada',
  '[*] Puerto 80 abierto (HTTP)',
  '[*] Puerto 443 abierto (HTTPS)',
  '[+] SSL/TLS: TLSv1.3 detectado',
  '[*] Detectando tecnologías...',
  '[+] CMS: WordPress 6.2.1',
  '[*] Escaneando formularios y parámetros...',
  '[!] Posible inyección SQL en /api/login',
  '[!] XSS detectado en campo de búsqueda',
  '[*] Verificando cabeceras HTTP...',
  '[!] Cabeceras de seguridad faltantes',
  '[*] Comprobando cookies de sesión...',
  '[!] Cookies sin HttpOnly/Secure',
  '[*] Revisando tokens CSRF...',
  '[!] CSRF sin validación en /contact',
  '[*] Generando reporte final...',
];
 
let scanning = false;
async function startScan() {
  if (scanning) return;
  scanning = true;
  const btn = document.getElementById('scan-btn');
  btn.disabled = true;
  const target = document.getElementById('scan-target').value || 'https://ejemplo.com';
 
  document.getElementById('scan-progress').style.display = 'block';
  document.getElementById('scan-results').style.display = 'none';
  const terminal = document.getElementById('scan-terminal');
  terminal.innerHTML = <span style="color:var(--accent)">[CyberShield] Escaneando: ${target}</span><br>;
 
  const bar = document.getElementById('scan-bar');
  const pct = document.getElementById('scan-pct');
  const status = document.getElementById('scan-status');
 
  for (let i = 0; i < scanSteps.length; i++) {
    await new Promise(r => setTimeout(r, 350));
    const progress = Math.round((i+1)/scanSteps.length*100);
    bar.style.width = progress + '%';
    pct.textContent = progress + '%';
    status.textContent = 'Escaneando...';
    const cls = scanSteps[i].startsWith('[!]') ? 't-warn' : scanSteps[i].startsWith('[+]') ? 't-info' : 't-dim';
    terminal.innerHTML += <span class="${cls}">${scanSteps[i]}</span><br>;
    terminal.scrollTop = terminal.scrollHeight;
  }
 
  await new Promise(r => setTimeout(r, 400));
  terminal.innerHTML += <br><span style="color:var(--success)">[✓] Escaneo completado — ${vulnDB.length} vulnerabilidades encontradas</span>;
  status.textContent = 'Completado';
 
  const vl = document.getElementById('vuln-list');
  vl.innerHTML = '';
  let crit=0, high=0, med=0, low=0;
  vulnDB.forEach(v => {
    if(v.sev==='critical') crit++;
    else if(v.sev==='high') high++;
    else if(v.sev==='medium') med++;
    else low++;
    const d = document.createElement('div');
    d.className = 'vuln-item';
    d.innerHTML = `<div class="vuln-icon">${v.icon}</div>
      <div style="flex:1;">
        <div class="vuln-name">${v.name}</div>
        <div style="font-size:11px;color:var(--text3);margin-top:2px;">${v.desc}</div>
      </div>
      <span class="vuln-severity ${v.cls}">${v.sev.toUpperCase()}</span>`;
    vl.appendChild(d);
  });
 
  document.getElementById('scan-summary').innerHTML =
    <span style="color:var(--danger);margin-right:8px;">${crit} críticas</span> +
    <span style="color:#ff9632;margin-right:8px;">${high} altas</span> +
    <span style="color:var(--warning);margin-right:8px;">${med} medias</span> +
    <span style="color:var(--success)">${low} bajas</span>;
 
  document.getElementById('scan-results').style.display = 'block';
  btn.disabled = false;
  scanning = false;
  showToast('Escaneo completado', 'ok');
}
 
// ========= FIREWALL =========
const wafRules = [
  {label:'Protección SQL Injection', on: true},
  {label:'Protección XSS', on: true},
  {label:'Bloqueo de bots maliciosos', on: true},
  {label:'Protección CSRF', on: false},
  {label:'Rate limiting (100 req/min)', on: true},
  {label:'Bloqueo por geolocalización', on: false},
];
 
const wt = document.getElementById('waf-toggles');
wafRules.forEach((r, i) => {
  const d = document.createElement('div');
  d.className = 'toggle-wrap';
  d.innerHTML = `<div class="toggle ${r.on?'on':''}" id="waf-${i}" onclick="toggleWaf(${i})"></div>
    <span style="font-size:12px;color:var(--text2)">${r.label}</span>`;
  wt.appendChild(d);
});
 
function toggleWaf(i) {
  wafRules[i].on = !wafRules[i].on;
  const el = document.getElementById('waf-'+i);
  el.className = 'toggle' + (wafRules[i].on ? ' on' : '');
  showToast(wafRules[i].label + (wafRules[i].on?' activada':' desactivada'), wafRules[i].on?'ok':'err');
}
 
let rulesData = [
  {name:'Bloquear Tor Nodes', type:'IP', origin:'Lista TOR', action:'BLOQUEAR', active:true, hits:1204},
  {name:'Permitir oficina', type:'IP', origin:'192.168.1.0/24', action:'PERMITIR', active:true, hits:8821},
  {name:'Bloquear User-Agents maliciosos', type:'User-Agent', origin:'sqlmap, nikto', action:'BLOQUEAR', active:true, hits:334},
  {name:'Limitar API', type:'Ruta URL', origin:'/api/*', action:'LIMITAR', active:true, hits:4492},
  {name:'Bloquear Rusia', type:'País', origin:'RU', action:'BLOQUEAR', active:false, hits:0},
];
 
function renderRules() {
  const tbody = document.getElementById('rules-body');
  tbody.innerHTML = '';
  rulesData.forEach((r, i) => {
    const tr = document.createElement('tr');
    tr.innerHTML = `
      <td style="color:var(--text)">${r.name}</td>
      <td>${r.type}</td>
      <td style="font-family:var(--mono);font-size:11px;color:var(--info)">${r.origin}</td>
      <td><span class="vuln-severity ${r.action==='BLOQUEAR'?'sev-critical':r.action==='PERMITIR'?'sev-low':'sev-medium'}">${r.action}</span></td>
      <td><span style="color:${r.active?'var(--success)':'var(--text3)'};font-size:11px;">${r.active?'Activa':'Inactiva'}</span></td>
      <td style="color:var(--text2)">${r.hits.toLocaleString()}</td>
      <td><button class="btn btn-outline" style="padding:4px 10px;font-size:10px;" onclick="removeRule(${i})">Eliminar</button></td>`;
    tbody.appendChild(tr);
  });
  document.getElementById('fw-rules').textContent = rulesData.filter(r=>r.active).length;
}
renderRules();
 
function removeRule(i) {
  rulesData.splice(i, 1);
  renderRules();
  showToast('Regla eliminada', 'ok');
}
 
function blockIP() {
  const ip = document.getElementById('block-ip').value.trim();
  const reason = document.getElementById('block-reason').value.trim() || 'Actividad sospechosa';
  if (!ip) { showToast('Ingresa una dirección IP', 'err'); return; }
  rulesData.unshift({name:'Bloquear ' + ip, type:'IP', origin:ip, action:'BLOQUEAR', active:true, hits:0});
  renderRules();
  document.getElementById('block-ip').value = '';
  document.getElementById('block-reason').value = '';
  const bl = parseInt(document.getElementById('fw-blacklist').textContent) + 1;
  document.getElementById('fw-blacklist').textContent = bl;
  showToast('IP ' + ip + ' bloqueada', 'ok');
}
 
function openAddRule() { document.getElementById('rule-modal').classList.add('open'); }
function closeModal() { document.getElementById('rule-modal').classList.remove('open'); }
 
function addRule() {
  const name = document.getElementById('rule-name').value.trim();
  const type = document.getElementById('rule-type').value;
  const val = document.getElementById('rule-value').value.trim();
  const action = document.getElementById('rule-action').value;
  if (!name || !val) { showToast('Completa todos los campos', 'err'); return; }
  rulesData.push({name, type, origin:val, action, active:true, hits:0});
  renderRules();
  closeModal();
  showToast('Regla creada: ' + name, 'ok');
}
 
// Close modal on overlay click
document.getElementById('rule-modal').addEventListener('click', function(e) {
  if (e.target === this) closeModal();
});
</script>
</body>
</html>
