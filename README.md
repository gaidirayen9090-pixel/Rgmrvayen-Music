# Rgmrvayen-Music
<!DOCTYPE html>
<html lang="ar">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>RGM Rvayen Music</title>
<style>
    body, html {
        margin: 0;
        padding: 0;
        width: 100%;
        height: 100%;
        font-family: 'Arial', sans-serif;
        background: #000;
        color: #fff;
        overflow-x: hidden;
        scroll-behavior: smooth;
    }

    canvas {
        position: fixed;
        top: 0;
        left: 0;
        z-index: 0;
    }

    .container {
        position: relative;
        z-index: 1;
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
        min-height: 100vh;
        text-align: center;
        padding: 50px 20px;
    }

    #cover {
        width: 250px;
        height: 250px;
        background: url('rgm.png') no-repeat center center;
        background-size: contain;
        border-radius: 50%;
        box-shadow: 0 0 50px #ffcc00;
        animation: pulse 2s infinite;
        margin-bottom: 20px;
    }

    @keyframes pulse {
        0% { transform: scale(1); box-shadow: 0 0 30px #ffcc00; }
        50% { transform: scale(1.08); box-shadow: 0 0 60px #ffcc00; }
        100% { transform: scale(1); box-shadow: 0 0 30px #ffcc00; }
    }

    h1 {
        text-shadow: 2px 2px 10px #000;
        margin-bottom: 20px;
    }

    .social-links {
        display: flex;
        gap: 25px;
        margin-bottom: 50px;
    }

    .social-links a {
        color: #fff;
        font-size: 2.5em;
        text-decoration: none;
        transition: transform 0.3s, color 0.3s, text-shadow 0.3s;
    }

    .social-links a:hover {
        color: #ffcc00;
        transform: scale(1.3) rotate(-10deg);
        text-shadow: 2px 2px 15px #000;
    }

    #about {
        background: rgba(0,0,0,0.7);
        padding: 30px 50px;
        border-radius: 15px;
        max-width: 600px;
        opacity: 0;
        transform: translateY(50px);
        transition: all 1s ease-out;
        box-shadow: 0 0 30px #ffcc00;
    }

    #about h2 {
        color: #ffcc00;
        margin-bottom: 15px;
    }

    #about p {
        font-size: 1.1em;
        line-height: 1.6em;
    }

    #about.visible {
        opacity: 1;
        transform: translateY(0);
    }

    @media (max-width: 500px) {
        #cover { width: 180px; height: 180px; }
        .social-links a { font-size: 2em; }
        #about { padding: 20px 25px; font-size: 0.95em; }
    }
</style>
<script src="https://kit.fontawesome.com/a076d05399.js" crossorigin="anonymous"></script>
</head>
<body>

<canvas id="bgCanvas"></canvas>

<div class="container">
    <div id="cover"></div>
    <h1>RGM Rvayen Music</h1>

    <div class="social-links">
        <a href="https://www.instagram.com/rgm__phinix" target="_blank"><i class="fab fa-instagram"></i></a>
        <a href="https://youtube.com/@rgmrvayen" target="_blank"><i class="fab fa-youtube"></i></a>
        <a href="#" target="_blank"><i class="fab fa-spotify"></i></a>
    </div>

    <div id="about">
        <h2>About Me</h2>
        <p>Hi! I'm Rayan, a new artist passionate about music and creating unique sounds. My journey started with a dream to express emotions through melodies and connect with people worldwide. Welcome to my musical world!</p>
    </div>
</div>

<!-- فيديو YouTube مخفي لتشغيل الأغنية تلقائياً -->
<iframe id="ytplayer" type="text/html" width="0" height="0"
    src="https://www.youtube.com/embed/HcITnTUGK9Q?autoplay=1&controls=0&loop=1&playlist=HcITnTUGK9Q"
    frameborder="0" allow="autoplay; encrypted-media" allowfullscreen>
</iframe>

<script>
    // خلفية متحركة تفاعلية
    const canvas = document.getElementById('bgCanvas');
    const ctx = canvas.getContext('2d');
    let width = canvas.width = window.innerWidth;
    let height = canvas.height = window.innerHeight;
    const particles = [];
    const particleCount = 150;

    function random(min, max) { return Math.random() * (max - min) + min; }

    class Particle {
        constructor() { this.reset(); }
        reset() {
            this.x = random(0, width);
            this.y = random(0, height);
            this.radius = random(1,4);
            this.speedX = random(-1,1);
            this.speedY = random(-1,1);
        }
        draw() {
            ctx.beginPath();
            ctx.arc(this.x, this.y, this.radius,0,Math.PI*2);
            ctx.fillStyle='rgba(255,204,0,0.7)';
            ctx.fill();
        }
        update() {
            this.x += this.speedX;
            this.y += this.speedY;
            if(this.x<0||this.x>width||this.y<0||this.y>height){ this.reset(); }
            this.draw();
        }
    }

    for(let i=0;i<particleCount;i++){ particles.push(new Particle()); }

    function animate(){
        ctx.fillStyle='rgba(0,0,0,0.1)';
        ctx.fillRect(0,0,width,height);
        particles.forEach(p=>p.update());
        requestAnimationFrame(animate);
    }

    animate();

    window.addEventListener('resize', ()=>{
        width = canvas.width = window.innerWidth;
        height = canvas.height = window.innerHeight;
    });

    // ظهور About Me عند التمرير
    const about = document.getElementById('about');
    window.addEventListener('scroll', ()=>{
        const top = about.getBoundingClientRect().top;
        if(top < window.innerHeight - 100){
            about.classList.add('visible');
        }
    });
</script>

</body>
</html>
