
<html lang="zh-Hant">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Evan Website Studio</title>
<style>
  html, body {
    width: 100%;
    height: 100%;
    margin: 0;
    padding: 0;
    font-family: "Noto Sans TC", sans-serif;
    background: linear-gradient(135deg, #1a3f6f, #006b8f);
    color: white;
    overflow-x: hidden;
    scroll-behavior: smooth;
  }

  /* 粒子背景 */
  #bgCanvas {
    position: fixed;
    top: 0;
    left: 0;
    width: 100vw;
    height: 100vh;
    z-index: 0;
    will-change: transform;
    transform: translateZ(0);
  }

  /* header */
  header {
    position: relative;
    z-index: 1;
    padding:60px 20px 20px;
    text-align:center;
  }
  header h1 { font-size:32px; margin:10px 0; }
  header p.tagline { max-width:600px; margin:0 auto; line-height:1.6; }

  /* 連結按鈕 */
  .link-buttons {
    position: relative;
    z-index: 1;
    display:flex; flex-direction:column; align-items:center; gap:12px; margin:30px 0;
  }
  .link-buttons a {
    text-decoration:none; background: rgba(0,0,0,0.5); color:white;
    padding:12px 20px; border-radius:10px; width:80%; max-width:300px; font-weight:500;
    transition:0.3s;
  }
  .link-buttons a:hover { background: rgba(255,255,255,0.2); transform: scale(1.05); }

  /* 輪播 */
  .slider { position:relative; z-index:1; max-width:400px; margin:30px auto; overflow:hidden; border-radius:12px; background: rgba(0,0,0,0.4); }
  .slides { display:flex; transition: transform 0.5s ease-in-out; }
  .slide { min-width:100%; display:flex; justify-content:center; align-items:center; }
  .prev, .next {
    position:absolute; top:50%; transform:translateY(-50%);
    background: rgba(0,0,0,0.5); color:white; border:none; padding:10px; border-radius:50%;
    cursor:pointer;
  }
  .prev { left:10px; } .next { right:10px; }
  .prev:hover, .next:hover { background: rgba(255,255,255,0.8); }

  /* 小圓點 */
  .dots { text-align:center; margin-top:10px; z-index:1; position:relative; }
  .dot {
    display:inline-block; width:10px; height:10px; margin:0 6px;
    background: rgba(255,255,255,0.5); border-radius:50%; cursor:pointer; transition:0.3s;
  }
  .dot.active { background:white; }

  /* 服務區 */
  .services { text-align:center; margin:50px 20px; position:relative; z-index:1; }
  .service-list { display:flex; flex-wrap:wrap; justify-content:center; gap:20px; }
  .service-item { background: rgba(0,0,0,0.6); padding:20px; border-radius:10px; width:250px; }

  /* footer */
  .footer { text-align:center; margin:40px 0 20px; font-size:14px; position:relative; z-index:1; }

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

<!-- 輪播作品範例（佔位符） -->
<section id="works" class="slider">
  <div class="slides" id="slides">
    <div class="slide">
      <div style="width:100%;height:200px;background:#888;color:white;display:flex;justify-content:center;align-items:center;font-size:24px;border-radius:12px;">
        作品 1 佔位符
      </div>
    </div>
    <div class="slide">
      <div style="width:100%;height:200px;background:#888;color:white;display:flex;justify-content:center;align-items:center;font-size:24px;border-radius:12px;">
        作品 2 佔位符
      </div>
    </div>
    <div class="slide">
      <div style="width:100%;height:200px;background:#888;color:white;display:flex;justify-content:center;align-items:center;font-size:24px;border-radius:12px;">
        作品 3 佔位符
      </div>
    </div>
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
/* === 輪播 === */
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

/* === 平滑版彩色流光粒子背景 === */
const canvas = document.getElementById('bgCanvas');
const ctx = canvas.getContext('2d');
canvas.width = window.innerWidth;
canvas.height = window.innerHeight;

const colors = ["#ff4d4d","#ff944d","#fff44d","#4dff4d","#4dffff","#4d4dff","#ff4dff"];
const particles = [];
for(let i=0;i<50;i++){
  particles.push({
    x: Math.random()*canvas.width,
    y: Math.random()*canvas.height,
    r: Math.random()*2+1,
    dx: (Math.random()-0.5)*0.7,
    dy: (Math.random()-0.5)*0.7,
    color: colors[Math.floor(Math.random()*colors.length)]
  });
}

function animate(time){
  ctx.clearRect(0,0,canvas.width,canvas.height);

  for(let i=0;i<particles.length;i++){
    const p = particles[i];
    p.x += p.dx;
    p.y += p.dy;
    if(p.x<0||p.x>canvas.width) p.dx*=-1;
    if(p.y<0||p.y>canvas.height) p.dy*=-1;

    ctx.beginPath();
    ctx.arc(p.x,p.y,p.r,0,Math.PI*2);
    ctx.fillStyle = p.color;
    ctx.fill();

    for(let j=i+1;j<particles.length;j++){
      const p2 = particles[j];
      const dx = p.x - p2.x;
      const dy = p.y - p2.y;
      const dist = Math.sqrt(dx*dx + dy*dy);
      if(dist<120){
        const grad = ctx.createLinearGradient(p.x,p.y,p2.x,p2.y);
        grad.addColorStop(0,p.color);
        grad.addColorStop(1,p2.color);
        ctx.strokeStyle = grad;
        ctx.globalAlpha = 0.15*(1-dist/120);
        ctx.beginPath();
        ctx.moveTo(p.x,p.y);
        ctx.lineTo(p2.x,p2.y);
        ctx.stroke();
        ctx.globalAlpha = 1;
      }
    }
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
