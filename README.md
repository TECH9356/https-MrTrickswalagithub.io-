<!doctype html>
<html lang="hi">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1" />
  <title>Secret Web — Mr Trickswala</title>
  <meta name="description" content="Mr Trickswala Secret Web — Next upload countdown, TV shows and contact." />
  <style>
    /* ---------- Fonts & Base ---------- */
    @import url('https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;600;800&display=swap');
    :root{
      --bg1:#07070a; --bg2:#0f0b1a; --accent1:#ff416c; --accent2:#00ffcc; --accent3:#00b3ff;
      --glass: rgba(255,255,255,0.04);
      --card: rgba(255,255,255,0.03);
      --radius:14px;
    }
    *{box-sizing:border-box}
    html,body{height:100%}
    body{
      margin:0;
      font-family:'Poppins',system-ui,-apple-system,Segoe UI,Roboto,"Helvetica Neue",Arial;
      color:#eaeef2;
      background: linear-gradient(120deg,#05040a 0%, #0f0b1a 35%, #071323 100%);
      -webkit-font-smoothing:antialiased;
      -moz-osx-font-smoothing:grayscale;
      overflow-x:hidden;
    }

    /* ---------- Canvas full-screen ---------- */
    #bgCanvas{ position:fixed; inset:0; width:100%; height:100%; z-index:0; display:block; }

    /* Matrix overlay (subtle) */
    .matrix {
      position:fixed; inset:0; z-index:0; pointer-events:none; mix-blend-mode:screen; opacity:0.06;
    }

    /* ---------- Layout ---------- */
    .wrap{ position:relative; z-index:2; max-width:1100px; margin:28px auto; padding:20px; }
    header{ display:flex; align-items:center; gap:16px; justify-content:center; margin-bottom:18px; }
    .logo {
      width:64px; height:64px; border-radius:14px;
      background: radial-gradient(circle at 20% 20%, var(--accent1), #ff7aa2 40%, var(--accent2));
      display:flex; align-items:center; justify-content:center; font-weight:800; color:#081018; box-shadow:0 8px 30px rgba(0,0,0,0.6), 0 0 24px rgba(255,65,108,0.06) inset;
      transform-origin:center; animation: logoPulse 2800ms ease-in-out infinite;
    }
    @keyframes logoPulse{0%{transform:scale(1)}50%{transform:scale(1.08)}100%{transform:scale(1)}}
    header h1{ margin:0; font-size:20px; font-weight:800; letter-spacing:0.6px; color:#fff; }
    header h1 .sub{ display:block; font-size:12px; font-weight:600; color:#cfeff0; opacity:0.9 }

    /* ---------- Countdown ---------- */
    .count-wrap{ display:flex; justify-content:center; gap:18px; margin-bottom:20px; }
    .count-box{
      min-width:260px; padding:18px; border-radius:16px;
      background: linear-gradient(180deg, rgba(255,255,255,0.03), rgba(255,255,255,0.02));
      border:1px solid rgba(255,255,255,0.04);
      box-shadow: 0 12px 30px rgba(2,6,23,0.6);
      text-align:center;
      backdrop-filter: blur(8px);
    }
    .count-title{ font-size:13px; color:#c7f7f0; margin-bottom:6px; font-weight:600; }
    .count-display{ font-family: 'Poppins', monospace; font-size:34px; color:var(--accent2); font-weight:800; letter-spacing:2px; text-shadow: 0 4px 22px rgba(0,255,204,0.06); }

    /* ---------- Sections ---------- */
    .section{ margin:22px auto; padding:18px; border-radius:var(--radius); background:var(--glass); border:1px solid rgba(255,255,255,0.03); backdrop-filter:blur(8px); box-shadow:0 8px 30px rgba(0,0,0,0.6); }
    .section h2{ margin:0 0 14px 0; font-size:18px; color:#fff; letter-spacing:0.4px }

    /* Serial List (pro cards) */
    .serial-grid{ display:grid; gap:12px; grid-template-columns: repeat(auto-fit,minmax(160px,1fr)); }
    .serial{
      display:flex; gap:10px; align-items:center; padding:12px; border-radius:12px; cursor:pointer;
      background:linear-gradient(135deg, rgba(255,255,255,0.02), rgba(255,255,255,0.01));
      border:1px solid rgba(255,255,255,0.02);
      transition: transform 0.2s ease, box-shadow .2s ease;
    }
    .serial:hover{ transform:translateY(-6px); box-shadow:0 12px 30px rgba(0,0,0,0.6); }
    .serial .icon{ width:46px; height:46px; border-radius:10px; display:flex; align-items:center; justify-content:center; font-size:18px; background:linear-gradient(90deg,var(--accent1),var(--accent3)); color:#061018; font-weight:800; box-shadow:0 6px 18px rgba(0,0,0,0.5) inset; }
    .serial .meta{ text-align:left; }
    .serial .meta .title{ font-size:15px; font-weight:700; color:#fff; }
    .serial .meta .sub{ font-size:12px; color:#bcdfe0; margin-top:4px; }

    /* more / join button */
    .more-row{ display:flex; justify-content:center; margin-top:14px; }
    .btn{
      display:inline-block; padding:12px 22px; border-radius:999px; font-weight:800; letter-spacing:0.6px;
      background: linear-gradient(90deg,var(--accent3),var(--accent2));
      color:#081018; text-decoration:none; box-shadow:0 8px 30px rgba(0,179,255,0.12);
      transition: transform .18s ease, box-shadow .18s ease;
    }
    .btn:hover{ transform:translateY(-6px); box-shadow:0 18px 40px rgba(0,179,255,0.18) }

    /* contact */
    .contact{ display:flex; flex-direction:column; align-items:center; gap:8px; max-width:420px; margin:0 auto; }
    .contact a{ color:var(--accent2); text-decoration:none; font-weight:700; }
    .contact .small{ color:#cbdfe2; font-size:13px; }

    /* footer */
    footer{ margin:28px 0 60px; color:#9fbfc1; font-size:13px; opacity:0.9; }

    /* responsiveness tweaks */
    @media (max-width:680px){
      header{ padding:18px }
      .count-display{ font-size:26px }
    }
  </style>
</head>
<body>
  <!-- Canvas for particles -->
  <canvas id="bgCanvas"></canvas>

  <!-- Subtle matrix overlay using canvas (same canvas used for particles and matrix) -->
  <div class="wrap" role="main" aria-live="polite">
    <header>
      <div class="logo" aria-hidden="true">SW</div>
      <h1>Secret Web <span class="sub">by Mr Trickswala</span></h1>
    </header>

    <div class="count-wrap">
      <div class="count-box" role="region" aria-label="Next upload countdown">
        <div class="count-title">Next Video Upload</div>
        <div class="count-display" id="countdown">00:00:00</div>
        <div style="margin-top:8px;font-size:12px;color:#cbdfe2">Daily at 6:30 PM</div>
      </div>
    </div>

    <section class="section" aria-labelledby="showsHeading">
      <h2 id="showsHeading">Popular TV Series</h2>

      <div class="serial-grid" id="serialGrid">
        <!-- Each card opens the same Telegram group (or different if you want later) -->
        <a class="serial" href="https://t.me/SMtrickswalatemcon" target="_blank" rel="noopener noreferrer">
          <div class="icon">TM</div>
          <div class="meta"><div class="title">Taarak Mehta</div><div class="sub">Free Episode Group</div></div>
        </a>

        <a class="serial" href="https://t.me/KBCfreeepisode" target="_blank" rel="noopener noreferrer">
          <div class="icon">KBC</div>
          <div class="meta"><div class="title">KBC</div><div class="sub">Join Episodes</div></div>
        </a>

        <a class="serial" href="https://t.me/KBCfreeepisode" target="_blank" rel="noopener noreferrer">
          <div class="icon">PU</div>
          <div class="meta"><div class="title">Parvati Umesh Jindagi</div><div class="sub">Latest & Archived</div></div>
        </a>

        <a class="serial" href="https://t.me/KBCfreeepisode" target="_blank" rel="noopener noreferrer">
          <div class="icon">B1</div>
          <div class="meta"><div class="title">Bahu No.1</div><div class="sub">Full Episodes</div></div>
        </a>

        <a class="serial" href="https://t.me/KBCfreeepisode" target="_blank" rel="noopener noreferrer">
          <div class="icon">MD</div>
          <div class="meta"><div class="title">Million Dollar</div><div class="sub">Watch Free</div></div>
        </a>

        <a class="serial" href="https://t.me/KBCfreeepisode" target="_blank" rel="noopener noreferrer">
          <div class="icon">SL</div>
          <div class="meta"><div class="title">Shrimati Lakhpati</div><div class="sub">Episodes</div></div>
        </a>

        <a class="serial" href="https://t.me/KBCfreeepisode" target="_blank" rel="noopener noreferrer">
          <div class="icon">SS</div>
          <div class="meta"><div class="title">Shiv Shakti Mahadev</div><div class="sub">Mythology Series</div></div>
        </a>

        <a class="serial" href="https://t.me/KBCfreeepisode" target="_blank" rel="noopener noreferrer">
          <div class="icon">BD</div>
          <div class="meta"><div class="title">Bindi</div><div class="sub">Classic Serial</div></div>
        </a>
      </div>

      <div class="more-row">
        <a class="btn" href="https://t.me/KBCfreeepisode" target="_blank" rel="noopener noreferrer">All Serials — Tap to Join</a>
      </div>
    </section>

    <section class="section" aria-labelledby="contactHeading">
      <h2 id="contactHeading">Contact</h2>
      <div class="contact">
        <div class="small">Telegram</div>
        <a id="tgLink" href="https://t.me/mrtrickswalas" target="_blank" rel="noopener noreferrer">@mrtrickswalas</a>
        <button id="copyTg" style="padding:8px 12px;border-radius:8px;border:0;background:#00ffcc;color:#081018;font-weight:700;cursor:pointer">Copy Telegram</button>

        <div style="height:6px"></div>
        <div class="small">Email</div>
        <a id="mailLink" href="mailto:cutcap671@gmail.com">cutcap671@gmail.com</a>
        <button id="copyEmail" style="padding:8px 12px;border-radius:8px;border:0;background:#ff416c;color:white;font-weight:700;cursor:pointer">Copy Email</button>
      </div>
    </section>

    <footer>Made by Mr Trickswala — Secret Web</footer>
  </div>

  <!-- ---------- Scripts: countdown + canvas particles + copy ---------- -->
  <script>
    /* -------- Countdown (6:30 PM daily) -------- */
    function updateCountdown(){
      const now = new Date();
      const target = new Date();
      target.setHours(18,30,0,0); // 6:30 PM
      if(now > target) target.setDate(target.getDate() + 1);
      const diff = target - now;
      const h = String(Math.floor(diff / (1000*60*60))).padStart(2,'0');
      const m = String(Math.floor((diff / (1000*60)) % 60).toString()).padStart(2,'0');
      const s = String(Math.floor((diff / 1000) % 60).toString()).padStart(2,'0');
      document.getElementById('countdown').textContent = `${h}:${m}:${s}`;
    }
    setInterval(updateCountdown, 1000);
    updateCountdown();

    /* -------- Copy buttons -------- */
    document.getElementById('copyTg').addEventListener('click', async ()=>{
      try { await navigator.clipboard.writeText('@mrtrickswalas'); document.getElementById('copyTg').textContent='Copied ✓'; setTimeout(()=>document.getElementById('copyTg').textContent='Copy Telegram',1500); }
      catch(e){ alert('Copy failed — use manual copy: @mrtrickswalas'); }
    });
    document.getElementById('copyEmail').addEventListener('click', async ()=>{
      try { await navigator.clipboard.writeText('cutcap671@gmail.com'); document.getElementById('copyEmail').textContent='Copied ✓'; setTimeout(()=>document.getElementById('copyEmail').textContent='Copy Email',1500); }
      catch(e){ alert('Copy failed — use manual copy: cutcap671@gmail.com'); }
    });

    /* -------- Canvas particles + matrix rain -------- */
    const canvas = document.getElementById('bgCanvas');
    const ctx = canvas.getContext('2d');
    let W = canvas.width = innerWidth;
    let H = canvas.height = innerHeight;
    window.addEventListener('resize', ()=>{ W = canvas.width = innerWidth; H = canvas.height = innerHeight; initParticles(); });

    // Particles (gentle upward/float neon)
    let particles = [];
    function Particle(){
      this.x = Math.random()*W;
      this.y = Math.random()*H;
      this.r = Math.random()*1.6 + 0.4;
      this.a = Math.random()*0.9 + 0.1;
      this.vx = (Math.random()-0.5)*0.2;
      this.vy = - (Math.random()*0.6 + 0.1);
      this.color = `rgba(0,255,200,${this.a})`;
    }
    Particle.prototype.update = function(){
      this.x += this.vx;
      this.y += this.vy;
      if(this.y < -10){ this.y = H + 10; this.x = Math.random()*W; }
    }
    Particle.prototype.draw = function(){
      ctx.beginPath();
      ctx.fillStyle = this.color;
      ctx.arc(this.x,this.y,this.r,0,Math.PI*2);
      ctx.fill();
    }

    // Matrix columns
    const cols = Math.floor(W/14);
    let matrixCols = [];
    function MatrixCol(x){
      this.x = x;
      this.y = Math.random()*-200;
      this.speed = 1 + Math.random()*2.5;
      this.chars = '01'; // binary look
    }
    MatrixCol.prototype.update = function(){
      this.y += this.speed;
      if(this.y > H + 100) this.y = Math.random()*-400;
    }
    MatrixCol.prototype.draw = function(){
      ctx.font = '12px monospace';
      ctx.fillStyle = 'rgba(0,255,102,0.06)';
      for(let i=0;i<6;i++){
        const yy = this.y - i*14;
        ctx.fillText( this.chars.charAt(Math.floor(Math.random()*this.chars.length)), this.x, yy);
      }
    }

    function initParticles(){
      particles = [];
      let total = Math.floor((W*H)/9000);
      for(let i=0;i<total;i++) particles.push(new Particle());
      // matrix columns
      matrixCols = [];
      const step = 16;
      for(let x = 0; x < W; x+=step) matrixCols.push(new MatrixCol(x));
    }
    initParticles();

    function animate(){
      ctx.clearRect(0,0,W,H);
      // gradient subtle overlay
      const g = ctx.createLinearGradient(0,0,W,H);
      g.addColorStop(0,'rgba(10,6,22,0.06)');
      g.addColorStop(1,'rgba(2,8,12,0.06)');
      ctx.fillStyle = g; ctx.fillRect(0,0,W,H);

      // draw matrix faint
      matrixCols.forEach(c=>{ c.update(); c.draw(); });

      // draw particles
      particles.forEach(p=>{ p.update(); p.draw(); });
      requestAnimationFrame(animate);
    }
    animate();

    /* Accessibility: allow opening group from keyboard on Enter for cards */
    document.querySelectorAll('.serial').forEach(s=>{
      s.setAttribute('tabindex','0');
      s.addEventListener('keypress', e=>{
        if(e.key === 'Enter') s.click();
      });
    });
  </script>
</body>
</html>
