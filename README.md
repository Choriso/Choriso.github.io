
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
for(let i=0;i<40;i++){
    let p=document.createElement("div");
    p.className="particle";
    p.style.left=Math.random()*100+"vw";
    p.style.animationDuration=5+Math.random()*8+"s";
    p.style.animationDelay=Math.random()*5+"s";
    p.style.opacity=Math.random();
    document.body.appendChild(p);
}
</script>

</body>
</html>
