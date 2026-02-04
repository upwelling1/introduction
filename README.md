
<html lang="zh-Hant">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Evan Website Studio</title>
  <link rel="stylesheet" href="style.css">
  <style>
    /* 輪播區塊樣式 */
    .slider {
      position: relative;
      max-width: 800px;
      margin: 50px auto;
      overflow: hidden;
      border-radius: 10px;
      box-shadow: 0 4px 15px rgba(0,0,0,0.2);
    }

    .slides {
      display: flex;
      transition: transform 0.5s ease-in-out;
    }

    .slide {
      min-width: 100%;
      box-sizing: border-box;
    }

    .slide img {
      width: 100%;
      display: block;
    }

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
  </style>
</head>
<body>
  <canvas id="bgCanvas"></canvas>
  <header>
    <h1>Evan Website Studio</h1>
    <div class="menu-toggle" id="menu-toggle">☰</div>
   
  </header>
  
  <section id="about" class="intro">
    <h2>關於我</h2>
    <p>嗨，我是 Evan，專門幫個人與品牌打造乾淨、有設計感的網站。  
    不論是個人介紹頁、活動宣傳或作品集網站，我都能協助從設計到上線，讓你的品牌更有質感。</p>
  </section>

  <section class="services">
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
  
  <!-- 作品範例區（輪播） -->
  <section id="works" class="works">
    <h2>作品範例展示</h2>
    <div class="slider">
      <div class="slides" id="slides">
        <div class="slide"><img src="images/work1.jpg" alt="作品1"></div>
        <div class="slide"><img src="images/work2.jpg" alt="作品2"></div>
        <div class="slide"><img src="images/work3.jpg" alt="作品3"></div>
      </div>
      <button class="prev" id="prev">❮</button>
      <button class="next" id="next">❯</button>
    </div>
  </section> 

  <footer>
    <p>© 2026 Evan Website Studio | 聯絡方式：<a href="mailto:upwelling11@gmail.com">upwelling11@gmail.com</a></p>
  </footer>

  <script>
    // 漢堡選單切換
    const toggle = document.getElementById('menu-toggle');
    const nav = document.getElementById('nav');
    toggle.addEventListener('click', () => {
      nav.classList.toggle('show');
    });

    // 輪播功能
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

    // 自動播放
    setInterval(() => {
      index = (index + 1) % totalSlides;
      updateSlide();
    }, 4000);
  </script>
</body>
</html>
