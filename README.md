<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Kaustubh Pawar — Full Stack Developer</title>
<link href="https://fonts.googleapis.com/css2?family=Syne:wght@400;600;700;800&family=DM+Mono:wght@300;400;500&display=swap" rel="stylesheet">
<style>
  :root {
    --bg: #050810;
    --surface: #0d1224;
    --surface2: #111827;
    --accent: #6ee7f7;
    --accent2: #a78bfa;
    --accent3: #f472b6;
    --gold: #fbbf24;
    --text: #e2e8f0;
    --muted: #64748b;
    --card-bg: rgba(13,18,36,0.85);
    --glow: 0 0 40px rgba(110,231,247,0.15);
  }

  *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

  html { scroll-behavior: smooth; }

  body {
    background: var(--bg);
    color: var(--text);
    font-family: 'DM Mono', monospace;
    overflow-x: hidden;
    min-height: 100vh;
  }

  /* ── CANVAS BG ── */
  #bgCanvas {
    position: fixed;
    inset: 0;
    z-index: 0;
    opacity: 0.6;
  }

  /* ── NOISE OVERLAY ── */
  body::before {
    content: '';
    position: fixed;
    inset: 0;
    background-image: url("data:image/svg+xml,%3Csvg viewBox='0 0 256 256' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='noise'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.9' numOctaves='4' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23noise)' opacity='0.03'/%3E%3C/svg%3E");
    pointer-events: none;
    z-index: 1;
    opacity: 0.4;
  }

  .wrapper {
    position: relative;
    z-index: 2;
    max-width: 1100px;
    margin: 0 auto;
    padding: 0 24px 80px;
  }

  /* ── HERO ── */
  .hero {
    min-height: 100vh;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    text-align: center;
    padding: 60px 20px;
    position: relative;
  }

  .avatar-ring {
    position: relative;
    width: 140px;
    height: 140px;
    margin-bottom: 36px;
    animation: floatAvatar 4s ease-in-out infinite;
  }

  @keyframes floatAvatar {
    0%, 100% { transform: translateY(0) rotateY(0deg); }
    50% { transform: translateY(-12px) rotateY(8deg); }
  }

  .avatar-ring::before {
    content: '';
    position: absolute;
    inset: -8px;
    border-radius: 50%;
    background: conic-gradient(from 0deg, var(--accent), var(--accent2), var(--accent3), var(--accent));
    animation: spinRing 4s linear infinite;
    z-index: -1;
  }

  @keyframes spinRing { to { transform: rotate(360deg); } }

  .avatar-inner {
    width: 140px;
    height: 140px;
    border-radius: 50%;
    background: linear-gradient(135deg, var(--accent2) 0%, var(--accent) 50%, var(--accent3) 100%);
    display: flex;
    align-items: center;
    justify-content: center;
    font-family: 'Syne', sans-serif;
    font-size: 52px;
    font-weight: 800;
    color: var(--bg);
    position: relative;
    z-index: 1;
    box-shadow: 0 0 60px rgba(110,231,247,0.3), 0 0 120px rgba(167,139,250,0.2);
  }

  .hero-greeting {
    font-family: 'DM Mono', monospace;
    font-size: 13px;
    color: var(--accent);
    letter-spacing: 4px;
    text-transform: uppercase;
    margin-bottom: 16px;
    opacity: 0;
    animation: fadeUp 0.8s 0.2s forwards;
  }

  .hero-name {
    font-family: 'Syne', sans-serif;
    font-size: clamp(42px, 8vw, 88px);
    font-weight: 800;
    line-height: 1;
    margin-bottom: 16px;
    opacity: 0;
    animation: fadeUp 0.8s 0.4s forwards;
  }

  .hero-name span {
    background: linear-gradient(135deg, var(--accent) 0%, var(--accent2) 50%, var(--accent3) 100%);
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
    background-clip: text;
    display: block;
  }

  .hero-role {
    font-size: clamp(14px, 2vw, 17px);
    color: var(--muted);
    margin-bottom: 40px;
    opacity: 0;
    animation: fadeUp 0.8s 0.6s forwards;
  }

  .hero-role em {
    color: var(--accent2);
    font-style: normal;
  }

  .hero-badges {
    display: flex;
    flex-wrap: wrap;
    gap: 12px;
    justify-content: center;
    margin-bottom: 48px;
    opacity: 0;
    animation: fadeUp 0.8s 0.8s forwards;
  }

  .badge {
    padding: 8px 18px;
    border-radius: 100px;
    font-size: 12px;
    font-weight: 500;
    border: 1px solid;
    letter-spacing: 1px;
    transition: all 0.3s;
    cursor: default;
    backdrop-filter: blur(10px);
  }

  .badge:hover {
    transform: translateY(-3px) scale(1.05);
    box-shadow: 0 8px 30px rgba(0,0,0,0.4);
  }

  .badge-cyan { color: var(--accent); border-color: rgba(110,231,247,0.4); background: rgba(110,231,247,0.07); }
  .badge-purple { color: var(--accent2); border-color: rgba(167,139,250,0.4); background: rgba(167,139,250,0.07); }
  .badge-pink { color: var(--accent3); border-color: rgba(244,114,182,0.4); background: rgba(244,114,182,0.07); }
  .badge-gold { color: var(--gold); border-color: rgba(251,191,36,0.4); background: rgba(251,191,36,0.07); }

  .scroll-hint {
    opacity: 0;
    animation: fadeUp 0.8s 1.2s forwards;
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 8px;
    color: var(--muted);
    font-size: 11px;
    letter-spacing: 2px;
  }

  .scroll-line {
    width: 1px;
    height: 50px;
    background: linear-gradient(to bottom, var(--accent), transparent);
    animation: scrollLine 2s ease-in-out infinite;
  }

  @keyframes scrollLine {
    0% { transform: scaleY(0); transform-origin: top; }
    50% { transform: scaleY(1); transform-origin: top; }
    51% { transform: scaleY(1); transform-origin: bottom; }
    100% { transform: scaleY(0); transform-origin: bottom; }
  }

  @keyframes fadeUp {
    from { opacity: 0; transform: translateY(30px); }
    to { opacity: 1; transform: translateY(0); }
  }

  /* ── SECTION HEADERS ── */
  .section { padding: 80px 0 40px; }

  .section-label {
    font-size: 11px;
    letter-spacing: 4px;
    color: var(--accent);
    text-transform: uppercase;
    margin-bottom: 8px;
  }

  .section-title {
    font-family: 'Syne', sans-serif;
    font-size: clamp(28px, 5vw, 44px);
    font-weight: 800;
    margin-bottom: 48px;
    position: relative;
    display: inline-block;
  }

  .section-title::after {
    content: '';
    position: absolute;
    bottom: -8px;
    left: 0;
    width: 60px;
    height: 3px;
    background: linear-gradient(to right, var(--accent), var(--accent2));
    border-radius: 2px;
  }

  /* ── ABOUT ── */
  .about-grid {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 24px;
  }

  .about-card {
    background: var(--card-bg);
    border: 1px solid rgba(110,231,247,0.1);
    border-radius: 20px;
    padding: 28px;
    backdrop-filter: blur(20px);
    transition: all 0.4s cubic-bezier(0.175, 0.885, 0.32, 1.275);
    transform-style: preserve-3d;
    position: relative;
    overflow: hidden;
  }

  .about-card::before {
    content: '';
    position: absolute;
    inset: 0;
    background: radial-gradient(circle at var(--mx, 50%) var(--my, 50%), rgba(110,231,247,0.06) 0%, transparent 60%);
    opacity: 0;
    transition: opacity 0.3s;
    border-radius: inherit;
    pointer-events: none;
  }

  .about-card:hover::before { opacity: 1; }
  .about-card:hover {
    border-color: rgba(110,231,247,0.3);
    box-shadow: 0 20px 60px rgba(0,0,0,0.4), var(--glow);
    transform: translateY(-6px) rotateX(2deg);
  }

  .about-card-icon {
    font-size: 28px;
    margin-bottom: 16px;
    display: block;
  }

  .about-card h3 {
    font-family: 'Syne', sans-serif;
    font-size: 16px;
    font-weight: 700;
    color: var(--text);
    margin-bottom: 10px;
  }

  .about-card p {
    font-size: 13px;
    color: var(--muted);
    line-height: 1.7;
  }

  /* ── SKILLS ── */
  .skills-grid {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(280px, 1fr));
    gap: 20px;
  }

  .skill-group {
    background: var(--card-bg);
    border: 1px solid rgba(167,139,250,0.1);
    border-radius: 20px;
    padding: 24px;
    backdrop-filter: blur(20px);
    transition: all 0.4s;
    transform-style: preserve-3d;
  }

  .skill-group:hover {
    border-color: rgba(167,139,250,0.35);
    transform: translateY(-5px) rotateX(1deg);
    box-shadow: 0 20px 60px rgba(0,0,0,0.4), 0 0 40px rgba(167,139,250,0.1);
  }

  .skill-group-title {
    font-family: 'Syne', sans-serif;
    font-size: 13px;
    font-weight: 700;
    letter-spacing: 2px;
    text-transform: uppercase;
    margin-bottom: 18px;
    color: var(--accent2);
  }

  .skill-pills {
    display: flex;
    flex-wrap: wrap;
    gap: 8px;
  }

  .pill {
    padding: 5px 14px;
    border-radius: 100px;
    font-size: 12px;
    background: rgba(255,255,255,0.04);
    border: 1px solid rgba(255,255,255,0.08);
    color: var(--text);
    transition: all 0.25s;
    cursor: default;
  }

  .pill:hover {
    background: rgba(110,231,247,0.1);
    border-color: rgba(110,231,247,0.4);
    color: var(--accent);
    transform: scale(1.06);
  }

  /* ── PROJECTS ── */
  .projects-grid {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(320px, 1fr));
    gap: 24px;
  }

  .project-card {
    background: var(--card-bg);
    border: 1px solid rgba(255,255,255,0.06);
    border-radius: 24px;
    padding: 32px;
    backdrop-filter: blur(20px);
    position: relative;
    overflow: hidden;
    transition: all 0.5s cubic-bezier(0.175, 0.885, 0.32, 1.275);
    transform-style: preserve-3d;
    perspective: 1000px;
    cursor: pointer;
    text-decoration: none;
    display: block;
    color: inherit;
  }

  .project-card::before {
    content: '';
    position: absolute;
    top: 0; left: 0; right: 0;
    height: 3px;
    background: var(--card-accent, linear-gradient(to right, var(--accent), var(--accent2)));
    opacity: 0;
    transition: opacity 0.3s;
  }

  .project-card:hover::before { opacity: 1; }

  .project-card::after {
    content: '';
    position: absolute;
    inset: 0;
    background: radial-gradient(ellipse at 30% -10%, rgba(110,231,247,0.07) 0%, transparent 60%);
    pointer-events: none;
    opacity: 0;
    transition: opacity 0.4s;
  }

  .project-card:hover::after { opacity: 1; }

  .project-card:hover {
    border-color: rgba(110,231,247,0.25);
    box-shadow: 0 30px 80px rgba(0,0,0,0.5), 0 0 60px rgba(110,231,247,0.08);
    transform: translateY(-10px) rotateX(3deg) rotateY(-2deg);
  }

  .project-emoji {
    font-size: 36px;
    display: block;
    margin-bottom: 20px;
    filter: drop-shadow(0 0 20px rgba(110,231,247,0.4));
    transition: transform 0.3s;
  }

  .project-card:hover .project-emoji { transform: scale(1.15) rotate(5deg); }

  .project-title {
    font-family: 'Syne', sans-serif;
    font-size: 20px;
    font-weight: 700;
    margin-bottom: 10px;
    color: var(--text);
  }

  .project-desc {
    font-size: 13px;
    color: var(--muted);
    line-height: 1.7;
    margin-bottom: 20px;
  }

  .project-tags {
    display: flex;
    flex-wrap: wrap;
    gap: 6px;
    margin-bottom: 20px;
  }

  .project-tag {
    font-size: 11px;
    padding: 3px 10px;
    border-radius: 100px;
    background: rgba(255,255,255,0.04);
    border: 1px solid rgba(255,255,255,0.1);
    color: var(--muted);
  }

  .project-stat {
    font-size: 12px;
    color: var(--accent);
    font-weight: 500;
  }

  .project-arrow {
    position: absolute;
    top: 28px;
    right: 28px;
    font-size: 18px;
    color: var(--muted);
    transition: all 0.3s;
  }

  .project-card:hover .project-arrow {
    color: var(--accent);
    transform: translate(3px, -3px);
  }

  /* ── STATS ── */
  .stats-row {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));
    gap: 20px;
    margin-bottom: 60px;
  }

  .stat-card {
    background: var(--card-bg);
    border: 1px solid rgba(255,255,255,0.06);
    border-radius: 20px;
    padding: 28px 24px;
    text-align: center;
    backdrop-filter: blur(20px);
    transition: all 0.4s;
    position: relative;
    overflow: hidden;
  }

  .stat-card::before {
    content: '';
    position: absolute;
    bottom: 0; left: 0; right: 0;
    height: 2px;
    background: var(--stat-color, var(--accent));
    transform: scaleX(0);
    transition: transform 0.4s;
    border-radius: 2px;
  }

  .stat-card:hover::before { transform: scaleX(1); }
  .stat-card:hover { transform: translateY(-6px); box-shadow: 0 20px 60px rgba(0,0,0,0.4); }

  .stat-number {
    font-family: 'Syne', sans-serif;
    font-size: 40px;
    font-weight: 800;
    background: linear-gradient(135deg, var(--accent), var(--accent2));
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
    background-clip: text;
    line-height: 1;
    margin-bottom: 8px;
  }

  .stat-label {
    font-size: 12px;
    color: var(--muted);
    letter-spacing: 1px;
  }

  /* ── CONNECT ── */
  .connect-section {
    text-align: center;
    padding: 80px 0;
  }

  .connect-card {
    background: var(--card-bg);
    border: 1px solid rgba(110,231,247,0.15);
    border-radius: 32px;
    padding: 64px 40px;
    backdrop-filter: blur(30px);
    position: relative;
    overflow: hidden;
    max-width: 700px;
    margin: 0 auto;
  }

  .connect-card::before {
    content: '';
    position: absolute;
    top: -50%;
    left: -50%;
    width: 200%;
    height: 200%;
    background: radial-gradient(circle at center, rgba(110,231,247,0.04) 0%, transparent 60%);
    animation: rotateBg 15s linear infinite;
  }

  @keyframes rotateBg { to { transform: rotate(360deg); } }

  .connect-title {
    font-family: 'Syne', sans-serif;
    font-size: clamp(28px, 4vw, 40px);
    font-weight: 800;
    margin-bottom: 16px;
    position: relative;
  }

  .connect-sub {
    font-size: 14px;
    color: var(--muted);
    margin-bottom: 40px;
    position: relative;
    line-height: 1.6;
  }

  .connect-btn {
    display: inline-flex;
    align-items: center;
    gap: 10px;
    padding: 16px 36px;
    border-radius: 100px;
    background: linear-gradient(135deg, var(--accent), var(--accent2));
    color: var(--bg);
    font-family: 'Syne', sans-serif;
    font-size: 15px;
    font-weight: 700;
    text-decoration: none;
    transition: all 0.35s cubic-bezier(0.175, 0.885, 0.32, 1.275);
    position: relative;
    box-shadow: 0 8px 30px rgba(110,231,247,0.3);
  }

  .connect-btn:hover {
    transform: translateY(-4px) scale(1.04);
    box-shadow: 0 16px 50px rgba(110,231,247,0.4);
  }

  /* ── LEARNING ── */
  .learning-list {
    display: flex;
    flex-wrap: wrap;
    gap: 14px;
    margin-top: 16px;
  }

  .learning-item {
    display: flex;
    align-items: center;
    gap: 10px;
    padding: 12px 20px;
    background: var(--card-bg);
    border: 1px solid rgba(255,255,255,0.07);
    border-radius: 12px;
    font-size: 13px;
    color: var(--text);
    transition: all 0.3s;
    backdrop-filter: blur(10px);
  }

  .learning-item:hover {
    border-color: rgba(110,231,247,0.3);
    color: var(--accent);
    transform: translateX(4px);
  }

  .learning-dot {
    width: 8px;
    height: 8px;
    border-radius: 50%;
    background: var(--accent);
    box-shadow: 0 0 10px var(--accent);
    animation: pulse 2s ease-in-out infinite;
  }

  @keyframes pulse {
    0%, 100% { opacity: 1; transform: scale(1); }
    50% { opacity: 0.5; transform: scale(0.8); }
  }

  /* ── NAV ── */
  .nav {
    position: fixed;
    top: 24px;
    left: 50%;
    transform: translateX(-50%);
    z-index: 100;
    background: rgba(5,8,16,0.8);
    backdrop-filter: blur(20px);
    border: 1px solid rgba(255,255,255,0.08);
    border-radius: 100px;
    padding: 10px 24px;
    display: flex;
    gap: 28px;
  }

  .nav a {
    color: var(--muted);
    text-decoration: none;
    font-size: 12px;
    letter-spacing: 1px;
    text-transform: uppercase;
    transition: color 0.2s;
  }

  .nav a:hover { color: var(--accent); }

  /* ── DIVIDER ── */
  .divider {
    height: 1px;
    background: linear-gradient(to right, transparent, rgba(110,231,247,0.2), transparent);
    margin: 20px 0;
  }

  /* ── RESPONSIVE ── */
  @media (max-width: 768px) {
    .nav { display: none; }
    .about-grid { grid-template-columns: 1fr; }
    .projects-grid { grid-template-columns: 1fr; }
    .skills-grid { grid-template-columns: 1fr; }
    .stats-row { grid-template-columns: 1fr 1fr; }
    .connect-card { padding: 40px 24px; }
    .hero { padding: 100px 16px 60px; }
  }

  @media (max-width: 480px) {
    .stats-row { grid-template-columns: 1fr; }
  }

  /* ── CURSOR GLOW ── */
  .cursor-glow {
    position: fixed;
    width: 400px;
    height: 400px;
    border-radius: 50%;
    pointer-events: none;
    z-index: 0;
    background: radial-gradient(circle, rgba(110,231,247,0.04) 0%, transparent 70%);
    transform: translate(-50%, -50%);
    transition: all 0.12s ease;
  }
</style>
</head>
<body>

<!-- Background canvas -->
<canvas id="bgCanvas"></canvas>
<div class="cursor-glow" id="cursorGlow"></div>

<!-- Nav -->
<nav class="nav">
  <a href="#about">About</a>
  <a href="#skills">Skills</a>
  <a href="#projects">Projects</a>
  <a href="#connect">Connect</a>
</nav>

<div class="wrapper">

  <!-- ── HERO ── -->
  <section class="hero" id="home">
    <div class="avatar-ring">
      <div class="avatar-inner">KP</div>
    </div>
    <p class="hero-greeting">👋 Hey, I'm</p>
    <h1 class="hero-name">
      <span>Kaustubh Pawar</span>
    </h1>
    <p class="hero-role">
      Full Stack Developer &nbsp;·&nbsp; <em>Java</em> &nbsp;·&nbsp; <em>React</em> &nbsp;·&nbsp; <em>Django</em> &nbsp;·&nbsp; <em>ML</em>
    </p>
    <div class="hero-badges">
      <span class="badge badge-cyan">🌐 Web Apps</span>
      <span class="badge badge-purple">🤖 Machine Learning</span>
      <span class="badge badge-pink">⚡ REST APIs</span>
      <span class="badge badge-gold">📊 Data Analysis</span>
    </div>
    <div class="scroll-hint">
      <div class="scroll-line"></div>
      SCROLL
    </div>
  </section>

  <div class="divider"></div>

  <!-- ── ABOUT ── -->
  <section class="section" id="about">
    <p class="section-label">// who am i</p>
    <h2 class="section-title">About Me</h2>
    <div class="about-grid">
      <div class="about-card">
        <span class="about-card-icon">🔭</span>
        <h3>What I Build</h3>
        <p>End-to-end web applications — clean, responsive UIs to robust backend APIs. Currently focused on Django REST + React full-stack projects with JWT-based auth and role-based access systems.</p>
      </div>
      <div class="about-card">
        <span class="about-card-icon">🤖</span>
        <h3>ML & Data</h3>
        <p>Building intelligent, data-driven solutions using Scikit-learn, Pandas, and Streamlit. Built a loan approval predictor achieving 89.68% accuracy on 45,000 records.</p>
      </div>
      <div class="about-card">
        <span class="about-card-icon">🌱</span>
        <h3>Always Learning</h3>
        <p>Constantly exploring new technologies — from advanced React patterns to MLOps, Docker, and beyond. Each project is a stepping stone to the next challenge.</p>
      </div>
      <div class="about-card">
        <span class="about-card-icon">💡</span>
        <h3>Philosophy</h3>
        <p>Building practical tools that solve real problems. Clean code, good architecture, and continuous improvement — one project at a time.</p>
      </div>
    </div>
  </section>

  <div class="divider"></div>

  <!-- ── STATS ── -->
  <section class="section">
    <p class="section-label">// by the numbers</p>
    <h2 class="section-title">Stats</h2>
    <div class="stats-row">
      <div class="stat-card" style="--stat-color: var(--accent)">
        <div class="stat-number">8</div>
        <div class="stat-label">Public Repos</div>
      </div>
      <div class="stat-card" style="--stat-color: var(--accent2)">
        <div class="stat-number">5+</div>
        <div class="stat-label">Tech Stacks Used</div>
      </div>
      <div class="stat-card" style="--stat-color: var(--accent3)">
        <div class="stat-number">89%</div>
        <div class="stat-label">ML Model Accuracy</div>
      </div>
      <div class="stat-card" style="--stat-color: var(--gold)">
        <div class="stat-number">45K</div>
        <div class="stat-label">Records Processed</div>
      </div>
    </div>
  </section>

  <div class="divider"></div>

  <!-- ── SKILLS ── -->
  <section class="section" id="skills">
    <p class="section-label">// what i work with</p>
    <h2 class="section-title">Tech Stack</h2>
    <div class="skills-grid">
      <div class="skill-group">
        <div class="skill-group-title">🎨 Frontend</div>
        <div class="skill-pills">
          <span class="pill">React 19</span>
          <span class="pill">Vite</span>
          <span class="pill">JavaScript</span>
          <span class="pill">Tailwind CSS</span>
          <span class="pill">HTML5</span>
          <span class="pill">CSS3</span>
          <span class="pill">Axios</span>
          <span class="pill">React Router</span>
        </div>
      </div>
      <div class="skill-group">
        <div class="skill-group-title">⚙️ Backend</div>
        <div class="skill-pills">
          <span class="pill">Django</span>
          <span class="pill">Django REST</span>
          <span class="pill">Python</span>
          <span class="pill">Java</span>
          <span class="pill">Simple JWT</span>
          <span class="pill">REST APIs</span>
          <span class="pill">django-cors</span>
        </div>
      </div>
      <div class="skill-group">
        <div class="skill-group-title">🤖 ML & Data</div>
        <div class="skill-pills">
          <span class="pill">Scikit-learn</span>
          <span class="pill">Pandas</span>
          <span class="pill">NumPy</span>
          <span class="pill">Streamlit</span>
          <span class="pill">Plotly</span>
          <span class="pill">Matplotlib</span>
          <span class="pill">Seaborn</span>
          <span class="pill">Jupyter</span>
        </div>
      </div>
      <div class="skill-group">
        <div class="skill-group-title">🗄️ Database & Tools</div>
        <div class="skill-pills">
          <span class="pill">SQL</span>
          <span class="pill">SQLite</span>
          <span class="pill">Git</span>
          <span class="pill">GitHub</span>
          <span class="pill">Joblib</span>
          <span class="pill">Kaggle API</span>
        </div>
      </div>
    </div>
  </section>

  <div class="divider"></div>

  <!-- ── PROJECTS ── -->
  <section class="section" id="projects">
    <p class="section-label">// things i've built</p>
    <h2 class="section-title">Featured Projects</h2>
    <div class="projects-grid">

      <a class="project-card" href="https://github.com/kaustubh023/MilkMan" target="_blank" style="--card-accent: linear-gradient(to right, #6ee7f7, #a78bfa)">
        <span class="project-arrow">↗</span>
        <span class="project-emoji">🥛</span>
        <div class="project-title">MilkMan — KP Fresh Dairy</div>
        <div class="project-desc">Full-stack dairy delivery & subscription platform with multi-role access (Customer / Admin / Staff), cart, checkout, and an admin dashboard.</div>
        <div class="project-tags">
          <span class="project-tag">Django REST</span>
          <span class="project-tag">React 19</span>
          <span class="project-tag">JWT Auth</span>
          <span class="project-tag">Tailwind</span>
          <span class="project-tag">SQLite</span>
        </div>
        <div class="project-stat">JavaScript 69.7% · Python 28.5%</div>
      </a>

      <a class="project-card" href="https://github.com/kaustubh023/loan_approval_Project" target="_blank" style="--card-accent: linear-gradient(to right, #a78bfa, #f472b6)">
        <span class="project-arrow">↗</span>
        <span class="project-emoji">🏦</span>
        <div class="project-title">Loan Approval Predictor</div>
        <div class="project-desc">ML-powered loan eligibility system trained on 45,000 records. Features an interactive Streamlit UI with gauge charts and factor analysis.</div>
        <div class="project-tags">
          <span class="project-tag">Scikit-learn</span>
          <span class="project-tag">Streamlit</span>
          <span class="project-tag">Plotly</span>
          <span class="project-tag">Pandas</span>
          <span class="project-tag">Python</span>
        </div>
        <div class="project-stat">✦ 89.68% Accuracy · 45K Records</div>
      </a>

      <a class="project-card" href="https://github.com/kaustubh023/Bizmetric" target="_blank" style="--card-accent: linear-gradient(to right, #f472b6, #fbbf24)">
        <span class="project-arrow">↗</span>
        <span class="project-emoji">📊</span>
        <div class="project-title">Bizmetric</div>
        <div class="project-desc">Business analytics system covering hotel and hostel management with data assessment modules built in Jupyter Notebooks and Python.</div>
        <div class="project-tags">
          <span class="project-tag">Python</span>
          <span class="project-tag">Jupyter</span>
          <span class="project-tag">Analytics</span>
        </div>
        <div class="project-stat">Jupyter 78.1% · Python 21.9%</div>
      </a>

      <a class="project-card" href="https://github.com/kaustubh023/Stock_Analysis_project" target="_blank" style="--card-accent: linear-gradient(to right, #fbbf24, #6ee7f7)">
        <span class="project-arrow">↗</span>
        <span class="project-emoji">📈</span>
        <div class="project-title">Stock Analysis Project</div>
        <div class="project-desc">Data-driven stock market analysis using Python, Pandas and visualization libraries to extract insights from financial data.</div>
        <div class="project-tags">
          <span class="project-tag">Python</span>
          <span class="project-tag">Pandas</span>
          <span class="project-tag">Data Viz</span>
        </div>
        <div class="project-stat">Python · Financial Data</div>
      </a>

      <a class="project-card" href="https://github.com/kaustubh023/ML-Flow-Project-" target="_blank" style="--card-accent: linear-gradient(to right, #6ee7f7, #f472b6)">
        <span class="project-arrow">↗</span>
        <span class="project-emoji">🤖</span>
        <div class="project-title">ML Flow Project</div>
        <div class="project-desc">Machine learning pipeline exploration — end-to-end ML workflows covering data preprocessing, model training, evaluation, and serialization.</div>
        <div class="project-tags">
          <span class="project-tag">Python</span>
          <span class="project-tag">Scikit-learn</span>
          <span class="project-tag">ML Pipeline</span>
        </div>
        <div class="project-stat">Python · ML Workflows</div>
      </a>

    </div>
  </section>

  <div class="divider"></div>

  <!-- ── CURRENTLY LEARNING ── -->
  <section class="section">
    <p class="section-label">// what's next</p>
    <h2 class="section-title">Currently Learning</h2>
    <div class="learning-list">
      <div class="learning-item"><span class="learning-dot"></span>Advanced React Patterns & State Management</div>
      <div class="learning-item"><span class="learning-dot" style="background:var(--accent2);box-shadow:0 0 10px var(--accent2)"></span>MLOps — Model Deployment & Monitoring</div>
      <div class="learning-item"><span class="learning-dot" style="background:var(--accent3);box-shadow:0 0 10px var(--accent3)"></span>Docker & Containerisation</div>
      <div class="learning-item"><span class="learning-dot" style="background:var(--gold);box-shadow:0 0 10px var(--gold)"></span>XGBoost & Random Forest for ML</div>
      <div class="learning-item"><span class="learning-dot"></span>SHAP Values for Explainability</div>
    </div>
  </section>

  <div class="divider"></div>

  <!-- ── CONNECT ── -->
  <section class="connect-section" id="connect">
    <div class="connect-card">
      <h2 class="connect-title">Let's Build Something<br><span style="background: linear-gradient(135deg, var(--accent), var(--accent2)); -webkit-background-clip: text; -webkit-text-fill-color: transparent; background-clip: text;">Together</span></h2>
      <p class="connect-sub">I'm always open to interesting projects, collaborations, or just a good conversation about tech. Feel free to reach out!</p>
      <a class="connect-btn" href="https://github.com/kaustubh023" target="_blank">
        <svg width="18" height="18" viewBox="0 0 24 24" fill="currentColor"><path d="M12 0c-6.626 0-12 5.373-12 12 0 5.302 3.438 9.8 8.207 11.387.599.111.793-.261.793-.577v-2.234c-3.338.726-4.033-1.416-4.033-1.416-.546-1.387-1.333-1.756-1.333-1.756-1.089-.745.083-.729.083-.729 1.205.084 1.839 1.237 1.839 1.237 1.07 1.834 2.807 1.304 3.492.997.107-.775.418-1.305.762-1.604-2.665-.305-5.467-1.334-5.467-5.931 0-1.311.469-2.381 1.236-3.221-.124-.303-.535-1.524.117-3.176 0 0 1.008-.322 3.301 1.23.957-.266 1.983-.399 3.003-.404 1.02.005 2.047.138 3.006.404 2.291-1.552 3.297-1.23 3.297-1.23.653 1.653.242 2.874.118 3.176.77.84 1.235 1.911 1.235 3.221 0 4.609-2.807 5.624-5.479 5.921.43.372.823 1.102.823 2.222v3.293c0 .319.192.694.801.576 4.765-1.589 8.199-6.086 8.199-11.386 0-6.627-5.373-12-12-12z"/></svg>
        View GitHub Profile
      </a>
    </div>
  </section>

  <div class="divider"></div>
  <p style="text-align:center; color: var(--muted); font-size: 12px; padding: 20px 0; letter-spacing: 1px;">
    Built with ❤️ by Kaustubh Pawar &nbsp;·&nbsp; <span style="color: var(--accent)">kaustubh023</span>
  </p>

</div>

<script>
// ── PARTICLE CANVAS ──
const canvas = document.getElementById('bgCanvas');
const ctx = canvas.getContext('2d');
let particles = [];
let W, H;

function resize() {
  W = canvas.width = window.innerWidth;
  H = canvas.height = window.innerHeight;
}
resize();
window.addEventListener('resize', resize);

class Particle {
  constructor() { this.reset(); }
  reset() {
    this.x = Math.random() * W;
    this.y = Math.random() * H;
    this.r = Math.random() * 1.5 + 0.3;
    this.vx = (Math.random() - 0.5) * 0.3;
    this.vy = (Math.random() - 0.5) * 0.3;
    this.alpha = Math.random() * 0.5 + 0.1;
    this.color = Math.random() < 0.5 ? '110,231,247' : '167,139,250';
  }
  update() {
    this.x += this.vx;
    this.y += this.vy;
    if (this.x < 0 || this.x > W || this.y < 0 || this.y > H) this.reset();
  }
  draw() {
    ctx.beginPath();
    ctx.arc(this.x, this.y, this.r, 0, Math.PI * 2);
    ctx.fillStyle = `rgba(${this.color},${this.alpha})`;
    ctx.fill();
  }
}

for (let i = 0; i < 120; i++) particles.push(new Particle());

function connectParticles() {
  for (let i = 0; i < particles.length; i++) {
    for (let j = i + 1; j < particles.length; j++) {
      const dx = particles[i].x - particles[j].x;
      const dy = particles[i].y - particles[j].y;
      const dist = Math.sqrt(dx*dx + dy*dy);
      if (dist < 100) {
        ctx.beginPath();
        ctx.moveTo(particles[i].x, particles[i].y);
        ctx.lineTo(particles[j].x, particles[j].y);
        ctx.strokeStyle = `rgba(110,231,247,${0.06 * (1 - dist/100)})`;
        ctx.lineWidth = 0.5;
        ctx.stroke();
      }
    }
  }
}

function animate() {
  ctx.clearRect(0, 0, W, H);
  particles.forEach(p => { p.update(); p.draw(); });
  connectParticles();
  requestAnimationFrame(animate);
}
animate();

// ── CURSOR GLOW ──
const glow = document.getElementById('cursorGlow');
window.addEventListener('mousemove', e => {
  glow.style.left = e.clientX + 'px';
  glow.style.top = e.clientY + 'px';
});

// ── 3D CARD TILT ──
document.querySelectorAll('.project-card, .about-card, .skill-group, .stat-card').forEach(card => {
  card.addEventListener('mousemove', e => {
    const rect = card.getBoundingClientRect();
    const x = (e.clientX - rect.left) / rect.width;
    const y = (e.clientY - rect.top) / rect.height;
    const tiltX = (y - 0.5) * 10;
    const tiltY = (x - 0.5) * -10;
    card.style.transform = `translateY(-8px) rotateX(${tiltX}deg) rotateY(${tiltY}deg)`;
    card.style.setProperty('--mx', `${x * 100}%`);
    card.style.setProperty('--my', `${y * 100}%`);
  });
  card.addEventListener('mouseleave', () => {
    card.style.transform = '';
  });
});

// ── SCROLL REVEAL ──
const observer = new IntersectionObserver(entries => {
  entries.forEach(entry => {
    if (entry.isIntersecting) {
      entry.target.style.opacity = '1';
      entry.target.style.transform = 'translateY(0)';
    }
  });
}, { threshold: 0.1 });

document.querySelectorAll('.about-card, .skill-group, .project-card, .stat-card, .learning-item').forEach((el, i) => {
  el.style.opacity = '0';
  el.style.transform = 'translateY(30px)';
  el.style.transition = `opacity 0.6s ${i * 0.07}s, transform 0.6s ${i * 0.07}s`;
  observer.observe(el);
});
</script>
</body>
</html>
