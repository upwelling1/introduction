
<!DOCTYPE html>
<html lang="zh-Hant">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Evan Website Studio</title>
  <style>
    /* ===== 全站背景 ===== */
    html, body {
      width: 100%;
      height: 100%;
      margin: 0;
      padding: 0;
      font-family: "Noto Sans TC", sans-serif;

      /* 漸層 + 圓點網格 */
      background: linear-gradient(135deg, #4facfe, #00f2fe);
      background-image: radial-gradient(circle, rgba(255,255,255,0.1) 1px, transparent 1px);
      background-size: 30px 30px;
      background-repeat: repeat;
      background-attachment: fixed;
      color: white;
    }

    /* 粒子 canvas */
    #bgCanvas {
      position: fixed;
      top: 0;
      left: 0;
      width: 100vw;
      height: 100vh;
      z-index: -9999;
    }

    /* ===== Header / 自我介紹 ===== */
    header {
      padding: 60px 20px 20px;
      text-align: center;
      background: transparent;
    }

    header h1 {
      margin: 10px 0;
      font-size: 32px;
    }

    header p.tagline {
      font-size: 16px;
      color: #f0f0f0;
      max-width: 600px;
      margin: 0 auto;
      line-height: 1.6;
    }

    /* ===== 主連結按鈕 ===== */
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
      background: transparent;
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
      border-radius: 12px;
    }

    /* 輪播箭頭 */
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

    /* 輪播小圓點 */
    .dots {
      text-align: center;
      margin-top: 10px;
    }

    .dot {
      display: inline-block;
      width: 10px;
      height: 10px;
      margin: 0 6px;
      background-color: rgba(255,255,255,0.5);
      border-radius: 50%;
      cursor: pointer;
      transition: 0.3s;
    }

    .dot.active {
      background-color: white;
    }

    /* ===== 服務區 ===== */
    .services {
      text-align: center;
      margin: 50px 20px;
    }

    .services h2 {
      margin-bottom: 30px;
      font-size: 28px;
    }

    .service-list {
      display: flex;
      flex-wrap: wrap;
      justify-content: center;
      gap: 20px;
    }

    .service-item {
      background: rgba(0,0,0,0.5);
      padding: 20px;
      border-radius: 10px;
      width: 250px;
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
      .service-item { width: 80%; }
    }
  </style>
</head>
<body>
  <!-- 粒子背景 -->
  <canvas id="bgCanvas"></canvas>

  <!-- Header / 自我介紹 -->
  <header>
    <h1>Evan Website Studio</h1>
    <p class="tagline">
      嗨，我是 Evan，專門幫個人與品牌打造乾淨、有設計感的網站。<br>
      不論是個人介紹頁、活動宣傳或作品集網站，我都能協助從設計到上線，讓你的品牌更有質感。
    </p>
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

    <!-- 小圓點指示器 -->
    <div class="dots" id="dots"></div>
  </section>

  <!-- 服務區 -->
  <section id="services" class="services">
    <h2>服務項目</h2>
    <div class="service-list">
      <div class="service-item">
        <h3>客製網站設計</h3>
        <p>依照需求設計專屬頁面，展現個人或品牌特色。</p>
      </div>
      <div class="service-item">
        <h3>GitHub Pages 架設</h3>
        <p>協助設定並上線網站，穩定又方便。</p>
      </div>
      <div class="service-item">
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
    /* ==== 輪播功能 + 小圓點 ==== */
    const slides = document.getElementById('slides');
    const totalSlides = slides.children.length;
    let index = 0;

    const dotsContainer = document.getElementById('dots');

    // 產生小圓點
    for(let i=0; i<totalSlides; i++){
      const dot = document.createElement('span');
      dot.classList.add('dot');
      if(i===0) dot.classList.add('active');
      dot.addEventListener('click', ()=>{
        index = i;
        updateSlide();
      });
      dotsContainer.appendChild(dot);
    }

    function updateSlide(){
      slides.style.transform = `translateX(-${index * 100}%)`;
      const allDots = dotsContainer.children;
      for(let i=0; i<allDots.length; i++){
        allDots[i].classList.remove('active');
      }
      allDots[index].classList.add('active');
    }

    document.getElementById('next').addEventListener('click', () => {
      index = (index + 1) % totalSlides;
      updateSlide();
    });

    document.getElementById('prev').addEventListener('click', () => {
      index = (index - 1 + totalSlides) % totalSlides;
      updateSlide();
    });

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
