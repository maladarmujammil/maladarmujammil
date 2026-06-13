<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=yes">
  <title>Mujammil Maladar | DevSecOps & Embedded Wizard</title>
  <!-- Google Fonts + Font Awesome -->
  <link href="https://fonts.googleapis.com/css2?family=Inter:opsz,wght@14..32,300;14..32,400;14..32,600;14..32,700;14..32,800&display=swap" rel="stylesheet">
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0-beta3/css/all.min.css">
  <style>
    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
    }

    body {
      font-family: 'Inter', sans-serif;
      background: #0a0c12;
      color: #eef5ff;
      line-height: 1.5;
      overflow-x: hidden;
    }

    /* animated gradient background + noise */
    .bg-gradient {
      position: fixed;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      z-index: -2;
      background: radial-gradient(circle at 20% 30%, #0b1120, #010101);
    }

    canvas#particle-canvas {
      position: fixed;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      z-index: -1;
      pointer-events: none;
      opacity: 0.45;
    }

    /* glass morphism containers */
    .glass-card {
      background: rgba(15, 25, 45, 0.55);
      backdrop-filter: blur(12px);
      border-radius: 2rem;
      border: 1px solid rgba(0, 255, 255, 0.2);
      box-shadow: 0 20px 35px -12px rgba(0, 0, 0, 0.5), 0 0 0 0.5px rgba(0, 255, 255, 0.1) inset;
      transition: transform 0.25s ease, box-shadow 0.3s ease;
    }

    .glass-card:hover {
      transform: translateY(-5px);
      box-shadow: 0 25px 40px -12px rgba(0, 255, 255, 0.2), 0 0 0 1px rgba(0, 255, 255, 0.4) inset;
      border-color: rgba(0, 255, 255, 0.5);
    }

    .container {
      max-width: 1280px;
      margin: 0 auto;
      padding: 1.5rem 2rem;
      position: relative;
      z-index: 2;
    }

    /* Typography */
    h1 {
      font-size: 3.5rem;
      font-weight: 800;
      background: linear-gradient(135deg, #FFFFFF, #7ec8ff, #2dd4bf);
      background-clip: text;
      -webkit-background-clip: text;
      color: transparent;
      letter-spacing: -0.02em;
    }

    .glow-text {
      text-shadow: 0 0 6px rgba(0, 255, 255, 0.4);
    }

    .section-title {
      font-size: 2rem;
      font-weight: 700;
      margin-bottom: 1.5rem;
      display: inline-block;
      background: linear-gradient(120deg, #b0f3ff, #2dd4bf);
      background-clip: text;
      -webkit-background-clip: text;
      color: transparent;
      border-left: 4px solid #2dd4bf;
      padding-left: 1rem;
    }

    .badge {
      background: rgba(45, 212, 191, 0.15);
      backdrop-filter: blur(4px);
      padding: 0.3rem 0.9rem;
      border-radius: 40px;
      font-size: 0.75rem;
      font-weight: 500;
      border: 1px solid rgba(45, 212, 191, 0.5);
      letter-spacing: 0.3px;
    }

    /* skill tags */
    .skill-tag {
      background: rgba(20, 30, 55, 0.7);
      border-radius: 40px;
      padding: 0.5rem 1.2rem;
      font-size: 0.85rem;
      font-weight: 500;
      transition: all 0.2s;
      border: 1px solid rgba(100, 210, 255, 0.2);
      backdrop-filter: blur(4px);
    }

    .skill-tag i {
      margin-right: 0.5rem;
      color: #2dd4bf;
    }

    .skill-tag:hover {
      background: rgba(45, 212, 191, 0.2);
      border-color: #2dd4bf;
      transform: scale(1.02);
    }

    /* Project cards */
    .project-card {
      background: rgba(10, 20, 35, 0.6);
      border-radius: 1.5rem;
      padding: 1.5rem;
      transition: all 0.3s cubic-bezier(0.2, 0.9, 0.4, 1.1);
      border: 1px solid rgba(0, 255, 255, 0.15);
      height: 100%;
    }

    .project-card:hover {
      border-color: #2dd4bf;
      background: rgba(20, 35, 60, 0.65);
      box-shadow: 0 15px 30px -12px rgba(0, 255, 200, 0.2);
    }

    .github-stats img {
      border-radius: 16px;
      transition: all 0.2s;
    }

    .btn-cyber {
      background: rgba(0, 0, 0, 0.5);
      border: 1px solid #2dd4bf;
      border-radius: 60px;
      padding: 0.6rem 1.4rem;
      font-weight: 600;
      transition: 0.25s;
      color: #ccf4ff;
      display: inline-flex;
      align-items: center;
      gap: 0.6rem;
    }

    .btn-cyber:hover {
      background: #2dd4bf20;
      box-shadow: 0 0 12px rgba(45, 212, 191, 0.3);
      color: white;
      transform: translateY(-2px);
    }

    /* grid & flex */
    .skills-grid {
      display: flex;
      flex-wrap: wrap;
      gap: 0.8rem;
      margin-top: 1rem;
    }

    .project-grid {
      display: grid;
      grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
      gap: 1.8rem;
    }

    .flex-between {
      display: flex;
      justify-content: space-between;
      flex-wrap: wrap;
      align-items: center;
    }

    /* icons & footer */
    .social-links a {
      color: #b4f0ff;
      font-size: 1.8rem;
      transition: 0.2s;
      margin: 0 0.5rem;
    }

    .social-links a:hover {
      color: #2dd4bf;
      transform: scale(1.1);
    }

    hr {
      border-color: rgba(45, 212, 191, 0.2);
      margin: 1rem 0;
    }

    @media (max-width: 780px) {
      .container {
        padding: 1rem 1.2rem;
      }
      h1 {
        font-size: 2.5rem;
      }
      .section-title {
        font-size: 1.6rem;
      }
    }

    /* scroll reveal animation */
    .reveal {
      opacity: 0;
      transform: translateY(25px);
      transition: opacity 0.7s ease, transform 0.6s ease;
    }
    .reveal.visible {
      opacity: 1;
      transform: translateY(0);
    }
  </style>
</head>
<body>

<div class="bg-gradient"></div>
<canvas id="particle-canvas"></canvas>

<main class="container">
  <!-- Hero Section -->
  <div class="reveal">
    <div class="glass-card" style="padding: 2rem 2rem; margin-bottom: 2rem;">
      <div class="flex-between" style="gap: 1rem;">
        <div>
          <div class="badge" style="margin-bottom: 1rem; display: inline-block;">
            <i class="fas fa-code"></i>  ENGINEER · BUILDER · BREAKER
          </div>
          <h1>Mujammil Maladar</h1>
          <div style="font-size: 1.2rem; font-weight: 500; margin: 0.8rem 0 0.5rem; color: #b2f0ff;">
            <i class="fas fa-bolt"></i> embedded · cybersecurity · full-stack vibe
          </div>
          <div style="display: flex; flex-wrap: wrap; gap: 1rem; margin-top: 1rem;">
            <span><i class="fas fa-phone-alt"></i> +91-7349208106</span>
            <span><i class="fas fa-envelope"></i> maladarmujammil@gmail.com</span>
            <span><i class="fab fa-github"></i> maladarmujammil</span>
            <span><i class="fab fa-linkedin"></i> mujammil-maladar</span>
          </div>
        </div>
        <div class="social-links">
          <a href="https://github.com/maladarmujammil" target="_blank"><i class="fab fa-github"></i></a>
          <a href="https://linkedin.com/in/mujammil-maladar" target="_blank"><i class="fab fa-linkedin-in"></i></a>
        </div>
      </div>
      <hr>
      <p style="font-size: 1.05rem; max-width: 85%;">
        ⚡ Electronics & Communication engineer fueled by <span class="glow-text">cybersecurity, embedded systems, and web dev</span>. 
        I craft smart automation, gesture-controlled magic, and sustainable tech. Obsessed with solving real-world problems using code & circuits.
      </p>
    </div>
  </div>

  <!-- Internship Experience + Mini Objective -->
  <div class="reveal" style="margin-bottom: 2.5rem;">
    <div class="glass-card" style="padding: 1.8rem;">
      <div style="display: flex; gap: 0.8rem; align-items: center; margin-bottom: 1rem;">
        <i class="fas fa-shield-haltered" style="font-size: 2rem; color: #2dd4bf;"></i>
        <h2 class="section-title" style="margin-bottom: 0;">cyber forge experience</h2>
      </div>
      <div style="display: flex; flex-wrap: wrap; justify-content: space-between; align-items: baseline;">
        <div>
          <h3 style="font-weight: 700; font-size: 1.4rem;">Cybersecurity Intern · Supraja Technologies</h3>
          <p style="color: #bbd4ff;"><i class="fas fa-globe"></i> Remote | Hands-on ethical hacking, network security, threat intelligence</p>
        </div>
        <div class="badge"><i class="fas fa-bolt"></i> vulnerability assessment</div>
      </div>
      <p style="margin-top: 1rem;">Performed deep-dive into attack surfaces, security protocols, and real-time vulnerability scanning. Sharpened offensive & defensive mindset — automating security checks and understanding intrusion patterns.</p>
    </div>
  </div>

  <!-- Featured Projects - THAGADA WALA CARD SECTION -->
  <div class="reveal" style="margin-bottom: 2.5rem;">
    <div style="display: flex; align-items: center; gap: 1rem; margin-bottom: 1rem;">
      <i class="fas fa-microchip" style="font-size: 1.8rem; color:#2dd4bf"></i>
      <h2 class="section-title" style="margin-bottom: 0;">⚡ flagship projects</h2>
    </div>
    <div class="project-grid">
      <!-- Milk Quality Billing System -->
      <div class="project-card">
        <div style="display: flex; justify-content: space-between;">
          <i class="fas fa-flask" style="font-size: 2rem; color: #2dd4bf;"></i>
          <span class="badge">Embedded · IoT</span>
        </div>
        <h3 style="font-size: 1.5rem; margin: 0.7rem 0 0.5rem;">Milk Quality Auto Billing</h3>
        <p style="font-size: 0.9rem; opacity: 0.85;">Smart sensor system measuring fat, SNF, water adulteration → real-time billing based on quality grade. Embedded C, sensor fusion, LCD interface. Zero manual errors.</p>
        <div class="skills-grid" style="margin-top: 1rem;">
          <span class="skill-tag" style="padding: 0.2rem 0.8rem;">Embedded C</span>
          <span class="skill-tag" style="padding: 0.2rem 0.8rem;">Microcontroller</span>
          <span class="skill-tag" style="padding: 0.2rem 0.8rem;">Keil uVision</span>
        </div>
        <div style="margin-top: 1rem;">
          <a href="#" class="btn-cyber" style="font-size: 0.8rem;" target="_blank"><i class="fab fa-github"></i> Code Vault</a>
        </div>
      </div>
      <!-- Eco-Friendly Shopping -->
      <div class="project-card">
        <div style="display: flex; justify-content: space-between;">
          <i class="fas fa-leaf" style="font-size: 2rem; color: #2dd4bf;"></i>
          <span class="badge">Web · Green Tech</span>
        </div>
        <h3 style="font-size: 1.5rem; margin: 0.7rem 0 0.5rem;">Eco-Friendly Shopping Hub</h3>
        <p style="font-size: 0.9rem; opacity: 0.85;">Responsive platform promoting sustainable products, interactive UI, product categories, and eco-lifestyle. HTML5, CSS3, vanilla JS magic.</p>
        <div class="skills-grid" style="margin-top: 1rem;">
          <span class="skill-tag">HTML/CSS</span>
          <span class="skill-tag">JavaScript</span>
          <span class="skill-tag">Responsive</span>
        </div>
        <div style="margin-top: 1rem;">
          <a href="#" class="btn-cyber" style="font-size: 0.8rem;"><i class="fab fa-github"></i> Live Demo</a>
        </div>
      </div>
      <!-- Hand Gesture LED System -->
      <div class="project-card">
        <div style="display: flex; justify-content: space-between;">
          <i class="fas fa-hand-peace" style="font-size: 2rem; color: #2dd4bf;"></i>
          <span class="badge">CV · Automation</span>
        </div>
        <h3 style="font-size: 1.5rem; margin: 0.7rem 0 0.5rem;">Gesture Controlled LED Matrix</h3>
        <p style="font-size: 0.9rem; opacity: 0.85;">Computer vision + microcontroller synergy: real-time hand gesture recognition to control LED patterns. MediaPipe + embedded integration.</p>
        <div class="skills-grid" style="margin-top: 1rem;">
          <span class="skill-tag">Python</span>
          <span class="skill-tag">OpenCV</span>
          <span class="skill-tag">Embedded</span>
        </div>
        <div style="margin-top: 1rem;">
          <a href="#" class="btn-cyber" style="font-size: 0.8rem;"><i class="fab fa-github"></i> Gesture repo</a>
        </div>
      </div>
    </div>
  </div>

  <!-- Skills Section : Core & dev tools -->
  <div class="reveal" style="margin-bottom: 2rem;">
    <div class="glass-card" style="padding: 1.8rem;">
      <div style="display: flex; gap: 0.8rem; align-items: center; margin-bottom: 1rem;">
        <i class="fas fa-cogs" style="font-size: 1.8rem; color:#2dd4bf"></i>
        <h2 class="section-title" style="margin-bottom: 0;">arsenal & toolchain</h2>
      </div>
      <div style="display: grid; grid-template-columns: repeat(auto-fit, minmax(240px,1fr)); gap: 1.2rem;">
        <div>
          <h4 style="margin-bottom: 0.7rem;"><i class="fas fa-microchip"></i> Core Engineering</h4>
          <div class="skills-grid">
            <span class="skill-tag">Embedded Systems</span>
            <span class="skill-tag">Electronics</span>
            <span class="skill-tag">Matlab</span>
            <span class="skill-tag">Cadence Virtuoso</span>
            <span class="skill-tag">Keil uVision</span>
          </div>
        </div>
        <div>
          <h4 style="margin-bottom: 0.7rem;"><i class="fas fa-code"></i> Languages & OOP</h4>
          <div class="skills-grid">
            <span class="skill-tag">Python</span>
            <span class="skill-tag">C / C++</span>
            <span class="skill-tag">Java (OOP)</span>
            <span class="skill-tag">JavaScript</span>
          </div>
        </div>
        <div>
          <h4 style="margin-bottom: 0.7rem;"><i class="fas fa-laptop-code"></i> DevSecOps Tools</h4>
          <div class="skills-grid">
            <span class="skill-tag">VS Code</span>
            <span class="skill-tag">Arduino IDE</span>
            <span class="skill-tag">Kali Linux</span>
            <span class="skill-tag">Burp Suite</span>
            <span class="skill-tag">Git/GitHub</span>
          </div>
        </div>
      </div>
      <div style="margin-top: 1.5rem;">
        <h4><i class="fas fa-users"></i> Soft skills : Adaptability · Problem Solving · Time Wizard · Team Synergy</h4>
      </div>
    </div>
  </div>

  <!-- Certifications & Achievements - badges area -->
  <div class="reveal" style="margin-bottom: 2rem;">
    <div class="glass-card" style="padding: 1.8rem;">
      <div style="display: flex; flex-wrap: wrap; gap: 2rem; justify-content: space-between;">
        <div style="flex: 1;">
          <h3><i class="fas fa-certificate"></i> certifications</h3>
          <ul style="margin-top: 1rem; list-style: none;">
            <li style="margin-bottom: 12px;">🔖 <strong>Cloud Computing</strong> – NPTEL</li>
            <li style="margin-bottom: 12px;">🔖 <strong>Quantitative Aptitude & Professional Skills</strong> – Z Skills Up</li>
            <li style="margin-bottom: 12px;">🔖 <strong>Machine Learning</strong> – Coursera</li>
            <li style="margin-bottom: 12px;">🔖 <strong>Supraja Hackathon (Level-1)</strong> – Completion</li>
          </ul>
        </div>
        <div style="flex: 1;">
          <h3><i class="fas fa-trophy"></i> achievements & footprints</h3>
          <ul style="margin-top: 1rem; list-style: none;">
            <li><i class="fas fa-microchip"></i> 3-day SDP: Embedded System & Product Design</li>
            <li><i class="fas fa-shield-alt"></i> 5-day SDP: Cybersecurity hands-on</li>
            <li><i class="fas fa-leaf"></i> BEC IEEE – Code For Green 12hrs Hackathon</li>
            <li><i class="fas fa-chart-line"></i> 10-day SDP: Linear Data Structures using C++</li>
            <li><i class="fas fa-robot"></i> Volunteer: Dept Level Roborace · Avishkaar Tech Fest</li>
          </ul>
        </div>
      </div>
    </div>
  </div>

  <!-- GITHUB STATS + DYNAMIC STREAK - THAGADA WALA INTEGRATION -->
  <div class="reveal" style="margin-bottom: 2rem;">
    <div class="glass-card" style="padding: 1.8rem; text-align: center;">
      <div style="display: flex; justify-content: center; gap: 1rem; align-items: baseline;">
        <i class="fab fa-github" style="font-size: 2rem;"></i>
        <h2 class="section-title" style="margin-bottom: 0;">dev pulse · GitHub chronicles</h2>
      </div>
      <div class="github-stats" style="display: flex; flex-wrap: wrap; justify-content: center; gap: 1.2rem; margin-top: 1.5rem;">
        <a href="https://github.com/maladarmujammil" target="_blank">
          <img src="https://github-readme-stats.vercel.app/api?username=maladarmujammil&show_icons=true&count_private=true&hide_border=true&bg_color=0a0c12&title_color=2dd4bf&icon_color=2dd4bf&text_color=cbd5e6&ring_color=2dd4bf" alt="GitHub Stats" width="400">
        </a>
        <a href="https://github.com/maladarmujammil" target="_blank">
          <img src="https://github-readme-stats.vercel.app/api/top-langs/?username=maladarmujammil&layout=compact&hide_border=true&bg_color=0a0c12&title_color=2dd4bf&text_color=cbd5e6" alt="Top Languages" width="320">
        </a>
      </div>
      <div style="margin-top: 1rem;">
        <img src="https://github-readme-streak-stats.herokuapp.com/?user=maladarmujammil&theme=dark&hide_border=true&ring=2dd4bf&fire=2dd4bf&currStreakLabel=2dd4bf&background=0a0c12" width="460" alt="streak stats">
      </div>
      <p style="margin-top: 1rem; font-size: 0.85rem;"><i class="fas fa-code-branch"></i> building the future, one commit at a time — with embedded magic & cyber spirit.</p>
    </div>
  </div>

  <!-- footer contact and vibe -->
  <div class="reveal">
    <div style="background: rgba(0,0,0,0.3); backdrop-filter: blur(10px); border-radius: 2rem; padding: 1rem 2rem; text-align: center; border: 1px solid rgba(45,212,191,0.3);">
      <div style="display: flex; justify-content: center; gap: 2rem; flex-wrap: wrap;">
        <a href="mailto:maladarmujammil@gmail.com" class="btn-cyber"><i class="fas fa-envelope"></i> Email me</a>
        <a href="https://github.com/maladarmujammil" target="_blank" class="btn-cyber"><i class="fab fa-github"></i> Explore repos</a>
        <a href="https://linkedin.com/in/mujammil-maladar" target="_blank" class="btn-cyber"><i class="fab fa-linkedin"></i> Connect</a>
      </div>
      <p style="margin-top: 1rem; font-size: 0.75rem; opacity: 0.6;">
        <i class="fas fa-terminal"></i>  #buildinpublic  |  turning hardware ideas into interactive reality   |  Cybersecurity mindset
      </p>
    </div>
  </div>
</main>

<script>
  // --- Particle network background "Thagada Wala" effect ---
  const canvas = document.getElementById('particle-canvas');
  let ctx = canvas.getContext('2d');
  let particles = [];
  let particleCount = 70;

  function resizeCanvas() {
    canvas.width = window.innerWidth;
    canvas.height = window.innerHeight;
  }
  
  class Particle {
    constructor() {
      this.x = Math.random() * canvas.width;
      this.y = Math.random() * canvas.height;
      this.size = Math.random() * 2.2 + 1;
      this.speedX = (Math.random() - 0.5) * 0.6;
      this.speedY = (Math.random() - 0.5) * 0.3;
      this.opacity = Math.random() * 0.5 + 0.2;
    }
    update() {
      this.x += this.speedX;
      this.y += this.speedY;
      if (this.x < 0) this.x = canvas.width;
      if (this.x > canvas.width) this.x = 0;
      if (this.y < 0) this.y = canvas.height;
      if (this.y > canvas.height) this.y = 0;
    }
    draw() {
      if (!ctx) return;
      ctx.beginPath();
      ctx.arc(this.x, this.y, this.size, 0, Math.PI * 2);
      ctx.fillStyle = `rgba(45, 212, 191, ${this.opacity})`;
      ctx.fill();
    }
  }

  function initParticles() {
    particles = [];
    for (let i = 0; i < particleCount; i++) {
      particles.push(new Particle());
    }
  }

  function animateParticles() {
    if (!ctx) return;
    ctx.clearRect(0, 0, canvas.width, canvas.height);
    for (let p of particles) {
      p.update();
      p.draw();
    }
    // draw faint connecting lines for extra Thagada
    ctx.beginPath();
    for (let i = 0; i < particles.length; i++) {
      for (let j = i+1; j < particles.length; j++) {
        let dx = particles[i].x - particles[j].x;
        let dy = particles[i].y - particles[j].y;
        let distance = Math.sqrt(dx*dx + dy*dy);
        if (distance < 100) {
          ctx.lineWidth = 0.4;
          ctx.strokeStyle = `rgba(45, 212, 191, ${0.15 * (1 - distance/100)})`;
          ctx.beginPath();
          ctx.moveTo(particles[i].x, particles[i].y);
          ctx.lineTo(particles[j].x, particles[j].y);
          ctx.stroke();
        }
      }
    }
    requestAnimationFrame(animateParticles);
  }

  window.addEventListener('resize', () => {
    resizeCanvas();
    initParticles();
  });

  resizeCanvas();
  initParticles();
  animateParticles();

  // reveal on scroll 
  const revealElements = document.querySelectorAll('.reveal');
  function checkReveal() {
    for (let el of revealElements) {
      const rect = el.getBoundingClientRect();
      const windowHeight = window.innerHeight;
      if (rect.top < windowHeight - 80) {
        el.classList.add('visible');
      } 
    }
  }
  window.addEventListener('scroll', checkReveal);
  window.addEventListener('load', checkReveal);
  checkReveal();
  
  // Small interactive console fun
  console.log("%c🔥 Mujammil Maladar Portfolio — embedded + cyberpunk energy loaded", "color: #2dd4bf; font-size: 16px");
</script>
</body>
</html>
