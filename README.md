
<html lang="zh-Hant">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Evan Website Studio</title>
<style>
  /* 全站背景 */
  html, body {
    width: 100%;
    height: 100%;
    margin: 0;
    padding: 0;
    font-family: "Noto Sans TC", sans-serif;
    background: linear-gradient(135deg, #0d1b2a, #1b263b, #415a77); /* 深色漸層 */
    color: white;
    overflow-x: hidden;
  }

  /* 粒子 Canvas */
  #bgCanvas {
    position: fixed;
    top:0; left:0;
    width:100vw; height:100vh;
    z-index:-9999;
  }

  /* header */
  header {
    padding:60px 20px 20px;
    text-align:center;
    background: transparent;
  }
  header h1 { font-size:32px; margin:10px 0; }
  header p.tagline { max-width:600px; margin:0 auto; line-height:1.6; }

  /* 連結按鈕 */
  .link-buttons {
    display:flex; flex-direction:column; align-items:center; gap:12px; margin:30px 0;
  }
  .link-buttons a {
    text-decoration:none; background: rgba(0,0,0,0.5); color:white;
    padding:12px 20px; border-radius:10px; width:80%; max-width:300px; font-weight:500;
    transition:0.3s;
  }
  .link-buttons a:hover { background: rgba(255,255,255,0.2); transform: scale(1.05); }

  /* 輪播 */
  .slider { position:relative; max-width:400px; margin:30px auto; overflow:hidden; border-radius:12px; background: rgba(0,0,0,0.4); }
  .slides { display:flex; transition: transform 0.5s ease-in-out; }
  .slide { min-width:100%; }
  .slide img { width:100%; border-radius:12px; display:block; }
  .prev, .next {
    position:absolute; top:50%; transform:translateY(-50%);
    background: rgba(0,0,0,0.5); color:white; border:none; padding:10px; border-radius:50%;
    cursor:pointer;
  }
  .prev { left:10px; } .next { right:10px; }
  .prev:hover, .next:hover { background: rgba(255,255,255,0.8); }

  /* 小圓點 */
  .dots { text-align:center; margin-top:10px; }
  .dot {
    display:inline-block; width:10px; height:10px; margin:0 6px;
    background: rgba(255,255,255,0.5); border-radius:50%; cursor:pointer; transition:0.3s;
  }
  .dot.active { background:white; }

  /* 服務區 */
  .services { text-align:center; margin:50px 20px; }
  .service-list { display:flex; flex-wrap:wrap; justify-content:center; gap:20px; }
  .service-item { background: rgba(0,0,0,0.6); padding:20px; border-radius:10px; width:250px; }

  /* footer */
  .footer { text-align:center; margin:40px 0 20px; font-size:14px; }

  /* 響應式 */
  @media (max-width:768px){
    .slider { max-width:90%; }
    .link-buttons a { width:90%; }
    .service-item { width:80%; }
  }
</style>
</head>
<body>

<canvas id="bgCanvas"></canvas>

<header>
  <h1>Evan Website Studio</h1>
  <p class="tagline">
    嗨，我是 Evan，專門幫個人與品牌打造乾淨、有設計感的網站。<br>
    不論是個人介紹頁、活動宣傳或作品集網站，我都能協助從設計到上線，讓你的品牌更有質感。
  </p>
</header>

<div class="link-buttons">
  <a href="#works">🎨 作品範例</a>
  <a href="#services">🧰 服務項目</a>
  <a href="mailto:upwelling11@gmail.com">💌 聯絡我</a>
</div>

<section id="works" class="slider">
  <div class="slides" id="slides">
    <div class="slide"><img src="images/work1.jpg" alt="作品1"></div>
    <div class="slide"><img src="images/work2.jpg" alt="作品2"></div>
    <div class="slide"><img src="images/work3.jpg" alt="作品3"></div>
  </div>
  <button class="prev" id="prev">❮</button>
  <button class="next" id="next">❯</button>
  <div class="dots" id="dots"></div>
</section>

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

<div class="footer">
  © 2026 Evan Website Studio<br>
  <a href="mailto:upwelling11@gmail.com" style="color:white;">upwelling11@gmail.com</a>
</div>

<script>
  /* ==== 輪播 + 小圓點 ==== */
  const slides = document.getElementById('slides');
  const totalSlides = slides.children.length;
  let index = 0;
  const dotsContainer = document.getElementById('dots');

  for(let i=0;i<totalSlides;i++){
    const dot=document.createElement('span');
    dot.classList.add('dot');
    if(i===0) dot.classList.add('active');
    dot.addEventListener('click',()=>{ index=i; updateSlide(); });
    dotsContainer.appendChild(dot);
  }

  function updateSlide(){
    slides.style.transform=`translateX(-${index*100}%)`;
    Array.from(dotsContainer.children).forEach((d,i)=>{
      d.classList.toggle('active', i===index);
    });
  }

  document.getElementById('next').addEventListener('click',()=>{
    index=(index+1)%totalSlides; updateSlide();
  });
  document.getElementById('prev').addEventListener('click',()=>{
    index=(index-1+totalSlides)%totalSlides; updateSlide();
  });

  setInterval(()=>{ index=(index+1)%totalSlides; updateSlide(); }, 4000);

  /* ==== 粒子背景 + 連線 + 滑鼠互動 ==== */
  const canvas = document.getElementById('bgCanvas');
  const ctx = canvas.getContext('2d');
  canvas.width = window.innerWidth; canvas.height = window.innerHeight;

  let mouseX = canvas.width/2;
  let mouseY = canvas.height/2;

  window.addEventListener('mousemove', e => {
    mouseX = e.clientX;
    mouseY = e.clientY;
  });

  window.addEventListener('resize', () => {
    canvas.width = window.innerWidth;
    canvas.height = window.innerHeight;
  });

  const particles = [];
  for(let i=0;i<80;i++){
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

    for(let i=0;i<particles.length;i++){
      const p = particles[i];

      // 粒子跟隨滑鼠微移
      p.dx += (mouseX - p.x) * 0.0005;
      p.dy += (mouseY - p.y) * 0.0005;

      p.x += p.dx; p.y += p.dy;

      // 邊界反彈
      if(p.x<0||p.x>canvas.width) p.dx*=-1;
      if(p.y<0||p.y>canvas.height) p.dy*=-1;

      // 畫粒子
      ctx.beginPath();
      ctx.arc(p.x,p.y,p.r,0,Math.PI*2);
      ctx.fillStyle = 'rgba(255,255,255,0.2)';
      ctx.fill();

      // 粒子連線
      for(let j=i+1;j<particles.length;j++){
        const p2 = particles[j];
        const dx = p.x - p2.x;
        const dy = p.y - p2.y;
        const dist = Math.sqrt(dx*dx + dy*dy);
        if(dist<120){
          ctx.strokeStyle = `rgba(255,255,255,${0.1*(1-dist/120)})`;
          ctx.beginPath();
          ctx.moveTo(p.x,p.y);
          ctx.lineTo(p2.x,p2.y);
          ctx.stroke();
        }
      }
    }

    requestAnimationFrame(animate);
  }

  animate();
</script>

</body>
</html>
