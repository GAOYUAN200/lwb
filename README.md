<!DOCTYPE html>
<html lang="zh-CN">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<meta name="theme-color" content="#0f172a">

<title>我们的故事</title>

<style>
*{
    margin:0;
    padding:0;
    box-sizing:border-box;
}

html,body{
    width:100%;
    height:100%;
}

body{
    background:linear-gradient(135deg,#0f172a 0%,#1a1f35 50%,#2d1b4e 100%);
    font-family:"PingFang SC","Microsoft YaHei",sans-serif;
    color:#fff;
    display:flex;
    justify-content:center;
    align-items:center;
    overflow:hidden;
}

body::before{
    content:"";
    position:fixed;
    top:-50%;
    right:-50%;
    width:200%;
    height:200%;
    background:
    radial-gradient(circle at 20% 50%,rgba(236,72,153,.15) 0%,transparent 50%),
    radial-gradient(circle at 80% 80%,rgba(139,92,246,.15) 0%,transparent 50%);
    animation:float 15s ease-in-out infinite;
}

@keyframes float{
    0%,100%{transform:translate(0,0);}
    50%{transform:translate(-30px,-30px);}
}

.container{
    position:relative;
    z-index:1;
    max-width:500px;
    width:100%;
    padding:20px;
    text-align:center;
}

.heart-container{
    position:relative;
    margin-bottom:20px;
}

.heart{
    font-size:60px;
    animation:heartbeat 1.3s infinite;
}

.glow-ring{
    position:absolute;
    width:100px;
    height:100px;
    border:2px solid rgba(236,72,153,.3);
    border-radius:50%;
    left:50%;
    top:50%;
    transform:translate(-50%,-50%);
    animation:pulse 2s infinite;
}

@keyframes heartbeat{
    0%,100%{transform:scale(1);}
    50%{transform:scale(1.1);}
}

@keyframes pulse{
    0%,100%{
        transform:translate(-50%,-50%) scale(1);
        opacity:.3;
    }
    50%{
        transform:translate(-50%,-50%) scale(1.2);
        opacity:.1;
    }
}

.couple-photo{
    width:220px;
    height:220px;
    object-fit:cover;
    border-radius:24px;
    box-shadow:0 20px 60px rgba(236,72,153,.25);
    margin-bottom:25px;
}

.names{
    font-size:36px;
    font-weight:700;
    background:linear-gradient(135deg,#ec4899,#a78bfa);
    -webkit-background-clip:text;
    -webkit-text-fill-color:transparent;
    margin-bottom:10px;
}

.divider{
    width:60px;
    height:2px;
    background:linear-gradient(90deg,transparent,#ec4899,transparent);
    margin:12px auto;
}

.subtitle{
    color:#a0aec0;
    margin-bottom:25px;
}

.timer-card{
    background:rgba(30,41,59,.7);
    border:1px solid rgba(236,72,153,.2);
    border-radius:20px;
    padding:20px;
}

.timer-label{
    margin-bottom:15px;
    color:#cbd5e0;
}

.time-units{
    display:grid;
    grid-template-columns:repeat(4,1fr);
    gap:10px;
}

.time-unit{
    background:rgba(167,139,250,.08);
    border:1px solid rgba(167,139,250,.2);
    border-radius:12px;
    padding:10px;
}

.time-value{
    font-size:26px;
    font-weight:bold;
    background:linear-gradient(135deg,#ec4899,#a78bfa);
    -webkit-background-clip:text;
    -webkit-text-fill-color:transparent;
}

.time-label{
    color:#94a3b8;
    font-size:12px;
    margin-top:5px;
}

.start-date{
    margin-top:18px;
    color:#94a3b8;
}

.date-highlight{
    color:#f472b6;
}

@media(max-width:480px){

    .couple-photo{
        width:160px;
        height:160px;
    }

    .names{
        font-size:28px;
    }

    .time-value{
        font-size:20px;
    }

    .time-unit{
        padding:8px;
    }
}
</style>
</head>

<body>

<div class="container">

    <div class="heart-container">
        <div class="glow-ring"></div>
        <div class="heart">❤️</div>
    </div>

    <img
        class="couple-photo"
        src="https://raw.githubusercontent.com/GAOYUAN200/our-story/main/1ee8ea1eedae471666d7a9b6961ce1b7.jpg"
        alt="我们的合影"
        onerror="this.src='https://via.placeholder.com/300x300?text=Photo'"
    >

    <h1 class="names">陆韦彬 & 高原</h1>

    <div class="divider"></div>

    <p class="subtitle">我们的故事</p>

    <div class="timer-card">

        <div class="timer-label">已经在一起</div>

        <div class="time-units">

            <div class="time-unit">
                <div class="time-value" id="days">0</div>
                <div class="time-label">天</div>
            </div>

            <div class="time-unit">
                <div class="time-value" id="hours">00</div>
                <div class="time-label">小时</div>
            </div>

            <div class="time-unit">
                <div class="time-value" id="minutes">00</div>
                <div class="time-label">分钟</div>
            </div>

            <div class="time-unit">
                <div class="time-value" id="seconds">00</div>
                <div class="time-label">秒</div>
            </div>

        </div>

    </div>

    <div class="start-date">
        始于 <span class="date-highlight">2025年10月5日 22:23</span>
    </div>

</div>

<script>

const startDate = new Date(2025,9,5,22,23,0).getTime();

function updateTimer(){

    const now = Date.now();

    const diff = now - startDate;

    const days = Math.floor(diff/(1000*60*60*24));

    const hours = Math.floor(
        (diff%(1000*60*60*24))
        /(1000*60*60)
    );

    const minutes = Math.floor(
        (diff%(1000*60*60))
        /(1000*60)
    );

    const seconds = Math.floor(
        (diff%(1000*60))
        /1000
    );

    document.getElementById("days").innerText=days;
    document.getElementById("hours").innerText=String(hours).padStart(2,"0");
    document.getElementById("minutes").innerText=String(minutes).padStart(2,"0");
    document.getElementById("seconds").innerText=String(seconds).padStart(2,"0");
}

updateTimer();

setInterval(updateTimer,1000);

</script>

</body>
</html>
