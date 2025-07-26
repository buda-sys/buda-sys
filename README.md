


<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Buda-sys | Ethical Hacking</title>
  <link href="https://fonts.googleapis.com/css2?family=Share+Tech+Mono&display=swap" rel="stylesheet"/>
  <style>
    body {
      background-color: #0d0d0d;
      color: #33ff33;
      font-family: 'Share Tech Mono', monospace;
      margin: 0;
      padding: 0;
    }
    header {
      background: #111;
      padding: 2rem;
      text-align: center;
      border-bottom: 2px solid #33ff33;
    }
    header h1 {
      margin: 0;
      font-size: 2.5rem;
    }
    nav {
      text-align: center;
      padding: 1rem;
    }
    nav a {
      margin: 0 1rem;
      text-decoration: none;
      color: #33ff33;
      border-bottom: 1px dashed transparent;
    }
    nav a:hover {
      border-color: #33ff33;
    }
    section {
      padding: 2rem;
      max-width: 800px;
      margin: auto;
    }
    h2 {
      border-bottom: 1px dashed #33ff33;
      padding-bottom: 0.5rem;
    }
    ul {
      list-style: square;
    }
    footer {
      text-align: center;
      padding: 1rem;
      border-top: 1px dashed #33ff33;
      color: #888;
      font-size: 0.9rem;
    }
    .highlight {
      color: #00ffcc;
    }
    #terminal {
      background-color: #000;
      color: #33ff33;
      font-size: 1.2rem;
      padding: 1rem;
      margin: 2rem auto;
      max-width: 800px;
      border: 1px solid #33ff33;
      white-space: pre-wrap;
      min-height: 100px;
    }
    .cursor {
      display: inline-block;
      width: 10px;
      background-color: #33ff33;
      animation: blink 0.8s infinite;
    }
    @keyframes blink {
      0%, 100% { opacity: 1; }
      50% { opacity: 0; }
    }
  </style>
</head>
<body>
  <header>
    <h1>🧠 Buda-sys</h1>
    <p>Ethical Hacking | Red Team | Malware | Ingeniería Inversa</p>
  </header>

  <div id="terminal"><span id="typed-text"></span><span class="cursor"></span></div>

  <nav>
    <a href="#about">Sobre mí</a>
    <a href="#projects">Proyectos</a>
    <a href="#contact">Contacto</a>
  </nav>

  <section id="about">
    <h2>💀 Sobre mí</h2>
    <p>Soy <span class="highlight">Buda-sys</span>, un apasionado del mundo oscuro (y ético) de la ciberseguridad.</p>
    <ul>
      <li>Estudiante de Licenciatura en Ciberseguridad</li>
      <li>Me encanta el Red Team, análisis de malware, ingeniería inversa y hardening</li>
      <li>Aprendiendo todos los días de forma autodidacta</li>
    </ul>
  </section>

  <section id="projects">
    <h2>📁 Proyectos y CTFs</h2>
    <ul>
      <li><strong>CTF:</strong> Write-ups de retos resueltos (en progreso)</li>
      <li><strong>Herramientas:</strong> Scripts personalizados para pentesting</li>
      <li><strong>Documentación:</strong> Notas y técnicas sobre malware y reversing</li>
    </ul>
  </section>

  <section id="contact">
    <h2>📡 Contacto</h2>
    <ul>
      <li>📱 Telegram: <a href="https://t.me/buda_sys" target="_blank">@buda_sys</a></li>
      <li>🎥 TikTok: <a href="https://www.tiktok.com/@buda_sys" target="_blank">@buda_sys</a></li>
      <li>📧 Email: buda.sys@protonmail.com</li>
    </ul>
  </section>

  <footer>
    Hecho con 💻 por Buda-sys — <em>“Hack the planet... ethically”</em>
  </footer>

  <script>
    const text = `> Iniciando conexión con Buda-sys...\n> Cargando perfil cibernético...\n> Red Team | Malware | Ingeniería Inversa\n> Bienvenido al mundo del hacking ético.\n`;
    const typedText = document.getElementById('typed-text');
    let i = 0;

    function type() {
      if (i < text.length) {
        typedText.textContent += text.charAt(i);
        i++;
        setTimeout(type, 40);
      }
    }

    window.onload = type;
  </script>
</body>
</html>



