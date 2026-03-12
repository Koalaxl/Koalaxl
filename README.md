<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8"/>
<meta name="viewport" content="width=device-width, initial-scale=1.0"/>
<title>Zaidan Faaris Abidi — Dev Profile</title>
<link href="https://fonts.googleapis.com/css2?family=Share+Tech+Mono&family=Orbitron:wght@400;700;900&family=Rajdhani:wght@300;400;600;700&display=swap" rel="stylesheet"/>
<style>
  :root {
    --cyan: #00FFD1;
    --cyan-dim: #00ffd155;
    --green: #39FF14;
    --red: #FF2D55;
    --bg: #020810;
    --bg2: #050f1a;
    --panel: #081525;
    --panel-border: #0a2540;
    --text: #c8d8e8;
    --text-dim: #4a6a8a;
    --font-mono: 'Share Tech Mono', monospace;
    --font-display: 'Orbitron', sans-serif;
    --font-body: 'Rajdhani', sans-serif;
  }

  *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

  html { scroll-behavior: smooth; }

  body {
    background: var(--bg);
    color: var(--text);
    font-family: var(--font-body);
    font-size: 16px;
    overflow-x: hidden;
    cursor: none;
  }

  /* Custom cursor */
  .cursor {
    width: 12px; height: 12px;
    background: var(--cyan);
    border-radius: 50%;
    position: fixed;
    pointer-events: none;
    z-index: 9999;
    transition: transform 0.1s ease;
    box-shadow: 0 0 12px var(--cyan), 0 0 24px var(--cyan-dim);
  }
  .cursor-ring {
    width: 36px; height: 36px;
    border: 1.5px solid var(--cyan-dim);
    border-radius: 50%;
    position: fixed;
    pointer-events: none;
    z-index: 9998;
    transition: transform 0.15s ease, width 0.2s, height 0.2s;
    transform: translate(-50%, -50%);
  }

  /* Canvas background */
  #matrix-bg {
    position: fixed;
    top: 0; left: 0;
    width: 100%; height: 100%;
    z-index: 0;
    opacity: 0.18;
  }

  /* Scanlines overlay */
  body::after {
    content: '';
    position: fixed;
    inset: 0;
    background: repeating-linear-gradient(
      0deg,
      transparent,
      transparent 2px,
      rgba(0,0,0,0.08) 2px,
      rgba(0,0,0,0.08) 4px
    );
    pointer-events: none;
    z-index: 1000;
  }

  /* Main layout */
  .container {
    position: relative;
    z-index: 10;
    max-width: 960px;
    margin: 0 auto;
    padding: 40px 24px 80px;
  }

  /* ── HERO ── */
  .hero {
    text-align: center;
    padding: 60px 0 40px;
    animation: fadeSlideDown 0.8s ease both;
  }

  .hero-status {
    display: inline-flex;
    align-items: center;
    gap: 8px;
    background: var(--panel);
    border: 1px solid var(--panel-border);
    padding: 6px 16px;
    border-radius: 100px;
    font-family: var(--font-mono);
    font-size: 12px;
    color: var(--text-dim);
    letter-spacing: 0.1em;
    margin-bottom: 32px;
  }
  .status-dot {
    width: 8px; height: 8px;
    background: var(--green);
    border-radius: 50%;
    animation: pulse-green 1.5s ease-in-out infinite;
    box-shadow: 0 0 8px var(--green);
  }

  .glitch-name {
    font-family: var(--font-display);
    font-size: clamp(32px, 6vw, 64px);
    font-weight: 900;
    letter-spacing: 0.05em;
    color: #fff;
    position: relative;
    display: inline-block;
    text-transform: uppercase;
    text-shadow: 0 0 40px rgba(0,255,209,0.3);
    animation: glitch-flicker 6s infinite;
  }
  .glitch-name::before,
  .glitch-name::after {
    content: attr(data-text);
    position: absolute;
    top: 0; left: 0; width: 100%;
    font-family: var(--font-display);
    font-weight: 900;
  }
  .glitch-name::before {
    color: var(--red);
    animation: glitch-before 4s 1s infinite;
    clip-path: polygon(0 30%, 100% 30%, 100% 50%, 0 50%);
  }
  .glitch-name::after {
    color: var(--cyan);
    animation: glitch-after 4s 1.5s infinite;
    clip-path: polygon(0 60%, 100% 60%, 100% 80%, 0 80%);
  }

  .hero-subtitle {
    font-family: var(--font-mono);
    font-size: 14px;
    color: var(--cyan);
    letter-spacing: 0.25em;
    text-transform: uppercase;
    margin-top: 12px;
    animation: fadeIn 1s 0.4s both;
  }

  /* Typing line */
  .typing-line {
    display: flex;
    align-items: center;
    justify-content: center;
    gap: 6px;
    margin-top: 24px;
    font-family: var(--font-mono);
    font-size: 15px;
    color: var(--text-dim);
    animation: fadeIn 1s 0.6s both;
  }
  .typing-text { color: var(--text); }
  .blink-cursor {
    display: inline-block;
    width: 10px; height: 18px;
    background: var(--cyan);
    animation: blink 1s step-end infinite;
    box-shadow: 0 0 8px var(--cyan);
  }

  /* Badges */
  .hero-badges {
    display: flex;
    justify-content: center;
    flex-wrap: wrap;
    gap: 10px;
    margin-top: 28px;
    animation: fadeIn 1s 0.8s both;
  }
  .badge {
    display: flex;
    align-items: center;
    gap: 6px;
    background: var(--panel);
    border: 1px solid var(--panel-border);
    padding: 6px 14px;
    border-radius: 6px;
    font-family: var(--font-mono);
    font-size: 12px;
    color: var(--text-dim);
    transition: border-color 0.2s, color 0.2s, box-shadow 0.2s;
  }
  .badge:hover {
    border-color: var(--cyan);
    color: var(--cyan);
    box-shadow: 0 0 16px var(--cyan-dim);
  }

  /* ── DIVIDER ── */
  .divider {
    display: flex;
    align-items: center;
    gap: 16px;
    margin: 48px 0 32px;
    opacity: 0;
    animation: fadeIn 0.5s forwards;
  }
  .divider-line { flex: 1; height: 1px; background: linear-gradient(90deg, transparent, var(--panel-border), transparent); }
  .divider-label {
    font-family: var(--font-mono);
    font-size: 11px;
    color: var(--text-dim);
    letter-spacing: 0.2em;
    text-transform: uppercase;
    white-space: nowrap;
  }
  .divider-label span { color: var(--cyan); }

  /* ── PANELS ── */
  .panel {
    background: var(--panel);
    border: 1px solid var(--panel-border);
    border-radius: 12px;
    overflow: hidden;
    position: relative;
    opacity: 0;
    transform: translateY(24px);
    transition: border-color 0.3s, box-shadow 0.3s;
  }
  .panel:hover {
    border-color: #0e3860;
    box-shadow: 0 0 40px rgba(0,255,209,0.05), 0 8px 40px rgba(0,0,0,0.4);
  }
  .panel.visible { animation: slideUp 0.6s ease forwards; }

  .panel-header {
    display: flex;
    align-items: center;
    gap: 10px;
    padding: 14px 20px;
    border-bottom: 1px solid var(--panel-border);
    background: rgba(0,0,0,0.2);
  }
  .panel-dot { width: 10px; height: 10px; border-radius: 50%; }
  .dot-red { background: #FF5F57; }
  .dot-yellow { background: #FEBC2E; }
  .dot-green { background: #28C840; }
  .panel-title {
    font-family: var(--font-mono);
    font-size: 12px;
    color: var(--text-dim);
    margin-left: 4px;
    letter-spacing: 0.1em;
  }
  .panel-body { padding: 24px; }

  /* ── WHOAMI GRID ── */
  .whoami-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 16px; }
  @media (max-width: 600px) { .whoami-grid { grid-template-columns: 1fr; } }

  .info-row {
    display: flex;
    gap: 10px;
    padding: 10px 14px;
    background: rgba(0,0,0,0.2);
    border-radius: 8px;
    border: 1px solid transparent;
    transition: border-color 0.2s, background 0.2s;
    align-items: flex-start;
  }
  .info-row:hover { border-color: var(--panel-border); background: rgba(0,255,209,0.03); }
  .info-key {
    font-family: var(--font-mono);
    font-size: 11px;
    color: var(--cyan);
    min-width: 70px;
    padding-top: 2px;
    letter-spacing: 0.05em;
  }
  .info-val {
    font-family: var(--font-body);
    font-size: 14px;
    color: var(--text);
    line-height: 1.5;
    font-weight: 400;
  }

  /* ── TECH STACK ── */
  .tech-section { margin-bottom: 24px; }
  .tech-section-title {
    font-family: var(--font-mono);
    font-size: 11px;
    color: var(--text-dim);
    letter-spacing: 0.2em;
    text-transform: uppercase;
    margin-bottom: 12px;
    padding-left: 2px;
  }
  .tech-section-title span { color: var(--cyan); }
  .tech-pills { display: flex; flex-wrap: wrap; gap: 8px; }
  .tech-pill {
    display: flex;
    align-items: center;
    gap: 8px;
    background: rgba(0,0,0,0.3);
    border: 1px solid var(--panel-border);
    border-radius: 8px;
    padding: 8px 14px;
    font-family: var(--font-mono);
    font-size: 12px;
    color: var(--text);
    cursor: default;
    transition: all 0.2s ease;
    position: relative;
    overflow: hidden;
  }
  .tech-pill::before {
    content: '';
    position: absolute;
    inset: 0;
    background: var(--pill-color, var(--cyan));
    opacity: 0;
    transition: opacity 0.2s;
  }
  .tech-pill:hover {
    border-color: var(--pill-color, var(--cyan));
    color: var(--pill-color, var(--cyan));
    box-shadow: 0 0 20px color-mix(in srgb, var(--pill-color, var(--cyan)) 30%, transparent);
    transform: translateY(-2px);
  }
  .tech-pill .pill-icon { font-size: 16px; }

  /* ── SKILL BARS ── */
  .skill-item { margin-bottom: 20px; }
  .skill-header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-bottom: 8px;
  }
  .skill-name {
    font-family: var(--font-mono);
    font-size: 13px;
    color: var(--text);
    display: flex;
    align-items: center;
    gap: 8px;
  }
  .skill-pct {
    font-family: var(--font-mono);
    font-size: 11px;
    color: var(--cyan);
  }
  .skill-track {
    height: 6px;
    background: rgba(255,255,255,0.06);
    border-radius: 100px;
    overflow: hidden;
    position: relative;
  }
  .skill-fill {
    height: 100%;
    border-radius: 100px;
    width: 0%;
    transition: width 1.4s cubic-bezier(0.25, 1, 0.5, 1);
    position: relative;
  }
  .skill-fill::after {
    content: '';
    position: absolute;
    right: 0; top: 50%;
    transform: translateY(-50%);
    width: 8px; height: 8px;
    border-radius: 50%;
    background: inherit;
    box-shadow: 0 0 10px currentColor;
  }
  .skill-fill.animated { width: var(--target-width); }

  /* ── PROJECTS ── */
  .projects-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(260px, 1fr)); gap: 16px; }
  .project-card {
    background: rgba(0,0,0,0.25);
    border: 1px solid var(--panel-border);
    border-radius: 10px;
    padding: 20px;
    position: relative;
    overflow: hidden;
    transition: all 0.3s ease;
    cursor: default;
  }
  .project-card::before {
    content: '';
    position: absolute;
    top: 0; left: 0; right: 0;
    height: 2px;
    background: var(--card-accent, var(--cyan));
    transform: scaleX(0);
    transform-origin: left;
    transition: transform 0.3s ease;
  }
  .project-card:hover::before { transform: scaleX(1); }
  .project-card:hover {
    border-color: var(--card-accent, var(--cyan));
    box-shadow: 0 0 30px color-mix(in srgb, var(--card-accent, var(--cyan)) 10%, transparent);
    transform: translateY(-4px);
  }
  .project-icon { font-size: 28px; margin-bottom: 12px; }
  .project-name {
    font-family: var(--font-display);
    font-size: 13px;
    font-weight: 700;
    color: #fff;
    letter-spacing: 0.05em;
    margin-bottom: 8px;
  }
  .project-desc {
    font-family: var(--font-body);
    font-size: 13px;
    color: var(--text-dim);
    line-height: 1.6;
    margin-bottom: 14px;
    font-weight: 300;
  }
  .project-stack { display: flex; flex-wrap: wrap; gap: 6px; }
  .stack-tag {
    font-family: var(--font-mono);
    font-size: 10px;
    color: var(--text-dim);
    background: rgba(255,255,255,0.04);
    border: 1px solid rgba(255,255,255,0.08);
    padding: 3px 8px;
    border-radius: 4px;
    letter-spacing: 0.05em;
  }

  /* ── STATS ── */
  .stats-grid { display: grid; grid-template-columns: repeat(3, 1fr); gap: 16px; }
  @media (max-width: 500px) { .stats-grid { grid-template-columns: 1fr 1fr; } }
  .stat-box {
    background: rgba(0,0,0,0.25);
    border: 1px solid var(--panel-border);
    border-radius: 10px;
    padding: 20px 16px;
    text-align: center;
    transition: all 0.2s;
    position: relative;
    overflow: hidden;
  }
  .stat-box::after {
    content: '';
    position: absolute;
    inset: 0;
    background: radial-gradient(circle at 50% 0%, var(--cyan-dim), transparent 70%);
    opacity: 0;
    transition: opacity 0.3s;
  }
  .stat-box:hover { border-color: var(--cyan); box-shadow: 0 0 24px var(--cyan-dim); }
  .stat-box:hover::after { opacity: 1; }
  .stat-number {
    font-family: var(--font-display);
    font-size: 28px;
    font-weight: 900;
    color: var(--cyan);
    display: block;
    line-height: 1;
    text-shadow: 0 0 20px var(--cyan);
  }
  .stat-label {
    font-family: var(--font-mono);
    font-size: 10px;
    color: var(--text-dim);
    letter-spacing: 0.15em;
    text-transform: uppercase;
    margin-top: 6px;
    display: block;
  }

  /* ── CONTACT ── */
  .contact-links { display: flex; flex-wrap: wrap; gap: 12px; justify-content: center; }
  .contact-link {
    display: flex;
    align-items: center;
    gap: 10px;
    background: rgba(0,0,0,0.3);
    border: 1px solid var(--panel-border);
    border-radius: 10px;
    padding: 14px 22px;
    font-family: var(--font-mono);
    font-size: 13px;
    color: var(--text);
    text-decoration: none;
    transition: all 0.25s ease;
    position: relative;
    overflow: hidden;
  }
  .contact-link::after {
    content: '';
    position: absolute;
    inset: 0;
    background: var(--link-color, var(--cyan));
    opacity: 0;
    transition: opacity 0.2s;
  }
  .contact-link:hover {
    border-color: var(--link-color, var(--cyan));
    color: var(--link-color, var(--cyan));
    box-shadow: 0 0 24px color-mix(in srgb, var(--link-color, var(--cyan)) 25%, transparent);
    transform: translateY(-3px);
  }
  .contact-link .link-icon { font-size: 18px; position: relative; z-index: 1; }
  .contact-link span { position: relative; z-index: 1; }

  /* ── FOOTER ── */
  .footer {
    text-align: center;
    margin-top: 64px;
    padding: 32px;
    border-top: 1px solid var(--panel-border);
    font-family: var(--font-mono);
    font-size: 12px;
    color: var(--text-dim);
    letter-spacing: 0.1em;
    animation: fadeIn 1s 1.5s both;
  }
  .footer .highlight { color: var(--cyan); }

  /* ── ANIMATIONS ── */
  @keyframes fadeIn { from { opacity:0 } to { opacity:1 } }
  @keyframes fadeSlideDown { from { opacity:0; transform:translateY(-20px) } to { opacity:1; transform:translateY(0) } }
  @keyframes slideUp { from { opacity:0; transform:translateY(24px) } to { opacity:1; transform:translateY(0) } }

  @keyframes blink { 0%,100%{opacity:1} 50%{opacity:0} }

  @keyframes pulse-green {
    0%,100% { box-shadow: 0 0 8px var(--green); opacity:1 }
    50% { box-shadow: 0 0 20px var(--green); opacity:0.6 }
  }

  @keyframes glitch-flicker {
    0%,94%,96%,98%,100% { text-shadow: 0 0 40px rgba(0,255,209,0.3) }
    95% { text-shadow: -3px 0 var(--red), 3px 0 var(--cyan) }
    97% { text-shadow: 3px 0 var(--red), -3px 0 var(--cyan) }
    99% { text-shadow: 0 0 40px rgba(0,255,209,0.3) }
  }
  @keyframes glitch-before {
    0%,90%,100% { transform:none; opacity:0 }
    92% { transform:translate(-4px,0); opacity:0.7 }
    96% { transform:translate(4px,0); opacity:0.4 }
  }
  @keyframes glitch-after {
    0%,90%,100% { transform:none; opacity:0 }
    93% { transform:translate(4px,0); opacity:0.7 }
    97% { transform:translate(-4px,0); opacity:0.4 }
  }

  /* Stagger delays */
  .panel:nth-child(1) { animation-delay: 0.1s; }
  .panel:nth-child(2) { animation-delay: 0.2s; }
  .panel:nth-child(3) { animation-delay: 0.3s; }
  .panel:nth-child(4) { animation-delay: 0.4s; }
  .panel:nth-child(5) { animation-delay: 0.5s; }
  .panel:nth-child(6) { animation-delay: 0.6s; }
  .divider { animation-delay: 0.05s; }
</style>
</head>
<body>

<canvas id="matrix-bg"></canvas>
<div class="cursor" id="cursor"></div>
<div class="cursor-ring" id="cursor-ring"></div>

<div class="container">

  <!-- HERO -->
  <header class="hero">
    <div class="hero-status">
      <span class="status-dot"></span>
      ONLINE · OPEN TO COLLABORATE
    </div>
    <h1 class="glitch-name" data-text="ZAIDAN FAARIS">ZAIDAN FAARIS</h1>
    <p class="hero-subtitle">ABIDI &nbsp;·&nbsp; SOFTWARE ENGINEERING STUDENT &nbsp;·&nbsp; INDONESIA 🇮🇩</p>
    <div class="typing-line">
      <span style="color:var(--text-dim)">$&nbsp;</span>
      <span class="typing-text" id="typing-el"></span>
      <span class="blink-cursor"></span>
    </div>
    <div class="hero-badges">
      <span class="badge">🌐 Web Developer</span>
      <span class="badge">⚙️ Backend Enthusiast</span>
      <span class="badge">🖥️ Desktop Apps</span>
      <span class="badge">📚 Always Learning</span>
    </div>
  </header>

  <!-- WHOAMI -->
  <div class="divider" style="animation-delay:0.1s">
    <div class="divider-line"></div>
    <div class="divider-label"><span>01</span> · WHOAMI</div>
    <div class="divider-line"></div>
  </div>

  <div class="panel" data-delay="0">
    <div class="panel-header">
      <span class="panel-dot dot-red"></span>
      <span class="panel-dot dot-yellow"></span>
      <span class="panel-dot dot-green"></span>
      <span class="panel-title">profile.yaml</span>
    </div>
    <div class="panel-body">
      <div class="whoami-grid">
        <div class="info-row"><span class="info-key">name:</span><span class="info-val">Zaidan Faaris Abidi</span></div>
        <div class="info-row"><span class="info-key">location:</span><span class="info-val">🇮🇩 Indonesia</span></div>
        <div class="info-row"><span class="info-key">status:</span><span class="info-val">Software Engineering Student</span></div>
        <div class="info-row"><span class="info-key">focus:</span><span class="info-val">Web Dev & Backend Systems</span></div>
        <div class="info-row" style="grid-column:1/-1"><span class="info-key">building:</span><span class="info-val">Web Apps · Desktop Apps · Real-world systems</span></div>
        <div class="info-row" style="grid-column:1/-1"><span class="info-key">currently:</span><span class="info-val">C# · JavaScript · PHP · Dart</span></div>
        <div class="info-row" style="grid-column:1/-1"><span class="info-key">fun_fact:</span><span class="info-val">I debug with determination and coffee ☕</span></div>
      </div>
    </div>
  </div>

  <!-- TECH STACK -->
  <div class="divider" style="animation-delay:0.15s">
    <div class="divider-line"></div>
    <div class="divider-label"><span>02</span> · TECH STACK</div>
    <div class="divider-line"></div>
  </div>

  <div class="panel" data-delay="100">
    <div class="panel-header">
      <span class="panel-dot dot-red"></span>
      <span class="panel-dot dot-yellow"></span>
      <span class="panel-dot dot-green"></span>
      <span class="panel-title">tech-stack.json</span>
    </div>
    <div class="panel-body">
      <div class="tech-section">
        <div class="tech-section-title"><span>//</span> Languages</div>
        <div class="tech-pills">
          <div class="tech-pill" style="--pill-color:#777BB4"><span class="pill-icon">🐘</span> PHP</div>
          <div class="tech-pill" style="--pill-color:#239120"><span class="pill-icon">🎯</span> C#</div>
          <div class="tech-pill" style="--pill-color:#F7DF1E"><span class="pill-icon">⚡</span> JavaScript</div>
          <div class="tech-pill" style="--pill-color:#0175C2"><span class="pill-icon">🎪</span> Dart</div>
        </div>
      </div>
      <div class="tech-section">
        <div class="tech-section-title"><span>//</span> Web & UI</div>
        <div class="tech-pills">
          <div class="tech-pill" style="--pill-color:#E34F26"><span class="pill-icon">🔖</span> HTML5</div>
          <div class="tech-pill" style="--pill-color:#1572B6"><span class="pill-icon">🎨</span> CSS3</div>
          <div class="tech-pill" style="--pill-color:#7952B3"><span class="pill-icon">🅱️</span> Bootstrap</div>
        </div>
      </div>
      <div class="tech-section" style="margin-bottom:0">
        <div class="tech-section-title"><span>//</span> Database & Tools</div>
        <div class="tech-pills">
          <div class="tech-pill" style="--pill-color:#4479A1"><span class="pill-icon">🗃️</span> MySQL</div>
          <div class="tech-pill" style="--pill-color:#F05032"><span class="pill-icon">🌿</span> Git</div>
          <div class="tech-pill" style="--pill-color:#007ACC"><span class="pill-icon">💻</span> VS Code</div>
          <div class="tech-pill" style="--pill-color:#FCC624"><span class="pill-icon">🐧</span> Linux</div>
        </div>
      </div>
    </div>
  </div>

  <!-- SKILL BARS -->
  <div class="divider" style="animation-delay:0.2s">
    <div class="divider-line"></div>
    <div class="divider-label"><span>03</span> · SKILL LEVEL</div>
    <div class="divider-line"></div>
  </div>

  <div class="panel" data-delay="200" id="skills-panel">
    <div class="panel-header">
      <span class="panel-dot dot-red"></span>
      <span class="panel-dot dot-yellow"></span>
      <span class="panel-dot dot-green"></span>
      <span class="panel-title">skills.log</span>
    </div>
    <div class="panel-body">
      <div class="skill-item">
        <div class="skill-header"><span class="skill-name">🐘 PHP & MySQL</span><span class="skill-pct">80%</span></div>
        <div class="skill-track"><div class="skill-fill" style="--target-width:80%;background:linear-gradient(90deg,#4a2d8a,#777BB4)" data-width="80%"></div></div>
      </div>
      <div class="skill-item">
        <div class="skill-header"><span class="skill-name">⚡ JavaScript</span><span class="skill-pct">72%</span></div>
        <div class="skill-track"><div class="skill-fill" style="--target-width:72%;background:linear-gradient(90deg,#7a6a00,#F7DF1E)" data-width="72%"></div></div>
      </div>
      <div class="skill-item">
        <div class="skill-header"><span class="skill-name">🎯 C# & .NET</span><span class="skill-pct">65%</span></div>
        <div class="skill-track"><div class="skill-fill" style="--target-width:65%;background:linear-gradient(90deg,#0d4d0d,#39FF14)" data-width="65%"></div></div>
      </div>
      <div class="skill-item">
        <div class="skill-header"><span class="skill-name">🔖 HTML5 / CSS3</span><span class="skill-pct">85%</span></div>
        <div class="skill-track"><div class="skill-fill" style="--target-width:85%;background:linear-gradient(90deg,#7a1b0d,#E34F26)" data-width="85%"></div></div>
      </div>
      <div class="skill-item" style="margin-bottom:0">
        <div class="skill-header"><span class="skill-name">🎪 Dart / Flutter</span><span class="skill-pct">40%</span></div>
        <div class="skill-track"><div class="skill-fill" style="--target-width:40%;background:linear-gradient(90deg,#003a6e,#0175C2)" data-width="40%"></div></div>
      </div>
    </div>
  </div>

  <!-- PROJECTS -->
  <div class="divider" style="animation-delay:0.25s">
    <div class="divider-line"></div>
    <div class="divider-label"><span>04</span> · PROJECTS</div>
    <div class="divider-line"></div>
  </div>

  <div class="panel" data-delay="300">
    <div class="panel-header">
      <span class="panel-dot dot-red"></span>
      <span class="panel-dot dot-yellow"></span>
      <span class="panel-dot dot-green"></span>
      <span class="panel-title">git log --oneline --projects</span>
    </div>
    <div class="panel-body">
      <div class="projects-grid">
        <div class="project-card" style="--card-accent:#00FFD1">
          <div class="project-icon">🚆</div>
          <div class="project-name">KAI ACCESS CLONE</div>
          <div class="project-desc">Train ticket booking system — search routes, book seats, and manage trips. Full KAI-style experience.</div>
          <div class="project-stack">
            <span class="stack-tag">PHP</span>
            <span class="stack-tag">MySQL</span>
            <span class="stack-tag">Bootstrap</span>
          </div>
        </div>
        <div class="project-card" style="--card-accent:#39FF14">
          <div class="project-icon">📍</div>
          <div class="project-name">GPS TRACKER DASHBOARD</div>
          <div class="project-desc">Real-time location tracking with live map visualization. Track assets on the fly with dynamic UI.</div>
          <div class="project-stack">
            <span class="stack-tag">JavaScript</span>
            <span class="stack-tag">Leaflet.js</span>
            <span class="stack-tag">CSS3</span>
          </div>
        </div>
        <div class="project-card" style="--card-accent:#FF6B35">
          <div class="project-icon">🧾</div>
          <div class="project-name">RFID ATTENDANCE SYSTEM</div>
          <div class="project-desc">Automated attendance logging via RFID hardware integration. Fast, reliable, and paperless.</div>
          <div class="project-stack">
            <span class="stack-tag">C#</span>
            <span class="stack-tag">MySQL</span>
            <span class="stack-tag">.NET</span>
          </div>
        </div>
      </div>
    </div>
  </div>

  <!-- STATS -->
  <div class="divider" style="animation-delay:0.3s">
    <div class="divider-line"></div>
    <div class="divider-label"><span>05</span> · GITHUB STATS</div>
    <div class="divider-line"></div>
  </div>

  <div class="panel" data-delay="400">
    <div class="panel-header">
      <span class="panel-dot dot-red"></span>
      <span class="panel-dot dot-yellow"></span>
      <span class="panel-dot dot-green"></span>
      <span class="panel-title">github --stats Koalaxl</span>
    </div>
    <div class="panel-body">
      <div class="stats-grid" style="margin-bottom:24px">
        <div class="stat-box"><span class="stat-number" data-count="3">0</span><span class="stat-label">Projects</span></div>
        <div class="stat-box"><span class="stat-number" data-count="4">0</span><span class="stat-label">Languages</span></div>
        <div class="stat-box"><span class="stat-number" data-count="2025">0</span><span class="stat-label">Since Year</span></div>
      </div>
      <div style="text-align:center;margin-bottom:20px">
        <img src="https://github-readme-stats.vercel.app/api?username=Koalaxl&show_icons=true&theme=tokyonight&hide_border=true&bg_color=050f1a&title_color=00FFD1&icon_color=00FFD1&text_color=c9d1d9&ring_color=00FFD1" style="border-radius:10px;max-width:100%;margin-bottom:12px;display:block;margin:0 auto 12px" alt="GitHub Stats"/>
      </div>
      <div style="text-align:center">
        <img src="https://streak-stats.demolab.com/?user=Koalaxl&theme=tokyonight&hide_border=true&background=050f1a&stroke=00FFD1&ring=00FFD1&fire=FF6B6B&currStreakLabel=00FFD1" style="border-radius:10px;max-width:100%;display:block;margin:0 auto" alt="Streak Stats"/>
      </div>
    </div>
  </div>

  <!-- CONTACT -->
  <div class="divider" style="animation-delay:0.35s">
    <div class="divider-line"></div>
    <div class="divider-label"><span>06</span> · CONNECT</div>
    <div class="divider-line"></div>
  </div>

  <div class="panel" data-delay="500">
    <div class="panel-header">
      <span class="panel-dot dot-red"></span>
      <span class="panel-dot dot-yellow"></span>
      <span class="panel-dot dot-green"></span>
      <span class="panel-title">contact --social</span>
    </div>
    <div class="panel-body" style="text-align:center">
      <p style="font-family:var(--font-mono);font-size:13px;color:var(--text-dim);margin-bottom:24px;letter-spacing:0.05em">
        // always open for collaborations, ideas, and cool projects<br/>
        // if you have something interesting — <span style="color:var(--cyan)">let's build it 🔧</span>
      </p>
      <div class="contact-links">
        <a href="https://github.com/Koalaxl" target="_blank" class="contact-link" style="--link-color:#ffffff">
          <span class="link-icon">🐙</span>
          <span>github.com/Koalaxl</span>
        </a>
      </div>
    </div>
  </div>

  <footer class="footer">
    <span class="highlight">⭐</span> &nbsp;Thanks for visiting!&nbsp; <span class="highlight">·</span> &nbsp;Built with <span class="highlight">passion</span> in 🇮🇩&nbsp; <span class="highlight">·</span> &nbsp;Drop a star if you like what you see
  </footer>

</div>

<script>
// ── CURSOR ──
const cursor = document.getElementById('cursor');
const ring = document.getElementById('cursor-ring');
let mx=0, my=0, rx=0, ry=0;
document.addEventListener('mousemove', e => {
  mx = e.clientX; my = e.clientY;
  cursor.style.left = mx - 6 + 'px';
  cursor.style.top  = my - 6 + 'px';
});
(function animRing(){
  rx += (mx - rx - 18) * 0.15;
  ry += (my - ry - 18) * 0.15;
  ring.style.left = rx + 'px';
  ring.style.top  = ry + 'px';
  requestAnimationFrame(animRing);
})();
document.querySelectorAll('a,button,.tech-pill,.project-card,.stat-box,.contact-link').forEach(el => {
  el.addEventListener('mouseenter', () => { cursor.style.transform='scale(1.8)'; ring.style.transform='translate(-50%,-50%) scale(1.4)'; });
  el.addEventListener('mouseleave', () => { cursor.style.transform='scale(1)'; ring.style.transform='translate(-50%,-50%) scale(1)'; });
});

// ── MATRIX RAIN ──
const canvas = document.getElementById('matrix-bg');
const ctx = canvas.getContext('2d');
function resizeCanvas(){ canvas.width=window.innerWidth; canvas.height=window.innerHeight; }
resizeCanvas(); window.addEventListener('resize', resizeCanvas);
const chars = 'ZAIDAN01ｦｧｨｩｪｫｬｭｮｯｰABCDEF0123456789アイウエオカキクケコ';
const fontSize = 14;
let cols;
let drops = [];
function initDrops(){
  cols = Math.floor(canvas.width / fontSize);
  drops = Array(cols).fill(1);
}
initDrops(); window.addEventListener('resize', initDrops);
function drawMatrix(){
  ctx.fillStyle = 'rgba(2,8,16,0.05)';
  ctx.fillRect(0,0,canvas.width,canvas.height);
  ctx.font = fontSize + 'px Share Tech Mono';
  drops.forEach((y,i) => {
    const ch = chars[Math.floor(Math.random()*chars.length)];
    const progress = y / (canvas.height / fontSize);
    ctx.fillStyle = progress > 0.9 ? '#ffffff' : progress > 0.7 ? '#00FFD1' : '#004a3a';
    ctx.fillText(ch, i*fontSize, y*fontSize);
    if(y*fontSize > canvas.height && Math.random() > 0.975) drops[i] = 0;
    drops[i]++;
  });
}
setInterval(drawMatrix, 50);

// ── TYPING EFFECT ──
const phrases = [
  'building real-world solutions...',
  'exploring backend architectures...',
  'crafting web experiences...',
  'learning something new every day...',
  'open to collaborate → ping me!'
];
let pi=0, ci=0, deleting=false;
const typEl = document.getElementById('typing-el');
function type(){
  const phrase = phrases[pi];
  if(!deleting){
    typEl.textContent = phrase.slice(0, ++ci);
    if(ci === phrase.length){ deleting=true; setTimeout(type, 1800); return; }
  } else {
    typEl.textContent = phrase.slice(0, --ci);
    if(ci === 0){ deleting=false; pi=(pi+1)%phrases.length; }
  }
  setTimeout(type, deleting ? 40 : 60);
}
type();

// ── INTERSECTION OBSERVER for panels ──
const observer = new IntersectionObserver(entries => {
  entries.forEach(entry => {
    if(entry.isIntersecting){
      const delay = parseInt(entry.target.dataset.delay || 0);
      setTimeout(() => entry.target.classList.add('visible'), delay);
      observer.unobserve(entry.target);
    }
  });
}, { threshold: 0.1 });
document.querySelectorAll('.panel').forEach(p => observer.observe(p));

// ── SKILL BAR ANIMATION ──
const skillObserver = new IntersectionObserver(entries => {
  entries.forEach(entry => {
    if(entry.isIntersecting){
      entry.target.querySelectorAll('.skill-fill').forEach((bar, i) => {
        setTimeout(() => bar.classList.add('animated'), i * 150);
      });
      skillObserver.unobserve(entry.target);
    }
  });
}, { threshold: 0.3 });
const skillsPanel = document.getElementById('skills-panel');
if(skillsPanel) skillObserver.observe(skillsPanel);

// ── COUNT UP ANIMATION ──
function countUp(el, target, duration=1200){
  const start = performance.now();
  const update = now => {
    const progress = Math.min((now-start)/duration, 1);
    const ease = 1 - Math.pow(1-progress, 3);
    el.textContent = Math.floor(ease * target);
    if(progress < 1) requestAnimationFrame(update);
    else el.textContent = target;
  };
  requestAnimationFrame(update);
}
const countObserver = new IntersectionObserver(entries => {
  entries.forEach(entry => {
    if(entry.isIntersecting){
      entry.target.querySelectorAll('[data-count]').forEach(el => {
        countUp(el, parseInt(el.dataset.count));
      });
      countObserver.unobserve(entry.target);
    }
  });
}, { threshold: 0.4 });
document.querySelectorAll('.panel').forEach(p => countObserver.observe(p));

// ── DIVIDER REVEAL ──
const dividerObserver = new IntersectionObserver(entries => {
  entries.forEach(e => { if(e.isIntersecting){ e.target.style.opacity=1; dividerObserver.unobserve(e.target); }});
}, { threshold: 0.5 });
document.querySelectorAll('.divider').forEach(d => dividerObserver.observe(d));
</script>
</body>
</html>
