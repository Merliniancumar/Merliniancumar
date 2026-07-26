<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Merlín Ian Cumar Vinci — Portfolio</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link href="https://fonts.googleapis.com/css2?family=JetBrains+Mono:ital,wght@0,400;0,500;0,700;0,800;1,400&family=Inter:wght@400;500;600;700&display=swap" rel="stylesheet">
<style>
  :root{
    --bg: #14141c;
    --bg-elevated: #1b1b26;
    --sidebar: #101017;
    --border: #2a2a38;
    --text: #d6d6e8;
    --text-dim: #7d7d99;
    --blue: #7aa2f7;
    --green: #9ece6a;
    --purple: #bb9af7;
    --orange: #e0af68;
    --red: #f7768e;
    --font-mono: 'JetBrains Mono', monospace;
    --font-sans: 'Inter', sans-serif;
  }

  *{ box-sizing: border-box; margin:0; padding:0; }

  body{
    background: var(--bg);
    color: var(--text);
    font-family: var(--font-sans);
    line-height: 1.6;
    -webkit-font-smoothing: antialiased;
  }

  a{ color: var(--blue); text-decoration: none; }
  a:hover{ text-decoration: underline; }
  a:focus-visible, button:focus-visible{ outline: 2px solid var(--blue); outline-offset: 2px; }

  /* ---- Title bar (mimics an editor window) ---- */
  .titlebar{
    background: var(--sidebar);
    border-bottom: 1px solid var(--border);
    padding: 10px 16px;
    display:flex;
    align-items:center;
    gap:10px;
    position: sticky;
    top:0;
    z-index: 10;
  }
  .dots{ display:flex; gap:6px; }
  .dots span{ width:11px; height:11px; border-radius:50%; display:block; }
  .dots span:nth-child(1){ background:#f7768e; }
  .dots span:nth-child(2){ background:#e0af68; }
  .dots span:nth-child(3){ background:#9ece6a; }
  .titlebar-name{
    font-family: var(--font-mono);
    font-size: 0.8rem;
    color: var(--text-dim);
    margin-left: 6px;
  }

  /* ---- Layout: sidebar + main ---- */
  .app{ display:flex; min-height: calc(100vh - 41px); }

  .sidebar{
    width: 230px;
    flex-shrink: 0;
    background: var(--sidebar);
    border-right: 1px solid var(--border);
    padding: 20px 0;
  }
  .sidebar-heading{
    font-family: var(--font-mono);
    font-size: 0.7rem;
    letter-spacing: 0.08em;
    color: var(--text-dim);
    text-transform: uppercase;
    padding: 0 20px 10px;
  }
  .filetree a{
    display:flex;
    align-items:center;
    gap:8px;
    font-family: var(--font-mono);
    font-size: 0.85rem;
    color: var(--text-dim);
    padding: 6px 20px;
    border-left: 2px solid transparent;
  }
  .filetree a:hover, .filetree a.active{
    color: var(--text);
    background: rgba(122,162,247,0.08);
    border-left-color: var(--blue);
    text-decoration:none;
  }
  .filetree .ext{ color: var(--text-dim); }

  main{ flex:1; min-width:0; }

  /* ---- Tabs ---- */
  .tabs{
    display:flex;
    background: var(--bg-elevated);
    border-bottom: 1px solid var(--border);
    overflow-x:auto;
  }
  .tabs .tab{
    font-family: var(--font-mono);
    font-size: 0.8rem;
    padding: 10px 18px;
    color: var(--text-dim);
    border-right: 1px solid var(--border);
    white-space:nowrap;
  }
  .tabs .tab.current{ color: var(--text); background: var(--bg); }

  section{
    padding: 56px 48px;
    max-width: 780px;
    border-bottom: 1px solid var(--border);
  }
  section:last-child{ border-bottom:none; }

  .comment{ color: var(--text-dim); font-family: var(--font-mono); font-size: 0.85rem; }
  .keyword{ color: var(--purple); font-family: var(--font-mono); }
  .string{ color: var(--green); font-family: var(--font-mono); }
  .func{ color: var(--blue); font-family: var(--font-mono); }

  h1{
    font-family: var(--font-mono);
    font-weight: 800;
    font-size: clamp(1.8rem, 4vw, 2.6rem);
    color: var(--text);
    margin: 6px 0 4px;
  }
  h1 .dim{ color: var(--text-dim); font-weight: 500; }

  .role{
    font-family: var(--font-mono);
    color: var(--orange);
    font-size: 1rem;
    margin-bottom: 22px;
  }

  h2{
    font-family: var(--font-mono);
    font-size: 0.75rem;
    text-transform: uppercase;
    letter-spacing: 0.1em;
    color: var(--text-dim);
    margin-bottom: 18px;
  }
  h2::before{ content: "// "; color: var(--purple); }

  p.lead{ font-size: 1.02rem; color: var(--text); max-width: 60ch; }

  .badge-row{ display:flex; flex-wrap:wrap; gap:8px; margin-top: 8px;}
  .badge{
    font-family: var(--font-mono);
    font-size: 0.78rem;
    padding: 5px 10px;
    border-radius: 5px;
    background: var(--bg-elevated);
    border: 1px solid var(--border);
    color: var(--text);
  }

  .group-label{
    font-family: var(--font-mono);
    font-size: 0.72rem;
    color: var(--text-dim);
    margin: 22px 0 8px;
  }
  .group-label:first-child{ margin-top: 0; }

  .card{
    background: var(--bg-elevated);
    border: 1px solid var(--border);
    border-radius: 8px;
    padding: 20px 22px;
    margin-bottom: 16px;
  }
  .card h3{
    font-family: var(--font-mono);
    font-size: 1rem;
    color: var(--text);
    margin-bottom: 6px;
  }
  .card p{ color: var(--text-dim); font-size: 0.92rem; }
  .card .tag-row{ margin-top: 10px; }

  .placeholder{
    border: 1px dashed var(--border);
    color: var(--text-dim);
    font-family: var(--font-mono);
    font-size: 0.85rem;
    padding: 18px 20px;
    border-radius: 8px;
  }

  .links-grid{ display:flex; flex-direction:column; gap: 14px; }
  .link-item{
    display:flex;
    align-items:center;
    gap: 12px;
    font-family: var(--font-mono);
    font-size: 0.95rem;
  }
  .link-item .tag{ color: var(--text-dim); width: 92px; flex-shrink:0; }

  footer{
    padding: 30px 48px;
    font-family: var(--font-mono);
    font-size: 0.78rem;
    color: var(--text-dim);
  }

  @media (max-width: 720px){
    .app{ flex-direction: column; }
    .sidebar{ width: 100%; border-right:none; border-bottom: 1px solid var(--border); padding: 12px 0; }
    .filetree{ display:flex; overflow-x:auto; }
    .filetree a{ padding: 8px 14px; border-left:none; border-bottom: 2px solid transparent; }
    .filetree a:hover, .filetree a.active{ border-left:none; border-bottom-color: var(--blue); }
    .sidebar-heading{ display:none; }
    section{ padding: 40px 22px; }
    footer{ padding: 24px 22px; }
  }

  @media (prefers-reduced-motion: reduce){
    *{ scroll-behavior: auto !important; }
  }

  html{ scroll-behavior: smooth; }
</style>
</head>
<body>

  <div class="titlebar">
    <div class="dots"><span></span><span></span><span></span></div>
    <span class="titlebar-name">merlin-cumar-vinci — portfolio</span>
  </div>

  <div class="app">
    <nav class="sidebar" aria-label="Navegación de secciones">
      <div class="sidebar-heading">Explorador</div>
      <div class="filetree">
        <a href="#about">about<span class="ext">.md</span></a>
        <a href="#stack">stack<span class="ext">.json</span></a>
        <a href="#projects">proyectos<span class="ext">/</span></a>
        <a href="#contact">contacto<span class="ext">.txt</span></a>
      </div>
    </nav>

    <main>
      <div class="tabs">
        <div class="tab current">about.md</div>
        <div class="tab">stack.json</div>
        <div class="tab">proyectos/</div>
        <div class="tab">contacto.txt</div>
      </div>

      <section id="about">
        <div class="comment">/* presentación */</div>
        <h1><span class="keyword">const</span> dev <span class="dim">=</span> <span class="func">"Merlín Ian Cumar Vinci"</span></h1>
        <p class="role">&gt; Estudiante de Programación Full Stack</p>
        <p class="lead">
          Curso la Tecnicatura Universitaria de Pregrado en Programación Full Stack
          en la sede regional Bernardo Houssay de Capilla del Monte, Córdoba, Argentina.
          Me interesa construir aplicaciones web de punta a punta: desde la interfaz
          que ve la gente hasta la base de datos que sostiene todo por detrás.
        </p>
      </section>

      <section id="stack">
        <h2>Stack</h2>

        <div class="group-label">Lenguajes</div>
        <div class="badge-row">
          <span class="badge">HTML5</span>
          <span class="badge">CSS3</span>
          <span class="badge">JavaScript</span>
          <span class="badge">Python</span>
          <span class="badge">SQL</span>
          <span class="badge">PostgreSQL</span>
        </div>

        <div class="group-label">Herramientas</div>
        <div class="badge-row">
          <span class="badge">Visual Studio Code</span>
          <span class="badge">Git</span>
          <span class="badge">GitHub</span>
          <span class="badge">GitHub Pages</span>
          <span class="badge">PSeInt</span>
        </div>

        <div class="group-label">Áreas de interés</div>
        <div class="badge-row">
          <span class="badge">Full Stack</span>
          <span class="badge">Frontend</span>
          <span class="badge">Backend</span>
          <span class="badge">Bases de datos</span>
          <span class="badge">Diseño UI</span>
          <span class="badge">Apps web</span>
        </div>
      </section>

    
      <section id="contact">
        <h2>Contacto</h2>
        <div class="links-grid">
          <div class="link-item"><span class="tag">email</span> <a href="mailto:cumarvincimerlinian@gmail.com">cumarvincimerlinian@gmail.com</a></div>
          <div class="link-item"><span class="tag">linkedin</span> <a href="https://www.linkedin.com/in/merl%C3%ADn-ian-cumar-vinci-883287391/" target="_blank" rel="noopener">linkedin.com/in/merlín-ian-cumar-vinci-883287391</a></div>
          <div class="link-item"><span class="tag">github</span> <a href="https://github.com/TU-USUARIO-GITHUB" target="_blank" rel="noopener">github.com/TU-USUARIO-GITHUB</a></div>
        </div>
      </section>

      <footer>
        // hecho por Merlín Ian Cumar Vinci — Bernardo Houssay, Capilla del Monte
      </footer>
    </main>
  </div>

</body>
</html>
