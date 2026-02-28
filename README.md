<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="UTF-8"/>
<meta name="viewport" content="width=device-width, initial-scale=1.0"/>
<title>Buda-sys // Ciberespacio</title>
<link href="https://fonts.googleapis.com/css2?family=Share+Tech+Mono&family=Orbitron:wght@400;700;900&family=VT323&display=swap" rel="stylesheet"/>
<style>
  :root {
    --neon-purple: #bb33ff;
    --neon-green: #33ff33;
    --neon-pink: #ff33aa;
    --neon-cyan: #00ffff;
    --dark-bg: #05000d;
    --panel-bg: rgba(187,51,255,0.04);
    --panel-border: rgba(187,51,255,0.25);
    --text-dim: #888;
    --text-bright: #eee;
  }

  * { margin:0; padding:0; box-sizing:border-box; }

  body {
    background: var(--dark-bg);
    color: var(--text-bright);
    font-family: 'Share Tech Mono', monospace;
    min-height: 100vh;
    overflow-x: hidden;
    cursor: crosshair;
  }

  /* Scanlines overlay */
  body::before {
    content:'';
    position: fixed;
    inset:0;
    background: repeating-linear-gradient(
      0deg,
      transparent,
      transparent 2px,
      rgba(0,0,0,0.07) 2px,
      rgba(0,0,0,0.07) 4px
    );
    pointer-events: none;
    z-index: 100;
  }

  /* Grid background */
  body::after {
    content:'';
    position: fixed;
    inset:0;
    background-image:
      linear-gradient(rgba(187,51,255,0.05) 1px, transparent 1px),
      linear-gradient(90deg, rgba(187,51,255,0.05) 1px, transparent 1px);
    background-size: 40px 40px;
    pointer-events: none;
    z-index: 0;
  }

  .wrapper {
    max-width: 900px;
    margin: 0 auto;
    padding: 40px 24px;
    position: relative;
    z-index: 1;
  }

  /* ─── HEADER ─── */
  .header {
    text-align: center;
    margin-bottom: 48px;
    position: relative;
  }

  .glitch-title {
    font-family: 'Orbitron', sans-serif;
    font-size: clamp(2rem, 5vw, 3.2rem);
    font-weight: 900;
    letter-spacing: 0.08em;
    position: relative;
    color: #fff;
    animation: flicker 8s infinite;
  }

  .glitch-title span.purple { color: var(--neon-purple); text-shadow: 0 0 20px var(--neon-purple), 0 0 40px var(--neon-purple); }
  .glitch-title span.green  { color: var(--neon-green);  text-shadow: 0 0 20px var(--neon-green),  0 0 40px var(--neon-green); }

  .glitch-title::before,
  .glitch-title::after {
    content: attr(data-text);
    position: absolute;
    inset: 0;
    opacity: 0;
  }
  .glitch-title::before {
    color: var(--neon-cyan);
    animation: glitch-a 6s infinite;
    clip-path: polygon(0 20%, 100% 20%, 100% 40%, 0 40%);
    transform: translate(-3px, 0);
  }
  .glitch-title::after {
    color: var(--neon-pink);
    animation: glitch-b 6s infinite 0.3s;
    clip-path: polygon(0 60%, 100% 60%, 100% 80%, 0 80%);
    transform: translate(3px, 0);
  }

  @keyframes glitch-a {
    0%,94%,100% { opacity:0 }
    95%,96% { opacity:0.7 }
  }
  @keyframes glitch-b {
    0%,96%,100% { opacity:0 }
    97%,98% { opacity:0.6 }
  }
  @keyframes flicker {
    0%,98%,100% { opacity:1 }
    99% { opacity:0.85 }
  }

  .terminal-line {
    font-family: 'Share Tech Mono', monospace;
    font-size: 0.85rem;
    color: var(--neon-green);
    margin-top: 16px;
    overflow: hidden;
    white-space: nowrap;
    border-right: 2px solid var(--neon-green);
    width: fit-content;
    margin-inline: auto;
    animation: typing 3s steps(60) 0.5s forwards, blink-caret 0.75s step-end infinite;
    max-width: 100%;
  }

  @keyframes typing {
    from { width: 0 }
    to { width: 100% }
  }
  @keyframes blink-caret {
    from,to { border-color: transparent }
    50% { border-color: var(--neon-green) }
  }

  /* ─── DIVIDER ─── */
  .divider {
    display: flex;
    align-items: center;
    gap: 12px;
    margin: 32px 0;
    opacity: 0.5;
  }
  .divider::before, .divider::after {
    content:'';
    flex:1;
    height: 1px;
    background: linear-gradient(90deg, transparent, var(--neon-purple), transparent);
  }
  .divider span { color: var(--neon-purple); font-size: 0.7rem; letter-spacing: 0.2em; white-space: nowrap; }

  /* ─── PANELS ─── */
  .panel {
    background: var(--panel-bg);
    border: 1px solid var(--panel-border);
    padding: 24px 28px;
    margin-bottom: 24px;
    position: relative;
    transition: border-color 0.3s, box-shadow 0.3s;
  }
  .panel:hover {
    border-color: rgba(187,51,255,0.6);
    box-shadow: 0 0 20px rgba(187,51,255,0.1), inset 0 0 20px rgba(187,51,255,0.03);
  }
  /* Corner cuts */
  .panel::before {
    content:'';
    position: absolute;
    top: -1px; right: -1px;
    width: 16px; height: 16px;
    border-top: 1px solid var(--neon-purple);
    border-right: 1px solid var(--neon-purple);
    background: var(--dark-bg);
  }
  .panel-title {
    font-family: 'Orbitron', sans-serif;
    font-size: 0.75rem;
    font-weight: 700;
    letter-spacing: 0.25em;
    color: var(--neon-purple);
    text-transform: uppercase;
    margin-bottom: 18px;
    display: flex;
    align-items: center;
    gap: 10px;
  }
  .panel-title::after {
    content:'';
    flex:1;
    height:1px;
    background: linear-gradient(90deg, var(--neon-purple), transparent);
    opacity:0.4;
  }

  /* ─── PROFILE GRID ─── */
  .profile-grid {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 10px;
  }
  @media(max-width:600px){ .profile-grid { grid-template-columns:1fr } }

  .profile-item {
    display: flex;
    align-items: flex-start;
    gap: 10px;
    padding: 10px 12px;
    background: rgba(0,0,0,0.3);
    border-left: 2px solid rgba(187,51,255,0.3);
    font-size: 0.82rem;
    line-height: 1.5;
    transition: border-color 0.2s, background 0.2s;
  }
  .profile-item:hover { border-color: var(--neon-purple); background: rgba(187,51,255,0.07); }
  .profile-item .icon { font-size: 1rem; flex-shrink:0; margin-top:2px; }
  .profile-item .text { color: #ccc; }
  .profile-item .text strong { color: var(--neon-green); }

  /* ─── SKILLS GRID ─── */
  .skills-grid {
    display: flex;
    flex-wrap: wrap;
    gap: 10px;
  }
  .skill-badge {
    display: flex;
    align-items: center;
    gap: 8px;
    padding: 8px 16px;
    background: rgba(0,0,0,0.5);
    border: 1px solid rgba(51,255,51,0.2);
    font-size: 0.8rem;
    color: var(--neon-green);
    letter-spacing: 0.1em;
    transition: all 0.2s;
    cursor: default;
  }
  .skill-badge:hover {
    border-color: var(--neon-green);
    background: rgba(51,255,51,0.08);
    box-shadow: 0 0 12px rgba(51,255,51,0.15);
    transform: translateY(-1px);
  }
  .skill-badge .dot {
    width: 6px; height: 6px;
    border-radius: 50%;
    background: var(--neon-green);
    box-shadow: 0 0 6px var(--neon-green);
    animation: pulse 2s infinite;
  }
  @keyframes pulse {
    0%,100% { opacity:1 }
    50% { opacity:0.4 }
  }

  /* ─── TOOLS ─── */
  .tools-grid {
    display: flex;
    flex-wrap: wrap;
    gap: 10px;
  }
  .tool-tag {
    padding: 6px 14px;
    border: 1px solid rgba(187,51,255,0.3);
    font-size: 0.78rem;
    color: #bb88ff;
    letter-spacing: 0.08em;
    background: rgba(187,51,255,0.05);
    transition: all 0.2s;
    cursor: default;
  }
  .tool-tag:hover {
    border-color: var(--neon-purple);
    background: rgba(187,51,255,0.12);
    color: #fff;
    box-shadow: 0 0 10px rgba(187,51,255,0.2);
  }

  /* ─── PROJECTS ─── */
  .project-card {
    background: rgba(0,0,0,0.4);
    border: 1px solid rgba(187,51,255,0.2);
    padding: 20px 22px;
    margin-bottom: 14px;
    position: relative;
    overflow: hidden;
    transition: all 0.3s;
  }
  .project-card:hover {
    border-color: rgba(187,51,255,0.5);
    box-shadow: 0 0 24px rgba(187,51,255,0.08);
  }
  .project-card::after {
    content:'';
    position:absolute;
    top:0; left:-100%;
    width:60%; height:100%;
    background: linear-gradient(90deg, transparent, rgba(187,51,255,0.04), transparent);
    transition: left 0.5s;
  }
  .project-card:hover::after { left:150%; }

  .project-header {
    display: flex;
    align-items: center;
    gap: 10px;
    margin-bottom: 10px;
  }
  .project-status {
    font-size: 0.65rem;
    padding: 3px 8px;
    letter-spacing: 0.15em;
    text-transform: uppercase;
  }
  .status-active  { background: rgba(51,255,51,0.1);  border:1px solid rgba(51,255,51,0.4);  color: var(--neon-green); }
  .status-wip     { background: rgba(255,170,0,0.1);  border:1px solid rgba(255,170,0,0.4);  color: #ffaa00; }

  .project-name {
    font-family: 'Orbitron', sans-serif;
    font-size: 0.9rem;
    font-weight: 700;
    color: #fff;
    letter-spacing: 0.06em;
  }

  .project-desc {
    font-size: 0.8rem;
    color: #aaa;
    line-height: 1.6;
    margin-bottom: 12px;
  }

  .project-tags {
    display: flex;
    flex-wrap: wrap;
    gap: 6px;
  }
  .ptag {
    font-size: 0.7rem;
    padding: 2px 8px;
    background: rgba(0,255,255,0.06);
    border: 1px solid rgba(0,255,255,0.2);
    color: var(--neon-cyan);
    letter-spacing: 0.08em;
  }

  /* ─── CONTACT ─── */
  .contact-grid {
    display: flex;
    flex-wrap: wrap;
    gap: 12px;
    justify-content: center;
  }
  .contact-btn {
    display: flex;
    align-items: center;
    gap: 8px;
    padding: 10px 20px;
    background: rgba(0,0,0,0.5);
    border: 1px solid rgba(187,51,255,0.3);
    color: #bb88ff;
    text-decoration: none;
    font-family: 'Share Tech Mono', monospace;
    font-size: 0.8rem;
    letter-spacing: 0.12em;
    transition: all 0.25s;
  }
  .contact-btn:hover {
    border-color: var(--neon-purple);
    color: #fff;
    background: rgba(187,51,255,0.12);
    box-shadow: 0 0 16px rgba(187,51,255,0.2);
    transform: translateY(-2px);
  }

  /* ─── STATS BAR ─── */
  .stat-row {
    display: flex;
    align-items: center;
    gap: 14px;
    margin-bottom: 12px;
  }
  .stat-label {
    font-size: 0.75rem;
    color: var(--text-dim);
    width: 120px;
    flex-shrink: 0;
    letter-spacing: 0.08em;
  }
  .stat-bar-wrap {
    flex: 1;
    height: 4px;
    background: rgba(255,255,255,0.05);
    position: relative;
    overflow: hidden;
  }
  .stat-bar {
    height: 100%;
    position: relative;
    transform-origin: left;
    animation: bar-in 1.2s ease forwards;
  }
  @keyframes bar-in {
    from { transform: scaleX(0) }
    to { transform: scaleX(1) }
  }
  .bar-purple { background: linear-gradient(90deg, #7700cc, var(--neon-purple)); box-shadow: 0 0 8px var(--neon-purple); }
  .bar-green  { background: linear-gradient(90deg, #006600, var(--neon-green));  box-shadow: 0 0 8px var(--neon-green); }
  .bar-cyan   { background: linear-gradient(90deg, #005555, var(--neon-cyan));   box-shadow: 0 0 8px var(--neon-cyan); }
  .stat-val {
    font-size: 0.75rem;
    color: var(--text-dim);
    width: 36px;
    text-align: right;
    flex-shrink:0;
  }

  /* ─── FOOTER QUOTE ─── */
  .footer-quote {
    text-align: center;
    margin-top: 48px;
    padding: 28px;
    border: 1px solid rgba(187,51,255,0.2);
    position: relative;
    background: rgba(187,51,255,0.03);
  }
  .footer-quote blockquote {
    font-family: 'VT323', monospace;
    font-size: 1.5rem;
    color: var(--neon-purple);
    text-shadow: 0 0 16px var(--neon-purple);
    letter-spacing: 0.05em;
    line-height: 1.5;
  }
  .footer-meta {
    margin-top: 20px;
    font-size: 0.72rem;
    color: var(--text-dim);
    letter-spacing: 0.1em;
  }
  .footer-meta span { color: var(--neon-green); }
  .footer-meta em { color: var(--neon-pink); font-style: normal; }

  /* ─── BOOT SEQUENCE ─── */
  .boot-line {
    font-size: 0.75rem;
    color: #555;
    margin-bottom: 4px;
    animation: fade-in 0.3s both;
  }
  .boot-line.ok::after { content: ' [OK]'; color: var(--neon-green); }
  .boot-line:nth-child(1) { animation-delay:0.1s }
  .boot-line:nth-child(2) { animation-delay:0.4s }
  .boot-line:nth-child(3) { animation-delay:0.7s }
  .boot-line:nth-child(4) { animation-delay:1.0s }
  @keyframes fade-in { from{opacity:0;transform:translateY(4px)} to{opacity:1;transform:none} }

  /* ─── 2-COL LAYOUT ─── */
  .two-col {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 24px;
  }
  @media(max-width:680px){ .two-col { grid-template-columns:1fr } }
</style>
</head>
<body>
<div class="wrapper">

  <!-- BOOT -->
  <div style="margin-bottom:32px">
    <div class="boot-line ok">// Initializing Buda-sys kernel...</div>
    <div class="boot-line ok">// Mounting offensive modules...</div>
    <div class="boot-line ok">// C2 channels established...</div>
    <div class="boot-line" style="color:#bb33ff;animation-delay:1.3s">// SESSION ACTIVE ▮</div>
  </div>

  <!-- HEADER -->
  <header class="header">
    <div class="glitch-title" data-text="👾 BUDA-SYS">
      👾 <span class="purple">BUDA</span>-<span class="green">SYS</span>
    </div>
    <div style="font-family:'Orbitron',sans-serif; font-size:0.7rem; letter-spacing:0.4em; color:#555; margin-top:8px; text-transform:uppercase;">
      Red Team Operator // Offensive Security
    </div>
    <div class="terminal-line">[ + ] Ciberespacio cargado — bienvenido al lado ofensivo</div>
  </header>

  <div class="divider"><span>◈ PERFIL ◈</span></div>

  <!-- PROFILE -->
  <div class="panel">
    <div class="panel-title">⬡ Identidad del operador</div>
    <div class="profile-grid">
      <div class="profile-item">
        <span class="icon">🧠</span>
        <div class="text"><strong>Rol:</strong> Explorador ético del lado ofensivo</div>
      </div>
      <div class="profile-item">
        <span class="icon">🎯</span>
        <div class="text"><strong>Focus:</strong> Red Team · Active Directory · Evasión · Post-explotación</div>
      </div>
      <div class="profile-item">
        <span class="icon">🛠️</span>
        <div class="text"><strong>Dev:</strong> Herramientas ofensivas & laboratorios educativos</div>
      </div>
      <div class="profile-item">
        <span class="icon">💻</span>
        <div class="text"><strong>Entornos:</strong> Linux · Windows · AD · Pivoting · Exfiltración</div>
      </div>
      <div class="profile-item">
        <span class="icon">🦠</span>
        <div class="text"><strong>Interés:</strong> Malware realista para análisis e investigación</div>
      </div>
      <div class="profile-item">
        <span class="icon">🚩</span>
        <div class="text"><strong>CTFs:</strong> Jugador activo & creador de entornos vulnerables</div>
      </div>
    </div>
  </div>

  <div class="divider"><span>◈ ARSENAL ◈</span></div>

  <!-- SKILLS + TOOLS -->
  <div class="two-col">
    <div class="panel">
      <div class="panel-title">⬡ Lenguajes & Scripting</div>
      <div class="skills-grid">
        <div class="skill-badge"><div class="dot"></div> Python</div>
        <div class="skill-badge"><div class="dot"></div> Bash</div>
        <div class="skill-badge"><div class="dot"></div> PowerShell</div>
        <div class="skill-badge"><div class="dot"></div> Rust</div>
      </div>

      <div style="margin-top:24px">
        <div class="panel-title" style="font-size:0.65rem; margin-bottom:12px">⬡ Proficiencia</div>
        <div class="stat-row">
          <div class="stat-label">Python</div>
          <div class="stat-bar-wrap"><div class="stat-bar bar-green" style="width:90%"></div></div>
          <div class="stat-val">90%</div>
        </div>
        <div class="stat-row">
          <div class="stat-label">Bash</div>
          <div class="stat-bar-wrap"><div class="stat-bar bar-green" style="width:85%"></div></div>
          <div class="stat-val">85%</div>
        </div>
        <div class="stat-row">
          <div class="stat-label">PowerShell</div>
          <div class="stat-bar-wrap"><div class="stat-bar bar-cyan" style="width:75%"></div></div>
          <div class="stat-val">75%</div>
        </div>
        <div class="stat-row">
          <div class="stat-label">Rust</div>
          <div class="stat-bar-wrap"><div class="stat-bar bar-purple" style="width:40%"></div></div>
          <div class="stat-val">WIP</div>
        </div>
      </div>
    </div>

    <div class="panel">
      <div class="panel-title">⬡ Frameworks & Herramientas</div>
      <div class="tools-grid">
        <div class="tool-tag">Metasploit</div>
        <div class="tool-tag">BloodHound</div>
        <div class="tool-tag">Impacket</div>
        <div class="tool-tag">CrackMapExec</div>
        <div class="tool-tag">Cobalt Strike</div>
        <div class="tool-tag">Mimikatz</div>
        <div class="tool-tag">Nmap</div>
        <div class="tool-tag">Burp Suite</div>
        <div class="tool-tag">Evil-WinRM</div>
        <div class="tool-tag">Responder</div>
        <div class="tool-tag">Kerbrute</div>
        <div class="tool-tag">Netexec</div>
      </div>
    </div>
  </div>

  <div class="divider"><span>◈ PROYECTOS ◈</span></div>

  <!-- PROJECTS -->
  <div class="panel">
    <div class="panel-title">⬡ Operaciones destacadas</div>

    <div class="project-card">
      <div class="project-header">
        <div class="project-name">RAT + C2 sobre Discord</div>
        <div class="project-status status-active">ACTIVO</div>
      </div>
      <div class="project-desc">
        Control remoto mediante canales privados de Discord. Arquitectura C2 encubierta, ideal para laboratorios de análisis y escenarios de post-explotación controlados.
      </div>
      <div class="project-tags">
        <div class="ptag">Python</div>
        <div class="ptag">C2 Framework</div>
        <div class="ptag">Post-Explotación</div>
        <div class="ptag">Laboratorio</div>
      </div>
    </div>

    <div class="project-card">
      <div class="project-header">
        <div class="project-name">Active Directory Labs (THM-style)</div>
        <div class="project-status status-active">ACTIVO</div>
      </div>
      <div class="project-desc">
        Máquinas vulnerables diseñadas para entrenar ataques reales sobre AD: Password Spraying, misconfiguraciones de GPO, abuso de privilegios, Kerberoasting y dump de credenciales offline.
      </div>
      <div class="project-tags">
        <div class="ptag">Active Directory</div>
        <div class="ptag">Kerberoasting</div>
        <div class="ptag">GPO Abuse</div>
        <div class="ptag">Cred Dump</div>
        <div class="ptag">Red Team</div>
      </div>
    </div>

    <div class="project-card">
      <div class="project-header">
        <div class="project-name">Port Scanner — Rust</div>
        <div class="project-status status-wip">EN DESARROLLO</div>
      </div>
      <div class="project-desc">
        Escáner de puertos de alto rendimiento construido en Rust. Objetivo: velocidad nativa, bajo footprint, integrable en cadenas de reconocimiento ofensivo.
      </div>
      <div class="project-tags">
        <div class="ptag">Rust</div>
        <div class="ptag">Networking</div>
        <div class="ptag">Reconocimiento</div>
        <div class="ptag">OSINT</div>
      </div>
    </div>
  </div>

  <div class="divider"><span>◈ CONTACTO ◈</span></div>

  <!-- CONTACT -->
  <div class="panel">
    <div class="panel-title">⬡ Canales de comunicación</div>
    <div class="contact-grid">
      <a class="contact-btn" href="https://github.com/buda-sys" target="_blank">
        <svg width="16" height="16" viewBox="0 0 24 24" fill="currentColor"><path d="M12 0C5.37 0 0 5.37 0 12c0 5.31 3.435 9.795 8.205 11.385.6.105.825-.255.825-.57 0-.285-.015-1.23-.015-2.235-3.015.555-3.795-.735-4.035-1.41-.135-.345-.72-1.41-1.23-1.695-.42-.225-1.02-.78-.015-.795.945-.015 1.62.87 1.845 1.23 1.08 1.815 2.805 1.305 3.495.99.105-.78.42-1.305.765-1.605-2.67-.3-5.46-1.335-5.46-5.925 0-1.305.465-2.385 1.23-3.225-.12-.3-.54-1.53.12-3.18 0 0 1.005-.315 3.3 1.23.96-.27 1.98-.405 3-.405s2.04.135 3 .405c2.295-1.56 3.3-1.23 3.3-1.23.66 1.65.24 2.88.12 3.18.765.84 1.23 1.905 1.23 3.225 0 4.605-2.805 5.625-5.475 5.925.435.375.81 1.095.81 2.22 0 1.605-.015 2.895-.015 3.3 0 .315.225.69.825.57A12.02 12.02 0 0024 12c0-6.63-5.37-12-12-12z"/></svg>
        GitHub
      </a>
      <a class="contact-btn" href="https://www.tiktok.com/@buda_sys" target="_blank">
        <svg width="16" height="16" viewBox="0 0 24 24" fill="currentColor"><path d="M19.59 6.69a4.83 4.83 0 01-3.77-4.25V2h-3.45v13.67a2.89 2.89 0 01-2.88 2.5 2.89 2.89 0 01-2.89-2.89 2.89 2.89 0 012.89-2.89c.28 0 .54.04.79.1V9.01a6.33 6.33 0 00-.79-.05 6.34 6.34 0 00-6.34 6.34 6.34 6.34 0 006.34 6.34 6.34 6.34 0 006.33-6.34V8.69a8.27 8.27 0 004.84 1.55V6.79a4.85 4.85 0 01-1.07-.1z"/></svg>
        TikTok
      </a>
      <a class="contact-btn" href="mailto:dark.exe1001@gmail.com">
        <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M4 4h16c1.1 0 2 .9 2 2v12c0 1.1-.9 2-2 2H4c-1.1 0-2-.9-2-2V6c0-1.1.9-2 2-2z"/><polyline points="22,6 12,13 2,6"/></svg>
        Email
      </a>
      <a class="contact-btn" href="https://discord.gg/demondark00" target="_blank">
        <svg width="16" height="16" viewBox="0 0 24 24" fill="currentColor"><path d="M20.317 4.37a19.791 19.791 0 00-4.885-1.515.074.074 0 00-.079.037c-.21.375-.444.864-.608 1.25a18.27 18.27 0 00-5.487 0 12.64 12.64 0 00-.617-1.25.077.077 0 00-.079-.037A19.736 19.736 0 003.677 4.37a.07.07 0 00-.032.027C.533 9.046-.32 13.58.099 18.057a.082.082 0 00.031.057 19.9 19.9 0 005.993 3.03.078.078 0 00.084-.028 14.09 14.09 0 001.226-1.994.076.076 0 00-.041-.106 13.107 13.107 0 01-1.872-.892.077.077 0 01-.008-.128 10.2 10.2 0 00.372-.292.074.074 0 01.077-.01c3.928 1.793 8.18 1.793 12.062 0a.074.074 0 01.078.01c.12.098.246.198.373.292a.077.077 0 01-.006.127 12.299 12.299 0 01-1.873.892.077.077 0 00-.041.107c.36.698.772 1.362 1.225 1.993a.076.076 0 00.084.028 19.839 19.839 0 006.002-3.03.077.077 0 00.032-.054c.5-5.177-.838-9.674-3.549-13.66a.061.061 0 00-.031-.03z"/></svg>
        Discord
      </a>
    </div>
  </div>

  <!-- FOOTER -->
  <div class="footer-quote">
    <blockquote>"El conocimiento es mi payload. La ética, mi rootkit."</blockquote>
    <div class="footer-meta">
      Última edición: <span>26/07/2025</span> &nbsp;·&nbsp;
      Creador: <span>Buda-sys</span> &nbsp;·&nbsp;
      <em>Si estás leyendo esto… ya ejecutaste el binario.</em>
    </div>
    <div style="margin-top:10px; font-size:0.65rem; color:#555; letter-spacing:0.2em;">
      // EOF &nbsp;·&nbsp; BUDA-SYS v2.0 &nbsp;·&nbsp; OFFENSIVE.MODE=ON
    </div>
  </div>

</div>
</body>
</html>


