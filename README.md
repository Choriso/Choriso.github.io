
<html lang="ru">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>С Днём Рождения</title>

<style>
*{
    margin:0;
    padding:0;
    box-sizing:border-box;
}

body{
    height:100vh;
    overflow:hidden;
    display:flex;
    justify-content:center;
    align-items:center;
    font-family:Arial,sans-serif;

    background:linear-gradient(
        -45deg,
        #ff7eb3,
        #ff758c,
        #ffb347,
        #ffd86f
    );
    background-size:400% 400%;
    animation:bg 12s ease infinite;
}

@keyframes bg{
    0%{background-position:0% 50%}
    50%{background-position:100% 50%}
    100%{background-position:0% 50%}
}

.card{
    text-align:center;
    backdrop-filter:blur(10px);
    background:rgba(255,255,255,0.15);
    border:1px solid rgba(255,255,255,0.3);
    border-radius:30px;
    padding:40px;
    box-shadow:0 8px 40px rgba(0,0,0,0.15);
}

#t{
    font-size:15vw;
    font-weight:700;
    color:white;
    text-shadow:
        0 0 10px rgba(255,255,255,.8),
        0 0 30px rgba(255,255,255,.5),
        0 0 60px rgba(255,255,255,.3);

    opacity:0;
    transform:scale(.5);
    animation:show 2s ease forwards;
}

@keyframes show{
    to{
        opacity:1;
        transform:scale(1);
    }
}

.particle{
    position:absolute;
    width:8px;
    height:8px;
    border-radius:50%;
    background:white;
    opacity:.8;
    animation:float linear infinite;
}

@keyframes float{
    from{
        transform:translateY(110vh) scale(0);
    }
    to{
        transform:translateY(-20vh) scale(1.5);
    }
}
</style>
</head>

<body>

<div class="card">
    <div id="t">16.06.2025</div>
</div>

<script>
// Частицы фона
for(let i=0;i<40;i++){
    let p=document.createElement("div");
    p.className="particle";
    p.style.left=Math.random()*100+"vw";
    p.style.animationDuration=5+Math.random()*8+"s";
    p.style.animationDelay=Math.random()*5+"s";
    p.style.opacity=Math.random();
    document.body.appendChild(p);
}

// Canvas для фейерверков
const canvas = document.createElement("canvas");
canvas.style.position = "fixed";
canvas.style.inset = "0";
canvas.style.pointerEvents = "none";
canvas.style.zIndex = "999";
document.body.appendChild(canvas);

const ctx = canvas.getContext("2d");

function resize(){
    canvas.width = innerWidth;
    canvas.height = innerHeight;
}
resize();
addEventListener("resize", resize);

const particles = [];

function firework(x, y){

    for(let i=0;i<80;i++){

        const angle = Math.random() * Math.PI * 2;
        const speed = 2 + Math.random() * 5;

        particles.push({
            x,
            y,
            vx: Math.cos(angle) * speed,
            vy: Math.sin(angle) * speed,
            life: 100,
            size: 2 + Math.random() * 3,
            hue: Math.random() * 360
        });
    }
}

function animate(){

    ctx.fillStyle = "rgba(0,0,0,0.08)";
    ctx.clearRect(0,0,canvas.width,canvas.height);

    for(let i=particles.length-1;i>=0;i--){

        const p = particles[i];

        p.x += p.vx;
        p.y += p.vy;

        p.vy += 0.03;
        p.life--;

        ctx.beginPath();
        ctx.arc(p.x,p.y,p.size,0,Math.PI*2);
        ctx.fillStyle =
            `hsla(${p.hue},100%,65%,${p.life/100})`;
        ctx.fill();

        if(p.life<=0){
            particles.splice(i,1);
        }
    }

    requestAnimationFrame(animate);
}

animate();

// Автоматические фейерверки вокруг даты
setInterval(()=>{

    const rect =
        document.getElementById("t")
        .getBoundingClientRect();

    const x =
        rect.left +
        Math.random()*rect.width;

    const y =
        rect.top -
        50 -
        Math.random()*150;

    firework(x,y);

},1200);
</script>

</body>
</html>
