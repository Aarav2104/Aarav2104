<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8"/>
<meta name="viewport" content="width=device-width,initial-scale=1"/>
<title>David — GitHub Profile README</title>
<link href="https://fonts.googleapis.com/css2?family=Share+Tech+Mono&family=Orbitron:wght@400;700;900&family=Exo+2:wght@300;400;600;800&display=swap" rel="stylesheet"/>
<style>
  :root {
    --neon-pink: #ff2d78;
    --neon-purple: #a855f7;
    --neon-cyan: #00f5ff;
    --neon-gold: #fbbf24;
    --bg-dark: #050b18;
    --bg-card: rgba(10,20,40,0.85);
    --grid-line: rgba(0,245,255,0.05);
    --font-hud: 'Share Tech Mono', monospace;
    --font-title: 'Orbitron', sans-serif;
    --font-body: 'Exo 2', sans-serif;
  }

  *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

  body {
    background: var(--bg-dark);
    color: #e2e8f0;
    font-family: var(--font-body);
    min-height: 100vh;
    overflow-x: hidden;
  }

  /* ──────────── PARTICLE CANVAS ──────────── */
  #particle-canvas {
    position: fixed; inset: 0; z-index: 0; pointer-events: none;
  }

  /* ──────────── GRID OVERLAY ──────────── */
  .grid-overlay {
    position: fixed; inset: 0; z-index: 0; pointer-events: none;
    background-image:
      linear-gradient(var(--grid-line) 1px, transparent 1px),
      linear-gradient(90deg, var(--grid-line) 1px, transparent 1px);
    background-size: 60px 60px;
    animation: gridShift 20s linear infinite;
  }
  @keyframes gridShift {
    from { background-position: 0 0; }
    to   { background-position: 60px 60px; }
  }

  /* ──────────── SCANLINE ──────────── */
  .scanline {
    position: fixed; inset: 0; z-index: 1; pointer-events: none;
    background: repeating-linear-gradient(
      to bottom,
      transparent 0px,
      transparent 3px,
      rgba(0,0,0,0.07) 3px,
      rgba(0,0,0,0.07) 4px
    );
  }

  /* ──────────── LAYOUT ──────────── */
  .wrapper {
    position: relative; z-index: 2;
    max-width: 900px; margin: 0 auto;
    padding: 40px 20px 80px;
  }

  /* ──────────── HERO ──────────── */
  .hero {
    text-align: center;
    padding: 60px 20px 40px;
    position: relative;
  }

  .hero-ring {
    position: relative;
    display: inline-block;
    margin-bottom: 24px;
  }

  .hero-ring svg {
    animation: spinRing 8s linear infinite;
  }
  @keyframes spinRing {
    from { transform: rotate(0deg); }
    to   { transform: rotate(360deg); }
  }

  .hero-avatar {
    position: absolute;
    top: 50%; left: 50%;
    transform: translate(-50%, -50%);
    width: 90px; height: 90px;
    border-radius: 50%;
    background: linear-gradient(135deg, #1a0533, #0d1b3e);
    border: 2px solid var(--neon-pink);
    display: flex; align-items: center; justify-content: center;
    font-family: var(--font-title);
    font-size: 32px; font-weight: 900;
    color: var(--neon-pink);
    text-shadow: 0 0 20px var(--neon-pink);
    box-shadow: 0 0 30px rgba(255,45,120,0.4), inset 0 0 20px rgba(255,45,120,0.1);
  }

  .hero-name {
    font-family: var(--font-title);
    font-size: clamp(2.5rem, 7vw, 5rem);
    font-weight: 900;
    letter-spacing: 0.15em;
    background: linear-gradient(90deg, var(--neon-pink) 0%, var(--neon-purple) 50%, var(--neon-cyan) 100%);
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
    background-clip: text;
    animation: gradientShift 4s ease-in-out infinite alternate;
    filter: drop-shadow(0 0 30px rgba(255,45,120,0.5));
  }
  @keyframes gradientShift {
    from { filter: drop-shadow(0 0 20px rgba(255,45,120,0.5)); }
    to   { filter: drop-shadow(0 0 40px rgba(0,245,255,0.5)); }
  }

  .hero-tagline {
    font-family: var(--font-hud);
    font-size: 0.85rem;
    color: var(--neon-cyan);
    letter-spacing: 0.3em;
    margin-top: 8px;
    opacity: 0;
    animation: fadeUp 0.8s 0.8s forwards;
  }

  /* ──────────── TYPING TERMINAL ──────────── */
  .terminal {
    background: rgba(0,0,0,0.7);
    border: 1px solid rgba(0,245,255,0.2);
    border-radius: 12px;
    padding: 20px 24px;
    margin: 32px 0;
    font-family: var(--font-hud);
    font-size: 0.88rem;
    position: relative;
    overflow: hidden;
  }
  .terminal::before {
    content: '';
    position: absolute; top: 0; left: 0; right: 0;
    height: 1px;
    background: linear-gradient(90deg, transparent, var(--neon-cyan), transparent);
    animation: scanBeam 3s ease-in-out infinite;
  }
  @keyframes scanBeam {
    0%   { transform: translateY(0); opacity: 1; }
    100% { transform: translateY(200px); opacity: 0; }
  }
  .terminal-bar {
    display: flex; gap: 8px; margin-bottom: 16px;
  }
  .dot { width: 12px; height: 12px; border-radius: 50%; }
  .dot-red { background: #ff5f57; }
  .dot-yellow { background: #febc2e; }
  .dot-green { background: #28c840; }
  .terminal-line {
    color: #94a3b8;
    margin: 4px 0;
    opacity: 0;
  }
  .terminal-line span.cmd { color: var(--neon-cyan); }
  .terminal-line span.val { color: var(--neon-pink); }
  .terminal-line span.ok  { color: #34d399; }
  .cursor {
    display: inline-block; width: 8px; height: 14px;
    background: var(--neon-cyan);
    animation: blink 1s infinite;
    vertical-align: middle;
    margin-left: 2px;
  }
  @keyframes blink { 0%,49%{opacity:1} 50%,100%{opacity:0} }

  /* ──────────── SECTION HEADING ──────────── */
  .section-heading {
    font-family: var(--font-title);
    font-size: 0.7rem;
    letter-spacing: 0.4em;
    color: var(--neon-cyan);
    text-transform: uppercase;
    margin: 48px 0 20px;
    display: flex; align-items: center; gap: 16px;
  }
  .section-heading::before, .section-heading::after {
    content: '';
    flex: 1; height: 1px;
    background: linear-gradient(90deg, transparent, rgba(0,245,255,0.3));
  }
  .section-heading::before { background: linear-gradient(90deg, rgba(0,245,255,0.3), transparent); }

  /* ──────────── STATS GRID ──────────── */
  .stats-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(180px, 1fr));
    gap: 16px;
  }

  .stat-card {
    background: var(--bg-card);
    border: 1px solid rgba(255,45,120,0.2);
    border-radius: 12px;
    padding: 24px 20px;
    position: relative;
    overflow: hidden;
    cursor: default;
    transition: border-color 0.3s, transform 0.3s;
    opacity: 0;
    transform: translateY(30px);
  }
  .stat-card::before {
    content: '';
    position: absolute; inset: 0;
    background: radial-gradient(circle at 30% 30%, rgba(255,45,120,0.07), transparent 60%);
    opacity: 0; transition: opacity 0.4s;
  }
  .stat-card:hover { border-color: var(--neon-pink); transform: translateY(-4px); }
  .stat-card:hover::before { opacity: 1; }

  .stat-card .icon {
    font-size: 1.4rem; margin-bottom: 10px;
    display: block;
  }
  .stat-card .value {
    font-family: var(--font-title);
    font-size: 2rem; font-weight: 700;
    color: var(--neon-pink);
    text-shadow: 0 0 20px rgba(255,45,120,0.6);
    display: block;
  }
  .stat-card .label {
    font-family: var(--font-hud);
    font-size: 0.72rem;
    color: #64748b;
    letter-spacing: 0.15em;
    text-transform: uppercase;
    margin-top: 4px;
    display: block;
  }
  .stat-corner {
    position: absolute; top: 10px; right: 10px;
    width: 20px; height: 20px;
    border-top: 2px solid rgba(0,245,255,0.3);
    border-right: 2px solid rgba(0,245,255,0.3);
    border-radius: 0 4px 0 0;
  }

  /* ──────────── STREAK ROW ──────────── */
  .streak-row {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    gap: 16px;
    margin-top: 0;
  }

  .streak-card {
    background: var(--bg-card);
    border: 1px solid rgba(168,85,247,0.25);
    border-radius: 12px;
    padding: 28px 20px;
    text-align: center;
    position: relative; overflow: hidden;
    opacity: 0; transform: scale(0.9);
    transition: border-color 0.3s, transform 0.3s;
  }
  .streak-card:hover { border-color: var(--neon-purple); transform: scale(1.02); }

  .streak-card .big {
    font-family: var(--font-title);
    font-size: 3rem; font-weight: 900;
    color: var(--neon-pink);
    text-shadow: 0 0 30px rgba(255,45,120,0.7);
    display: block;
  }
  .streak-card.fire .big { color: var(--neon-gold); text-shadow: 0 0 30px rgba(251,191,36,0.8); }
  .streak-card .sub {
    font-family: var(--font-hud);
    font-size: 0.65rem; letter-spacing: 0.2em;
    color: #64748b; text-transform: uppercase;
    margin-top: 4px; display: block;
  }
  .streak-card .sub-date {
    font-family: var(--font-hud);
    font-size: 0.65rem; color: #475569;
    margin-top: 6px; display: block;
  }

  .fire-ring {
    display: inline-block;
    position: relative;
  }
  .fire-ring::before {
    content: '🔥';
    position: absolute; top: -28px; left: 50%;
    transform: translateX(-50%);
    font-size: 1.4rem;
    animation: fireFloat 1.5s ease-in-out infinite alternate;
  }
  @keyframes fireFloat {
    from { transform: translateX(-50%) translateY(0) scale(1); }
    to   { transform: translateX(-50%) translateY(-6px) scale(1.15); }
  }

  /* ──────────── LANGUAGE BAR ──────────── */
  .lang-section {
    background: var(--bg-card);
    border: 1px solid rgba(0,245,255,0.15);
    border-radius: 12px;
    padding: 28px;
    opacity: 0;
  }

  .lang-spectrum {
    display: flex; height: 10px; border-radius: 99px; overflow: hidden;
    margin-bottom: 28px; gap: 2px;
  }
  .lang-seg {
    height: 100%; border-radius: 99px;
    transform: scaleX(0); transform-origin: left;
    transition: transform 1.2s cubic-bezier(.16,1,.3,1);
  }

  .lang-grid {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 14px 32px;
  }

  .lang-row {
    display: flex; align-items: center; gap: 10px;
  }
  .lang-dot {
    width: 10px; height: 10px; border-radius: 50%; flex-shrink: 0;
  }
  .lang-name {
    font-family: var(--font-hud);
    font-size: 0.78rem; color: #94a3b8; flex: 1;
  }
  .lang-pct {
    font-family: var(--font-title);
    font-size: 0.75rem; font-weight: 700;
    color: #e2e8f0;
  }
  .lang-bar-wrap {
    flex: 2; height: 4px; background: rgba(255,255,255,0.05); border-radius: 99px; overflow: hidden;
  }
  .lang-bar-fill {
    height: 100%; border-radius: 99px;
    transform: scaleX(0); transform-origin: left;
    transition: transform 1.4s cubic-bezier(.16,1,.3,1);
  }

  /* ──────────── BADGES ──────────── */
  .badge-row {
    display: flex; flex-wrap: wrap; gap: 10px; justify-content: center;
    margin-top: 16px;
  }
  .badge {
    font-family: var(--font-hud);
    font-size: 0.72rem;
    padding: 6px 14px;
    border-radius: 99px;
    border: 1px solid;
    letter-spacing: 0.1em;
    text-transform: uppercase;
    opacity: 0;
    transform: translateY(10px);
    transition: transform 0.25s, box-shadow 0.25s;
    cursor: default;
  }
  .badge:hover {
    transform: translateY(-2px);
    box-shadow: 0 0 18px currentColor;
  }
  .badge-pink   { color: var(--neon-pink);   border-color: rgba(255,45,120,0.4);   background: rgba(255,45,120,0.07); }
  .badge-cyan   { color: var(--neon-cyan);   border-color: rgba(0,245,255,0.4);    background: rgba(0,245,255,0.07); }
  .badge-purple { color: var(--neon-purple); border-color: rgba(168,85,247,0.4);   background: rgba(168,85,247,0.07); }
  .badge-gold   { color: var(--neon-gold);   border-color: rgba(251,191,36,0.4);   background: rgba(251,191,36,0.07); }

  /* ──────────── ACTIVITY PULSE ──────────── */
  .activity-line {
    height: 60px; display: flex; align-items: flex-end; gap: 4px;
    padding: 0 4px;
  }
  .act-bar {
    flex: 1; background: rgba(255,45,120,0.15);
    border-radius: 3px 3px 0 0;
    border-top: 1px solid rgba(255,45,120,0.4);
    transition: background 0.3s;
    position: relative;
    transform: scaleY(0); transform-origin: bottom;
    animation: barGrow 0.5s ease forwards;
  }
  .act-bar:hover { background: rgba(255,45,120,0.5); cursor: default; }

  /* ──────────── FOOTER ──────────── */
  .footer {
    text-align: center; margin-top: 60px;
    font-family: var(--font-hud); font-size: 0.7rem;
    color: #334155; letter-spacing: 0.2em;
    opacity: 0; animation: fadeUp 0.8s 3s forwards;
  }
  .footer span { color: var(--neon-pink); }

  /* ──────────── HELPERS ──────────── */
  @keyframes fadeUp {
    from { opacity:0; transform: translateY(20px); }
    to   { opacity:1; transform: translateY(0); }
  }
  @keyframes fadeIn {
    from { opacity:0; }
    to   { opacity:1; }
  }

  .glow-line {
    height: 1px;
    background: linear-gradient(90deg, transparent, var(--neon-pink), var(--neon-purple), var(--neon-cyan), transparent);
    margin: 32px 0;
    animation: linePulse 3s ease-in-out infinite;
  }
  @keyframes linePulse {
    0%,100% { opacity: 0.4; }
    50%      { opacity: 1; }
  }

  /* Responsive */
  @media (max-width: 600px) {
    .streak-row { grid-template-columns: 1fr; }
    .lang-grid  { grid-template-columns: 1fr; }
    .stats-grid { grid-template-columns: repeat(2,1fr); }
  }
</style>
</head>
<body>

<canvas id="particle-canvas"></canvas>
<div class="grid-overlay"></div>
<div class="scanline"></div>

<div class="wrapper">

  <!-- ═══ HERO ═══ -->
  <div class="hero">
    <div class="hero-ring">
      <svg width="130" height="130" viewBox="0 0 130 130">
        <circle cx="65" cy="65" r="58" fill="none" stroke="rgba(255,45,120,0.15)" stroke-width="1"/>
        <circle cx="65" cy="65" r="58" fill="none" stroke="url(#ringGrad)" stroke-width="2"
                stroke-dasharray="80 280" stroke-linecap="round"/>
        <circle cx="65" cy="65" r="46" fill="none" stroke="rgba(0,245,255,0.1)" stroke-width="1"/>
        <circle cx="65" cy="65" r="46" fill="none" stroke="rgba(0,245,255,0.5)" stroke-width="1.5"
                stroke-dasharray="30 260" stroke-linecap="round"/>
        <defs>
          <linearGradient id="ringGrad" x1="0%" y1="0%" x2="100%" y2="0%">
            <stop offset="0%" stop-color="#ff2d78"/>
            <stop offset="100%" stop-color="#a855f7"/>
          </linearGradient>
        </defs>
      </svg>
      <div class="hero-avatar">D</div>
    </div>

    <div class="hero-name">DAVID</div>
    <div class="hero-tagline">◈ &nbsp; SOFTWARE ENGINEER &nbsp;·&nbsp; OPEN SOURCE &nbsp;·&nbsp; SYSTEMS ARCHITECT &nbsp; ◈</div>
  </div>

  <!-- ═══ TERMINAL ═══ -->
  <div class="terminal" id="terminal">
    <div class="terminal-bar">
      <div class="dot dot-red"></div>
      <div class="dot dot-yellow"></div>
      <div class="dot dot-green"></div>
    </div>
    <div class="terminal-line" id="t1"><span class="cmd">$</span> <span class="val">whoami</span></div>
    <div class="terminal-line" id="t2">&nbsp;&nbsp;→ David · Software Engineer · Systems Thinker · OSS Contributor</div>
    <div class="terminal-line" id="t3"><span class="cmd">$</span> <span class="val">git log --all --oneline | wc -l</span></div>
    <div class="terminal-line" id="t4">&nbsp;&nbsp;→ <span class="ok">21,600</span> commits across all time</div>
    <div class="terminal-line" id="t5"><span class="cmd">$</span> <span class="val">./status.sh</span></div>
    <div class="terminal-line" id="t6">&nbsp;&nbsp;→ <span class="ok">▶ ONLINE</span> &nbsp;|&nbsp; Streak: <span class="val">7 days</span> &nbsp;|&nbsp; Peak: <span class="val">53 days</span> &nbsp;|&nbsp; Stars: <span class="val">501 ⭐</span></div>
    <div class="terminal-line" id="t7"><span class="cmd">$</span> <span class="cursor"></span></div>
  </div>

  <div class="glow-line"></div>

  <!-- ═══ GITHUB STATS ═══ -->
  <div class="section-heading">◈ &nbsp; Mission Stats &nbsp; ◈</div>

  <div class="stats-grid" id="stats-grid">
    <div class="stat-card" data-delay="0">
      <div class="stat-corner"></div>
      <span class="icon">⭐</span>
      <span class="value" data-count="501">0</span>
      <span class="label">Total Stars Earned</span>
    </div>
    <div class="stat-card" data-delay="100">
      <div class="stat-corner"></div>
      <span class="icon">📦</span>
      <span class="value">21.6k</span>
      <span class="label">Total Commits</span>
    </div>
    <div class="stat-card" data-delay="200">
      <div class="stat-corner"></div>
      <span class="icon">🔀</span>
      <span class="value">1.2k</span>
      <span class="label">Pull Requests</span>
    </div>
    <div class="stat-card" data-delay="300">
      <div class="stat-corner"></div>
      <span class="icon">💬</span>
      <span class="value" data-count="35">0</span>
      <span class="label">Discussions Answered</span>
    </div>
    <div class="stat-card" data-delay="400" style="grid-column: 1 / -1; max-width: 380px; margin: 0 auto; width: 100%;">
      <div class="stat-corner"></div>
      <span class="icon">🚀</span>
      <span class="value" data-count="6284">0</span>
      <span class="label">Total Contributions · Jan 1 2024 – Present</span>
    </div>
  </div>

  <div class="glow-line"></div>

  <!-- ═══ STREAK ═══ -->
  <div class="section-heading">◈ &nbsp; Streak Intelligence &nbsp; ◈</div>

  <div class="streak-row" id="streak-row">
    <div class="streak-card">
      <span class="big" data-count="6284">6,284</span>
      <span class="sub">Total Contributions</span>
      <span class="sub-date">Jan 1, 2024 — Present</span>
    </div>
    <div class="streak-card fire">
      <div class="fire-ring">
        <span class="big">7</span>
      </div>
      <span class="sub" style="color: var(--neon-gold); margin-top: 12px;">Current Streak 🔥</span>
      <span class="sub-date">Apr 1 — Apr 7, 2026</span>
    </div>
    <div class="streak-card">
      <span class="big">53</span>
      <span class="sub">Longest Streak</span>
      <span class="sub-date">Jun 6 — Jul 28, 2025</span>
    </div>
  </div>

  <div class="glow-line"></div>

  <!-- ═══ ACTIVITY GRAPH ═══ -->
  <div class="section-heading">◈ &nbsp; Activity Pulse &nbsp; ◈</div>
  <div class="lang-section" id="activity-section" style="padding: 20px 24px;">
    <div class="activity-line" id="activity-line"></div>
    <div style="font-family: var(--font-hud); font-size: 0.65rem; color: #334155; text-align: right; margin-top: 8px; letter-spacing: 0.15em;">
      WEEKLY CONTRIBUTION RHYTHM · 2024–PRESENT
    </div>
  </div>

  <div class="glow-line"></div>

  <!-- ═══ LANGUAGES ═══ -->
  <div class="section-heading">◈ &nbsp; Language Arsenal &nbsp; ◈</div>

  <div class="lang-section" id="lang-section">
    <div class="lang-spectrum" id="lang-spectrum">
      <div class="lang-seg" style="width:24.94%; background:#3572A5;" data-w="24.94"></div>
      <div class="lang-seg" style="width:23.89%; background:#f34b7d;" data-w="23.89"></div>
      <div class="lang-seg" style="width:20.94%; background:#00ADD8;" data-w="20.94"></div>
      <div class="lang-seg" style="width:10.92%; background:#555555;" data-w="10.92"></div>
      <div class="lang-seg" style="width:9.65%;  background:#f1e05a;" data-w="9.65"></div>
      <div class="lang-seg" style="width:6.47%;  background:#89e051;" data-w="6.47"></div>
      <div class="lang-seg" style="width:3.13%;  background:#4F5D95;" data-w="3.13"></div>
      <div class="lang-seg" style="width:0.07%;  background:#701516;" data-w="0.07"></div>
    </div>

    <div class="lang-grid">
      <div class="lang-row">
        <div class="lang-dot" style="background:#3572A5;box-shadow:0 0 8px #3572A5;"></div>
        <span class="lang-name">Python</span>
        <div class="lang-bar-wrap"><div class="lang-bar-fill" style="background:#3572A5;" data-pct="24.94"></div></div>
        <span class="lang-pct">24.94%</span>
      </div>
      <div class="lang-row">
        <div class="lang-dot" style="background:#f1e05a;box-shadow:0 0 8px #f1e05a;"></div>
        <span class="lang-name">JavaScript</span>
        <div class="lang-bar-wrap"><div class="lang-bar-fill" style="background:#f1e05a;" data-pct="9.65"></div></div>
        <span class="lang-pct">9.65%</span>
      </div>
      <div class="lang-row">
        <div class="lang-dot" style="background:#f34b7d;box-shadow:0 0 8px #f34b7d;"></div>
        <span class="lang-name">C++</span>
        <div class="lang-bar-wrap"><div class="lang-bar-fill" style="background:#f34b7d;" data-pct="23.89"></div></div>
        <span class="lang-pct">23.89%</span>
      </div>
      <div class="lang-row">
        <div class="lang-dot" style="background:#89e051;box-shadow:0 0 8px #89e051;"></div>
        <span class="lang-name">Shell</span>
        <div class="lang-bar-wrap"><div class="lang-bar-fill" style="background:#89e051;" data-pct="6.47"></div></div>
        <span class="lang-pct">6.47%</span>
      </div>
      <div class="lang-row">
        <div class="lang-dot" style="background:#00ADD8;box-shadow:0 0 8px #00ADD8;"></div>
        <span class="lang-name">Go</span>
        <div class="lang-bar-wrap"><div class="lang-bar-fill" style="background:#00ADD8;" data-pct="20.94"></div></div>
        <span class="lang-pct">20.94%</span>
      </div>
      <div class="lang-row">
        <div class="lang-dot" style="background:#4F5D95;box-shadow:0 0 8px #4F5D95;"></div>
        <span class="lang-name">PHP</span>
        <div class="lang-bar-wrap"><div class="lang-bar-fill" style="background:#4F5D95;" data-pct="3.13"></div></div>
        <span class="lang-pct">3.13%</span>
      </div>
      <div class="lang-row">
        <div class="lang-dot" style="background:#555555;box-shadow:0 0 8px #999;"></div>
        <span class="lang-name">C</span>
        <div class="lang-bar-wrap"><div class="lang-bar-fill" style="background:#555555;" data-pct="10.92"></div></div>
        <span class="lang-pct">10.92%</span>
      </div>
      <div class="lang-row">
        <div class="lang-dot" style="background:#701516;box-shadow:0 0 8px #701516;"></div>
        <span class="lang-name">Ruby</span>
        <div class="lang-bar-wrap"><div class="lang-bar-fill" style="background:#701516;" data-pct="0.07"></div></div>
        <span class="lang-pct">0.07%</span>
      </div>
    </div>
  </div>

  <div class="glow-line"></div>

  <!-- ═══ TECH BADGES ═══ -->
  <div class="section-heading">◈ &nbsp; Tech Stack &nbsp; ◈</div>
  <div class="badge-row" id="badge-row">
    <span class="badge badge-cyan">Python</span>
    <span class="badge badge-pink">C++</span>
    <span class="badge badge-cyan">Go</span>
    <span class="badge badge-purple">JavaScript</span>
    <span class="badge badge-gold">Shell</span>
    <span class="badge badge-pink">Linux</span>
    <span class="badge badge-cyan">Docker</span>
    <span class="badge badge-purple">Kubernetes</span>
    <span class="badge badge-gold">Git</span>
    <span class="badge badge-pink">PostgreSQL</span>
    <span class="badge badge-cyan">Redis</span>
    <span class="badge badge-purple">Rust</span>
    <span class="badge badge-gold">gRPC</span>
    <span class="badge badge-pink">Terraform</span>
    <span class="badge badge-cyan">AWS</span>
    <span class="badge badge-purple">CI/CD</span>
  </div>

  <!-- ═══ FOOTER ═══ -->
  <div class="footer">
    <div>◈ &nbsp; DAVID &nbsp;·&nbsp; <span>6,284 CONTRIBUTIONS</span> &nbsp;·&nbsp; <span>501 STARS</span> &nbsp;·&nbsp; <span>1.2K PRs</span> &nbsp; ◈</div>
    <div style="margin-top:8px;">REPLACE <span>YOUR_USERNAME</span> WITH YOUR GITHUB HANDLE &nbsp;·&nbsp; BUILT WITH MOTION &amp; PRECISION</div>
  </div>

</div><!-- /wrapper -->

<script>
/* ══════════════════════════════════════════════
   PARTICLES
══════════════════════════════════════════════ */
(function(){
  const canvas = document.getElementById('particle-canvas');
  const ctx = canvas.getContext('2d');
  let W, H, particles = [];

  function resize(){
    W = canvas.width = window.innerWidth;
    H = canvas.height = window.innerHeight;
  }
  resize();
  window.addEventListener('resize', resize);

  function rand(a,b){ return a + Math.random()*(b-a); }

  const COLORS = ['rgba(255,45,120,', 'rgba(0,245,255,', 'rgba(168,85,247,'];

  for(let i=0;i<90;i++){
    particles.push({
      x: rand(0, window.innerWidth),
      y: rand(0, window.innerHeight),
      r: rand(0.5, 2.5),
      vx: rand(-0.3,0.3),
      vy: rand(-0.5,-0.1),
      col: COLORS[Math.floor(rand(0,3))],
      alpha: rand(0.3, 0.9)
    });
  }

  function draw(){
    ctx.clearRect(0,0,W,H);
    particles.forEach(p=>{
      p.x += p.vx; p.y += p.vy;
      if(p.y < -10){ p.y = H+10; p.x = rand(0,W); }
      if(p.x < -10) p.x = W+10;
      if(p.x > W+10) p.x = -10;
      ctx.beginPath();
      ctx.arc(p.x, p.y, p.r, 0, Math.PI*2);
      ctx.fillStyle = p.col + p.alpha + ')';
      ctx.fill();
    });

    // draw faint connection lines
    for(let i=0;i<particles.length;i++){
      for(let j=i+1;j<particles.length;j++){
        const dx = particles[i].x - particles[j].x;
        const dy = particles[i].y - particles[j].y;
        const dist = Math.sqrt(dx*dx+dy*dy);
        if(dist < 100){
          ctx.beginPath();
          ctx.strokeStyle = 'rgba(255,45,120,' + (0.05*(1-dist/100)) + ')';
          ctx.lineWidth = 0.5;
          ctx.moveTo(particles[i].x, particles[i].y);
          ctx.lineTo(particles[j].x, particles[j].y);
          ctx.stroke();
        }
      }
    }
    requestAnimationFrame(draw);
  }
  draw();
})();

/* ══════════════════════════════════════════════
   TERMINAL TYPEWRITER
══════════════════════════════════════════════ */
(function(){
  const lines = [
    {id:'t1', delay:300},
    {id:'t2', delay:700},
    {id:'t3', delay:1400},
    {id:'t4', delay:1900},
    {id:'t5', delay:2600},
    {id:'t6', delay:3100},
    {id:'t7', delay:3800},
  ];
  lines.forEach(({id,delay})=>{
    setTimeout(()=>{
      const el = document.getElementById(id);
      if(el) el.style.cssText = 'opacity:1; animation: fadeUp 0.4s forwards;';
    }, delay);
  });
})();

/* ══════════════════════════════════════════════
   INTERSECTION OBSERVER — animate on scroll
══════════════════════════════════════════════ */
const io = new IntersectionObserver((entries)=>{
  entries.forEach(e=>{
    if(e.isIntersecting) animateSection(e.target);
  });
}, {threshold: 0.15});

/* Stats cards */
const statsGrid = document.getElementById('stats-grid');
io.observe(statsGrid);

function animateSection(el){
  if(el === statsGrid){
    el.querySelectorAll('.stat-card').forEach((card,i)=>{
      const delay = parseInt(card.dataset.delay)||0;
      setTimeout(()=>{
        card.style.cssText = 'opacity:1; transform:translateY(0); transition: opacity 0.6s, transform 0.6s;';
        const val = card.querySelector('[data-count]');
        if(val) countUp(val, parseInt(val.dataset.count));
      }, delay + 200);
    });
    io.unobserve(el);
  }

  if(el === streakRow){
    el.querySelectorAll('.streak-card').forEach((c,i)=>{
      setTimeout(()=>{
        c.style.cssText = 'opacity:1; transform:scale(1); transition: opacity 0.6s, transform 0.6s;';
      }, i*150+100);
    });
    io.unobserve(el);
  }

  if(el === langSection){
    setTimeout(()=>{
      el.style.cssText = 'opacity:1; transition: opacity 0.6s;';
      el.querySelectorAll('.lang-seg').forEach(s=>{
        s.style.transform = 'scaleX(1)';
      });
      el.querySelectorAll('.lang-bar-fill').forEach(b=>{
        b.style.transform = `scaleX(${parseFloat(b.dataset.pct)/100})`;
      });
    },200);
    io.unobserve(el);
  }

  if(el === activitySection){
    buildActivityBars();
    setTimeout(()=>{ el.style.cssText = 'opacity:1; transition: opacity 0.6s;'; },100);
    io.unobserve(el);
  }

  if(el === badgeRow){
    el.querySelectorAll('.badge').forEach((b,i)=>{
      setTimeout(()=>{
        b.style.cssText = 'opacity:1; transform:translateY(0); transition: opacity 0.4s, transform 0.4s, box-shadow 0.25s;';
      }, i*55);
    });
    io.unobserve(el);
  }
}

const streakRow      = document.getElementById('streak-row');
const langSection    = document.getElementById('lang-section');
const activitySection= document.getElementById('activity-section');
const badgeRow       = document.getElementById('badge-row');

io.observe(streakRow);
io.observe(langSection);
io.observe(activitySection);
io.observe(badgeRow);

/* ══════════════════════════════════════════════
   COUNT-UP
══════════════════════════════════════════════ */
function countUp(el, target){
  const duration = 1500;
  const start = Date.now();
  function step(){
    const p = Math.min((Date.now()-start)/duration, 1);
    const eased = 1 - Math.pow(1-p, 3);
    const val = Math.round(eased * target);
    el.textContent = val >= 1000 ? val.toLocaleString() : val;
    if(p < 1) requestAnimationFrame(step);
  }
  requestAnimationFrame(step);
}

/* ══════════════════════════════════════════════
   ACTIVITY BARS
══════════════════════════════════════════════ */
function buildActivityBars(){
  const container = document.getElementById('activity-line');
  const seed = [40,65,30,80,55,70,90,45,60,75,35,85,50,95,40,70,55,80,65,45,30,75,90,60,40,55,80,70,35,65,50,85,45,75,60,30,90,55,70,45,65,80,50,35,75,60,90,45,70,55,30,80];
  seed.forEach((h,i)=>{
    const bar = document.createElement('div');
    bar.className = 'act-bar';
    bar.style.height = h + '%';
    bar.style.animationDelay = (i * 18) + 'ms';
    bar.style.animationDuration = '0.4s';
    container.appendChild(bar);
  });
}
</script>
</body>
</html>
