
<html lang="zh-Hant">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Evan Website Studio</title>
  <link rel="stylesheet" href="style.css">
  <style>
    /* ===== 背景樣式 ===== */
    body {
      margin: 0;
      font-family: "Noto Sans TC", sans-serif;

      /* 漸層背景 */
      background: linear-gradient(135deg, #4facfe, #00f2fe);

      /* 圓點網格疊加 */
      background-image: radial-gradient(circle, rgba(255,255,255,0.1) 1px, transparent 1px);
      background-size: 30px 30px;

      background-repeat: repeat;
      background-attachment: fixed;
    }

    /* 粒子 canvas */
    #bgCanvas {
      position: fixed;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      z-index: -1;
    }

    /* ===== Header / Hero ===== */
    header {
      padding: 50px 20px 20px;
      text-align: center;
      color: white;
    }

    header img {
      width: 100px;
      height: 100px;
      border-radius: 50%;
      object-fit: cover;
      border: 2px solid white;
    }

    h1 { margin: 15px 0 5px; font-size: 28px; }
    p.tagline { font-size: 16px; color: #f0f0f0; }

    /* ===== 連結按鈕 ===== */
    .link-buttons {
      display: flex;
      flex-direction: column;
      align-items: center;
      gap: 12px;
      margin: 30px 0;
    }

    .link-buttons a {
      text-decoration: none;
      background: rgba(0,0,0,0.7);
      color: white;
      padding: 12px 20px;
      border-radius: 10px;
      width: 80%;
      max-width: 300px;
      transition: 0.3s;
      font-weight: 500;
    }

    .link-buttons a:hover {
      background: rgba(255,255,255,0.2);
      transform: scale(1.05);
    }

    /* ===== 輪播區塊 ===== */
    .slider {
      position: relative;
      max-width: 400px;
      margin: 30px auto;
      overflow: hidden;
      border-radius: 12px;
      box-shadow: 0 4px 15px rgba(0,0,0,0.2);
    }

    .slides {
      display: flex;
      transition: transform 0.5s ease-in-out;
    }

    .slide {
      min-width: 100%;
    }

    .slide img {
      width: 100%;
      display: block;
    }

    /* 箭頭（可選） */
    .prev, .next {
      position: absolute;
      top: 50%;
      transform: translateY(-50%);
      background-color: rgba(0,0,0,0.5);
      color: white;
      border: none;
      padding: 10px;
      cursor: pointer;
      border-radius: 50%;
    }

    .prev { left: 10px; }
    .next { right: 10px; }

    .prev:hover, .next:hover {
      background-color: rgba(0,0,0,0.8);
    }

    /* ===== Footer ===== */
    .footer {
      margin: 40px 0 20px;
      font-size: 14px;
      color: white;
      text-align: center;
    }

    /* ===== 響應式 ===== */
    @media (max-width: 768px) {
      .slider { max-width: 90%; }
      .link-buttons a { width: 90%; }
    }
  </style>
</head>
<body>
  <!-- 粒子背景 -->
  <canvas id="bgCanvas"></canvas>

  <!-- Header / Hero -->
  <header>
    <img src="images/profile.jpg" alt="Evan 頭像">
    <h1>Evan Website Studio</h1>
    <p class="tagline">打造乾淨、有質感的個人與品牌網站</p>
  </header>

  <!-- 主連結區 -->
  <div class="link-buttons">
    <a href="#works">🎨 作品範例</a>
    <a href="#services">🧰 服務項目</a>
    <a href="mailto:upwelling11@gmail.com">💌 聯絡我</a>
    <a href="https://github.com/">🌐 GitHub</a>
  </div>

  <!-- 作品輪播 -->
  <section id="works" class="slider">
    <div class="slides" id="slides">
      <div class="slide"><img src="images/work1.jpg" alt="作品1"></div>
      <div class="slide"><img src="images/work2.jpg" alt="作品2"></div>
      <div class="slide"><img src="images/work3.jpg" alt="作品3"></div>
    </div>
    <button class="prev" id="prev">❮</button>
    <button class="next" id="next">❯</button>
  </section>

  <!-- 服務項目 -->
  <section id="services" class="services" style="color:white; text-align:center; margin:50px 20px;">
    <h2>服務項目</h2>
    <div style="display:flex; flex-wrap:wrap; justify-content:center; gap:20px; margin-top:20px;">
      <div style="background:rgba(0,0,0,0.5); padding:20px; border-radius:10px; width:250px;">
        <h3>客製網站設計</h3>
        <p>依照需求設計專屬頁面，展現個人或品牌特色。</p>
      </div>
      <div style="background:rgba(0,0,0,0.5); padding:20px; border-radius:10px; width:250px;">
        <h3>GitHub Pages 架設</h3>
        <p>協助設定並上線網站，穩定又方便。</p>
      </div>
      <div style="background:rgba(0,0,0,0.5); padding:20px; border-radius:10px; width:250px;">
        <h3>RWD 響應式設計</h3>
        <p>手機、平板、電腦皆完美呈現，給訪客最佳瀏覽體驗。</p>
      </div>
    </div>
  </section>

  <!-- Footer -->
  <div class="footer">
    © 2026 Evan Website Studio<br>
    <a href="mailto:upwelling11@gmail.com" style="color:white;">upwelling11@gmail.com</a>
  </div>

  <!-- ===== Script ===== -->
  <script>
    /* ==== 輪播功能 ==== */
    const slides = document.getElementById('slides');
    const totalSlides = slides.children.length;
    let index = 0;

    document.getElementById('next').addEventListener('click', () => {
      index = (index + 1) % totalSlides;
      updateSlide();
    });

    document.getElementById('prev').addEventListener('click', () => {
      index = (index - 1 + totalSlides) % totalSlides;
      updateSlide();
    });

    function updateSlide() {
      slides.style.transform = `translateX(-${index * 100}%)`;
    }

    setInterval(() => {
      index = (index + 1) % totalSlides;
      updateSlide();
    }, 4000);

    /* ==== 粒子動畫背景 ==== */
    const canvas = document.getElementById('bgCanvas');
    const ctx = canvas.getContext('2d');
    canvas.width = window.innerWidth;
    canvas.height = window.innerHeight;

    const particles = [];
    const num = 80;

    for(let i=0;i<num;i++){
      particles.push({
        x: Math.random()*canvas.width,
        y: Math.random()*canvas.height,
        r: Math.random()*3+1,
        dx: (Math.random()-0.5)*0.5,
        dy: (Math.random()-0.5)*0.5
      });
    }

    function animate(){
      ctx.clearRect(0,0,canvas.width,canvas.height);
      for(let p of particles){
        ctx.beginPath();
        ctx.arc(p.x,p.y,p.r,0,Math.PI*2);
        ctx.fillStyle = 'rgba(255,255,255,0.3)';
        ctx.fill();
        p.x += p.dx;
        p.y += p.dy;

        if(p.x < 0 || p.x > canvas.width) p.dx *= -1;
        if(p.y < 0 || p.y > canvas.height) p.dy *= -1;
      }
      requestAnimationFrame(animate);
    }

    animate();

    window.addEventListener('resize',()=>{
      canvas.width = window.innerWidth;
      canvas.height = window.innerHeight;
    });
  </script>
</body>
</html>
