<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Tarik Bufardi — Portfolio</title>
  <link href="https://fonts.googleapis.com/css2?family=Press+Start+2P&family=VT323:wght@400&family=Share+Tech+Mono&display=swap" rel="stylesheet"/>
  <style>
    :root {
      --green: #00ff41;
      --green-dim: #00aa2a;
      --green-dark: #003d0f;
      --bg: #0a0a0a;
      --bg2: #0f0f0f;
      --amber: #ffb000;
      --cyan: #00eeff;
      --red: #ff2244;
      --white: #e8ffe8;
      --scanline: rgba(0,255,65,0.03);
    }

    * { margin: 0; padding: 0; box-sizing: border-box; }

    html { scroll-behavior: smooth; }

    body {
      background: var(--bg);
      color: var(--green);
      font-family: 'Share Tech Mono', monospace;
      font-size: 15px;
      line-height: 1.7;
      overflow-x: hidden;
      cursor: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='16' height='16'%3E%3Crect x='6' y='0' width='4' height='16' fill='%2300ff41'/%3E%3Crect x='0' y='6' width='16' height='4' fill='%2300ff41'/%3E%3C/svg%3E") 8 8, crosshair;
    }

    /* CRT SCANLINES OVERLAY */
    body::before {
      content: '';
      position: fixed;
      top: 0; left: 0;
      width: 100%; height: 100%;
      background: repeating-linear-gradient(
        to bottom,
        transparent 0px,
        transparent 3px,
        var(--scanline) 3px,
        var(--scanline) 4px
      );
      pointer-events: none;
      z-index: 9999;
    }

    /* CRT VIGNETTE */
    body::after {
      content: '';
      position: fixed;
      top: 0; left: 0;
      width: 100%; height: 100%;
      background: radial-gradient(ellipse at center, transparent 60%, rgba(0,0,0,0.85) 100%);
      pointer-events: none;
      z-index: 9998;
    }

    /* NOISE TEXTURE */
    .noise {
      position: fixed;
      top: 0; left: 0;
      width: 100%; height: 100%;
      opacity: 0.025;
      pointer-events: none;
      z-index: 9997;
      background-image: url("data:image/svg+xml,%3Csvg viewBox='0 0 256 256' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='noise'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.9' numOctaves='4' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23noise)'/%3E%3C/svg%3E");
    }

    /* ─── TOPBAR ─── */
    #topbar {
      position: fixed;
      top: 0; left: 0; right: 0;
      z-index: 1000;
      background: rgba(10,10,10,0.97);
      border-bottom: 1px solid var(--green-dim);
      padding: 10px 40px;
      display: flex;
      justify-content: space-between;
      align-items: center;
    }

    #topbar .logo {
      font-family: 'Press Start 2P', monospace;
      font-size: 10px;
      color: var(--green);
      text-shadow: 0 0 8px var(--green);
      letter-spacing: 2px;
    }

    #topbar .logo span { color: var(--amber); }

    nav a {
      font-family: 'Share Tech Mono', monospace;
      font-size: 13px;
      color: var(--green-dim);
      text-decoration: none;
      margin-left: 28px;
      letter-spacing: 1px;
      transition: color 0.2s, text-shadow 0.2s;
    }

    nav a:hover {
      color: var(--green);
      text-shadow: 0 0 8px var(--green);
    }

    /* ─── HERO ─── */
    #hero {
      min-height: 100vh;
      display: flex;
      flex-direction: column;
      justify-content: center;
      align-items: flex-start;
      padding: 120px 10vw 60px;
      position: relative;
    }

    .boot-text {
      font-family: 'VT323', monospace;
      font-size: 18px;
      color: var(--green-dim);
      margin-bottom: 30px;
      opacity: 0;
      animation: fadeIn 0.5s ease 0.3s forwards;
    }

    .boot-text span { color: var(--amber); }

    .hero-name {
      font-family: 'Press Start 2P', monospace;
      font-size: clamp(22px, 4vw, 48px);
      color: var(--green);
      text-shadow:
        0 0 10px var(--green),
        0 0 30px var(--green),
        0 0 60px var(--green-dim);
      line-height: 1.5;
      opacity: 0;
      animation: glitchIn 0.8s ease 0.8s forwards;
    }

    .hero-name .highlight { color: var(--amber); text-shadow: 0 0 15px var(--amber); }

    .hero-sub {
      font-family: 'VT323', monospace;
      font-size: 28px;
      color: var(--cyan);
      margin-top: 20px;
      letter-spacing: 3px;
      opacity: 0;
      animation: fadeIn 0.5s ease 1.4s forwards;
    }

    .hero-desc {
      margin-top: 16px;
      font-size: 14px;
      color: var(--green-dim);
      max-width: 520px;
      opacity: 0;
      animation: fadeIn 0.5s ease 1.7s forwards;
    }

    .cta-row {
      margin-top: 40px;
      display: flex;
      gap: 20px;
      flex-wrap: wrap;
      opacity: 0;
      animation: fadeIn 0.5s ease 2s forwards;
    }

    .btn {
      font-family: 'Press Start 2P', monospace;
      font-size: 9px;
      padding: 14px 22px;
      border: 2px solid var(--green);
      color: var(--green);
      background: transparent;
      cursor: pointer;
      text-decoration: none;
      display: inline-block;
      letter-spacing: 1px;
      transition: all 0.2s;
      position: relative;
      overflow: hidden;
    }

    .btn::before {
      content: '';
      position: absolute;
      top: 0; left: -100%;
      width: 100%; height: 100%;
      background: var(--green);
      transition: left 0.25s ease;
      z-index: -1;
    }

    .btn:hover::before { left: 0; }
    .btn:hover { color: var(--bg); }

    .btn.amber {
      border-color: var(--amber);
      color: var(--amber);
    }
    .btn.amber::before { background: var(--amber); }

    /* BLINKING CURSOR */
    .cursor {
      display: inline-block;
      width: 12px;
      height: 20px;
      background: var(--green);
      margin-left: 6px;
      vertical-align: middle;
      animation: blink 1s step-end infinite;
    }

    /* PIXEL ART DECORATION */
    .pixel-deco {
      position: absolute;
      right: 8vw;
      top: 50%;
      transform: translateY(-50%);
      opacity: 0;
      animation: fadeIn 1s ease 1.5s forwards;
    }

    .pixel-deco svg { filter: drop-shadow(0 0 12px var(--green)); }

    /* GRID BG */
    .grid-bg {
      position: absolute;
      inset: 0;
      background-image:
        linear-gradient(rgba(0,255,65,0.04) 1px, transparent 1px),
        linear-gradient(90deg, rgba(0,255,65,0.04) 1px, transparent 1px);
      background-size: 40px 40px;
      z-index: -1;
    }

    /* ─── SECTIONS ─── */
    section {
      padding: 80px 10vw;
      border-top: 1px solid var(--green-dark);
      position: relative;
    }

    .section-header {
      font-family: 'Press Start 2P', monospace;
      font-size: 13px;
      color: var(--amber);
      text-shadow: 0 0 10px var(--amber);
      margin-bottom: 10px;
      letter-spacing: 2px;
    }

    .section-header::before {
      content: '> ';
      color: var(--green-dim);
    }

    .section-divider {
      border: none;
      height: 1px;
      background: linear-gradient(to right, var(--green-dim), transparent);
      margin-bottom: 50px;
      width: 200px;
    }

    /* ─── ABOUT ─── */
    #about .about-grid {
      display: grid;
      grid-template-columns: 1fr 1fr;
      gap: 60px;
      align-items: start;
    }

    .terminal-box {
      background: var(--bg2);
      border: 1px solid var(--green-dim);
      padding: 0;
      font-family: 'Share Tech Mono', monospace;
    }

    .terminal-header {
      background: var(--green-dark);
      padding: 8px 14px;
      font-size: 11px;
      color: var(--green-dim);
      display: flex;
      align-items: center;
      gap: 8px;
    }

    .dot { width: 8px; height: 8px; background: var(--green-dim); display: inline-block; }
    .dot.red { background: var(--red); }
    .dot.amber { background: var(--amber); }

    .terminal-body {
      padding: 20px;
      font-size: 13px;
      color: var(--green-dim);
      line-height: 2;
    }

    .terminal-body .line::before { content: '$ '; color: var(--green); }
    .terminal-body .output { color: var(--white); padding-left: 16px; margin-bottom: 8px; }
    .terminal-body .comment { color: #336633; }

    /* STATS */
    .stat-grid {
      display: grid;
      grid-template-columns: 1fr 1fr;
      gap: 16px;
    }

    .stat-card {
      border: 1px solid var(--green-dark);
      padding: 20px;
      text-align: center;
      transition: border-color 0.2s, box-shadow 0.2s;
    }

    .stat-card:hover {
      border-color: var(--green);
      box-shadow: 0 0 15px rgba(0,255,65,0.15);
    }

    .stat-num {
      font-family: 'Press Start 2P', monospace;
      font-size: 22px;
      color: var(--green);
      text-shadow: 0 0 10px var(--green);
      display: block;
    }

    .stat-label {
      font-size: 11px;
      color: var(--green-dim);
      margin-top: 6px;
    }

    /* ─── SKILLS ─── */
    #skills .skills-grid {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(260px, 1fr));
      gap: 24px;
    }

    .skill-category {
      background: var(--bg2);
      border: 1px solid var(--green-dark);
      padding: 24px;
      transition: border-color 0.3s, transform 0.3s;
    }

    .skill-category:hover {
      border-color: var(--green-dim);
      transform: translateY(-4px);
    }

    .skill-cat-title {
      font-family: 'Press Start 2P', monospace;
      font-size: 8px;
      color: var(--cyan);
      margin-bottom: 20px;
      letter-spacing: 1px;
    }

    .skill-item {
      margin-bottom: 16px;
    }

    .skill-name {
      font-size: 12px;
      color: var(--white);
      margin-bottom: 6px;
      display: flex;
      justify-content: space-between;
    }

    .skill-name span { color: var(--green-dim); font-size: 11px; }

    .skill-bar-bg {
      height: 8px;
      background: var(--green-dark);
      position: relative;
      overflow: hidden;
    }

    .skill-bar-fill {
      height: 100%;
      background: var(--green);
      box-shadow: 0 0 8px var(--green);
      width: 0;
      transition: width 1.4s cubic-bezier(0.4,0,0.2,1);
      position: relative;
    }

    .skill-bar-fill::after {
      content: '';
      position: absolute;
      right: 0; top: 0;
      width: 4px; height: 100%;
      background: white;
      opacity: 0.8;
    }

    .skill-bar-fill.amber { background: var(--amber); box-shadow: 0 0 8px var(--amber); }
    .skill-bar-fill.cyan  { background: var(--cyan);  box-shadow: 0 0 8px var(--cyan);  }

    /* ─── PROJECTS ─── */
    #projects .projects-grid {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
      gap: 28px;
    }

    .project-card {
      background: var(--bg2);
      border: 1px solid var(--green-dark);
      padding: 28px;
      transition: all 0.3s;
      position: relative;
      overflow: hidden;
    }

    .project-card::before {
      content: '';
      position: absolute;
      top: 0; left: 0;
      width: 3px; height: 0;
      background: var(--green);
      transition: height 0.3s;
    }

    .project-card:hover { border-color: var(--green-dim); }
    .project-card:hover::before { height: 100%; }

    .project-id {
      font-family: 'Press Start 2P', monospace;
      font-size: 8px;
      color: var(--green-dark);
      margin-bottom: 14px;
    }

    .project-title {
      font-family: 'VT323', monospace;
      font-size: 26px;
      color: var(--green);
      margin-bottom: 12px;
    }

    .project-desc {
      font-size: 12px;
      color: var(--green-dim);
      margin-bottom: 20px;
      line-height: 1.8;
    }

    .tag-row { display: flex; flex-wrap: wrap; gap: 8px; margin-bottom: 20px; }

    .tag {
      font-size: 10px;
      padding: 3px 10px;
      border: 1px solid var(--green-dark);
      color: var(--green-dim);
      font-family: 'Share Tech Mono', monospace;
    }

    .tag.amber { border-color: var(--amber); color: var(--amber); }

    .project-links { display: flex; gap: 14px; }

    .project-link {
      font-size: 11px;
      color: var(--green-dim);
      text-decoration: none;
      transition: color 0.2s;
      font-family: 'Share Tech Mono', monospace;
    }

    .project-link:hover { color: var(--green); text-shadow: 0 0 6px var(--green); }
    .project-link::before { content: '[ '; }
    .project-link::after  { content: ' ]'; }

    /* ─── CONTACT ─── */
    #contact {
      text-align: center;
    }

    .contact-box {
      max-width: 560px;
      margin: 0 auto;
      background: var(--bg2);
      border: 1px solid var(--green-dim);
      padding: 50px;
    }

    .contact-box p {
      font-size: 13px;
      color: var(--green-dim);
      margin-bottom: 36px;
      line-height: 2;
    }

    .contact-links {
      display: flex;
      justify-content: center;
      gap: 20px;
      flex-wrap: wrap;
    }

    /* ─── FOOTER ─── */
    footer {
      border-top: 1px solid var(--green-dark);
      padding: 24px 10vw;
      display: flex;
      justify-content: space-between;
      align-items: center;
      font-size: 11px;
      color: var(--green-dark);
    }

    footer span { color: var(--green-dim); }

    /* ─── ANIMATIONS ─── */
    @keyframes blink {
      0%, 100% { opacity: 1; }
      50%       { opacity: 0; }
    }

    @keyframes fadeIn {
      from { opacity: 0; transform: translateY(10px); }
      to   { opacity: 1; transform: translateY(0); }
    }

    @keyframes glitchIn {
      0%   { opacity: 0; transform: skewX(10deg); filter: blur(4px); }
      40%  { opacity: 1; transform: skewX(-3deg); filter: blur(0); }
      60%  { transform: skewX(2deg); }
      80%  { transform: skewX(-1deg); }
      100% { opacity: 1; transform: skewX(0); }
    }

    @keyframes glitch {
      0%, 90%, 100% { transform: translate(0); }
      92%           { transform: translate(-3px, 1px); color: var(--cyan); }
      94%           { transform: translate(3px, -1px); color: var(--red); }
      96%           { transform: translate(-2px, 0); }
    }

    .hero-name { animation: glitchIn 0.8s ease 0.8s forwards, glitch 6s infinite 3s; }

    @keyframes scanMove {
      0%   { top: -10%; }
      100% { top: 110%; }
    }

    .scan-line {
      position: fixed;
      left: 0; right: 0;
      height: 2px;
      background: linear-gradient(to right, transparent, rgba(0,255,65,0.15), transparent);
      animation: scanMove 6s linear infinite;
      z-index: 9996;
      pointer-events: none;
    }

    /* ─── RESPONSIVE ─── */
    @media (max-width: 768px) {
      #about .about-grid { grid-template-columns: 1fr; }
      .pixel-deco { display: none; }
      #topbar { padding: 10px 20px; }
      nav a { margin-left: 14px; font-size: 11px; }
      section { padding: 60px 6vw; }
      .contact-box { padding: 30px 20px; }
    }
  </style>
</head>
<body>
  <div class="noise"></div>
  <div class="scan-line"></div>

  <!-- TOPBAR -->
  <div id="topbar">
    <div class="logo">T<span>.</span>BUFARDI</div>
    <nav>
      <a href="#about">ABOUT</a>
      <a href="#skills">SKILLS</a>
      <a href="#projects">PROJECTS</a>
      <a href="#contact">CONTACT</a>
    </nav>
  </div>

  <!-- HERO -->
  <section id="hero">
    <div class="grid-bg"></div>
    <p class="boot-text">// SYSTEM BOOT... <span>OK</span> &nbsp;|&nbsp; LOADING PORTFOLIO... <span>DONE</span></p>
    <h1 class="hero-name">TARIK<br><span class="highlight">BUFARDI</span></h1>
    <p class="hero-sub">WEB DEVELOPER &amp; CRAFTSMAN</p>
    <p class="hero-desc">
      22 y/o developer passionate about building things for the web.<br>
      HTML · CSS · JavaScript · PHP — pixel by pixel.
    </p>
    <div class="cta-row">
      <a href="#projects" class="btn">VIEW PROJECTS</a>
      <a href="#contact" class="btn amber">CONTACT ME</a>
    </div>

    <!-- PIXEL ART AVATAR -->
    <div class="pixel-deco">
      <svg width="160" height="180" viewBox="0 0 160 180" xmlns="http://www.w3.org/2000/svg">
        <!-- pixel character -->
        <rect x="56" y="16" width="48" height="48" fill="#00ff41" opacity="0.9"/>
        <rect x="64" y="28" width="12" height="12" fill="#0a0a0a"/>
        <rect x="84" y="28" width="12" height="12" fill="#0a0a0a"/>
        <rect x="72" y="48" width="16" height="4" fill="#0a0a0a"/>
        <rect x="44" y="64" width="72" height="48" fill="#00aa2a"/>
        <rect x="28" y="64" width="20" height="40" fill="#00aa2a"/>
        <rect x="112" y="64" width="20" height="40" fill="#00aa2a"/>
        <rect x="8" y="64" width="24" height="8" fill="#00aa2a"/>
        <rect x="128" y="64" width="24" height="8" fill="#00aa2a"/>
        <rect x="52" y="112" width="24" height="52" fill="#00aa2a"/>
        <rect x="84" y="112" width="24" height="52" fill="#00aa2a"/>
        <rect x="36" y="156" width="28" height="12" fill="#00aa2a"/>
        <rect x="96" y="156" width="28" height="12" fill="#00aa2a"/>
        <!-- glow base -->
        <rect x="40" y="168" width="80" height="8" fill="#003d0f" opacity="0.6"/>
      </svg>
    </div>
  </section>

  <!-- ABOUT -->
  <section id="about">
    <p class="section-header">ABOUT_ME.EXE</p>
    <hr class="section-divider"/>
    <div class="about-grid">
      <div class="terminal-box">
        <div class="terminal-header">
          <span class="dot red"></span>
          <span class="dot amber"></span>
          <span class="dot"></span>
          &nbsp; terminal — tarik@portfolio
        </div>
        <div class="terminal-body">
          <p class="line">whoami</p>
          <p class="output">Tarik Bufardi, 22</p>
          <p class="line">cat bio.txt</p>
          <p class="output">Web developer focused on crafting<br>clean, functional interfaces and<br>solid back-end logic with PHP.</p>
          <p class="line">cat interests.txt</p>
          <p class="output">Building for the web, open source,<br>retro aesthetics, problem solving.</p>
          <p class="comment"># always learning, always building</p>
          <p class="line">_<span class="cursor"></span></p>
        </div>
      </div>
      <div class="stat-grid">
        <div class="stat-card">
          <span class="stat-num">22</span>
          <p class="stat-label">YEARS OLD</p>
        </div>
        <div class="stat-card">
          <span class="stat-num">4+</span>
          <p class="stat-label">LANGUAGES</p>
        </div>
        <div class="stat-card">
          <span class="stat-num">∞</span>
          <p class="stat-label">COFFEE CUPS</p>
        </div>
        <div class="stat-card">
          <span class="stat-num">01</span>
          <p class="stat-label">MISSION</p>
        </div>
      </div>
    </div>
  </section>

  <!-- SKILLS -->
  <section id="skills">
    <p class="section-header">SKILLS.DAT</p>
    <hr class="section-divider"/>
    <div class="skills-grid">
      <div class="skill-category">
        <p class="skill-cat-title">[ FRONTEND ]</p>
        <div class="skill-item">
          <div class="skill-name">HTML5 <span>95%</span></div>
          <div class="skill-bar-bg"><div class="skill-bar-fill" data-w="95"></div></div>
        </div>
        <div class="skill-item">
          <div class="skill-name">CSS3 <span>88%</span></div>
          <div class="skill-bar-bg"><div class="skill-bar-fill" data-w="88"></div></div>
        </div>
        <div class="skill-item">
          <div class="skill-name">JavaScript <span>80%</span></div>
          <div class="skill-bar-bg"><div class="skill-bar-fill" data-w="80"></div></div>
        </div>
      </div>
      <div class="skill-category">
        <p class="skill-cat-title">[ BACKEND ]</p>
        <div class="skill-item">
          <div class="skill-name">PHP <span>75%</span></div>
          <div class="skill-bar-bg"><div class="skill-bar-fill amber" data-w="75"></div></div>
        </div>
        <div class="skill-item">
          <div class="skill-name">MySQL <span>68%</span></div>
          <div class="skill-bar-bg"><div class="skill-bar-fill amber" data-w="68"></div></div>
        </div>
        <div class="skill-item">
          <div class="skill-name">REST APIs <span>60%</span></div>
          <div class="skill-bar-bg"><div class="skill-bar-fill amber" data-w="60"></div></div>
        </div>
      </div>
      <div class="skill-category">
        <p class="skill-cat-title">[ TOOLS ]</p>
        <div class="skill-item">
          <div class="skill-name">Git / GitHub <span>85%</span></div>
          <div class="skill-bar-bg"><div class="skill-bar-fill cyan" data-w="85"></div></div>
        </div>
        <div class="skill-item">
          <div class="skill-name">VS Code <span>90%</span></div>
          <div class="skill-bar-bg"><div class="skill-bar-fill cyan" data-w="90"></div></div>
        </div>
        <div class="skill-item">
          <div class="skill-name">Responsive Design <span>82%</span></div>
          <div class="skill-bar-bg"><div class="skill-bar-fill cyan" data-w="82"></div></div>
        </div>
      </div>
    </div>
  </section>

  <!-- PROJECTS -->
  <section id="projects">
    <p class="section-header">PROJECTS.LOG</p>
    <hr class="section-divider"/>
    <div class="projects-grid">
      <div class="project-card">
        <p class="project-id">PROJECT_001</p>
        <p class="project-title">My Portfolio Site</p>
        <p class="project-desc">This very site — a retro-terminal themed portfolio built from scratch with HTML, CSS and vanilla JS. No frameworks, just craft.</p>
        <div class="tag-row">
          <span class="tag">HTML</span>
          <span class="tag">CSS</span>
          <span class="tag">JS</span>
        </div>
        <div class="project-links">
          <a href="#" class="project-link">GITHUB</a>
          <a href="#" class="project-link">LIVE</a>
        </div>
      </div>
      <div class="project-card">
        <p class="project-id">PROJECT_002</p>
        <p class="project-title">PHP Web App</p>
        <p class="project-desc">A dynamic web application built with PHP and MySQL. Features user authentication, CRUD operations and a clean admin dashboard.</p>
        <div class="tag-row">
          <span class="tag amber">PHP</span>
          <span class="tag amber">MySQL</span>
          <span class="tag">HTML</span>
          <span class="tag">CSS</span>
        </div>
        <div class="project-links">
          <a href="#" class="project-link">GITHUB</a>
          <a href="#" class="project-link">LIVE</a>
        </div>
      </div>
      <div class="project-card">
        <p class="project-id">PROJECT_003</p>
        <p class="project-title">JS Interactive UI</p>
        <p class="project-desc">An interactive front-end experiment — animations, DOM manipulation and a smooth user experience. Pure JavaScript, zero dependencies.</p>
        <div class="tag-row">
          <span class="tag">JS</span>
          <span class="tag">CSS</span>
          <span class="tag">HTML</span>
        </div>
        <div class="project-links">
          <a href="#" class="project-link">GITHUB</a>
          <a href="#" class="project-link">LIVE</a>
        </div>
      </div>
    </div>
  </section>

  <!-- CONTACT -->
  <section id="contact">
    <p class="section-header">CONTACT.SH</p>
    <hr class="section-divider" style="margin: 0 auto 50px;"/>
    <div class="contact-box">
      <p>Have a project in mind or just want to say hi?<br>
      My inbox is always open — let's build something together.</p>
      <div class="contact-links">
        <a href="mailto:tarik@example.com" class="btn">EMAIL ME</a>
        <a href="https://github.com/" target="_blank" class="btn amber">GITHUB</a>
      </div>
    </div>
  </section>

  <!-- FOOTER -->
  <footer>
    <span>© 2026 TARIK BUFARDI</span>
    <span>CRAFTED WITH &lt;3 + CAFFEINE</span>
  </footer>

  <script>
    // ── Skill bars animate on scroll ──
    const bars = document.querySelectorAll('.skill-bar-fill');
    const observer = new IntersectionObserver(entries => {
      entries.forEach(e => {
        if (e.isIntersecting) {
          e.target.style.width = e.target.dataset.w + '%';
        }
      });
    }, { threshold: 0.3 });
    bars.forEach(b => observer.observe(b));

    // ── Typewriter boot sequence ──
    const bootEl = document.querySelector('.boot-text');
    const messages = [
      '// SYSTEM BOOT... <span>OK</span> &nbsp;|&nbsp; LOADING PORTFOLIO... <span>DONE</span>',
      '// WELCOME, VISITOR. &nbsp;<span>ENJOY THE RIDE.</span>'
    ];
    let mi = 0;
    setInterval(() => {
      mi = (mi + 1) % messages.length;
      bootEl.innerHTML = messages[mi];
    }, 4000);

    // ── Smooth active nav highlight ──
    const sections = document.querySelectorAll('section[id]');
    const navLinks = document.querySelectorAll('nav a');
    window.addEventListener('scroll', () => {
      let current = '';
      sections.forEach(s => {
        if (window.scrollY >= s.offsetTop - 120) current = s.id;
      });
      navLinks.forEach(a => {
        a.style.color = a.getAttribute('href') === '#' + current
          ? 'var(--green)' : '';
        a.style.textShadow = a.getAttribute('href') === '#' + current
          ? '0 0 8px var(--green)' : '';
      });
    });

    // ── Random glitch flicker on hero name ──
    const heroName = document.querySelector('.hero-name');
    setInterval(() => {
      if (Math.random() < 0.15) {
        heroName.style.filter = 'blur(1px)';
        setTimeout(() => heroName.style.filter = '', 80);
      }
    }, 2000);
  </script>
</body>
</html>
