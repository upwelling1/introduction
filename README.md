<!DOCTYPE html>
<html lang="zh-Hant">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>粒子背景測試</title>
<style>
  html, body {
    margin: 0;
    padding: 0;
    width: 100%;
    height: 100%;
    background: linear-gradient(135deg, #0d1b2a, #1b263b, #415a77);
    overflow: hidden;
  }
  #bgCanvas {
    position: fixed;
    top:0; left:0;
    width:100vw;
    height:100vh;
    z-index:-1;
  }
</style>
</head>
<body>
<canvas id="bgCanvas"></canvas>
<script>
const canvas = document.getElementById('bgCanvas');
const ctx = canvas.getContext('2d');
canvas.width = window.innerWidth;
canvas.height = window.innerHeight;

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
    p.dx += (mouseX - p.x) * 0.0005;
    p.dy += (mouseY - p.y) * 0.0005;
    p.x += p.dx; p.y += p.dy;

    if(p.x<0||p.x>canvas.width) p.dx*=-1;
    if(p.y<0||p.y>canvas.height) p.dy*=-1;

    ctx.beginPath();
    ctx.arc(p.x,p.y,p.r,0,Math.PI*2);
    ctx.fillStyle = 'rgba(255,255,255,0.5)';
    ctx.fill();

    for(let j=i+1;j<particles.length;j++){
      const p2 = particles[j];
      const dx = p.x - p2.x;
      const dy = p.y - p2.y;
      const dist = Math.sqrt(dx*dx + dy*dy);
      if(dist<120){
        ctx.strokeStyle = `rgba(255,255,255,${0.2*(1-dist/120)})`;
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
