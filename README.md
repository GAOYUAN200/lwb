<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <!-- 修复1：加上 viewport，所有手机正常显示 -->
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>我们的故事</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }
        body {
            font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, "Helvetica Neue", Arial, sans-serif;
            background: #000;
            color: #fff;
            min-height: 100vh;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            padding: 20px;
        }
        .container {
            text-align: center;
            max-width: 400px;
            width: 100%;
        }
        .photo {
            width: 100%;
            border-radius: 12px;
            margin-bottom: 20px;
            box-shadow: 0 0 20px rgba(255,255,255,0.1);
        }
        .title {
            font-size: 24px;
            margin-bottom: 15px;
            font-weight: 600;
        }
        .timer {
            display: flex;
            justify-content: center;
            gap: 10px;
            flex-wrap: wrap;
        }
        .item {
            background: rgba(255,255,255,0.1);
            padding: 12px 10px;
            border-radius: 8px;
            min-width: 70px;
        }
        .num {
            font-size: 28px;
            font-weight: bold;
        }
        .unit {
            font-size: 12px;
            opacity: 0.8;
        }
    </style>
</head>
<body>
    <div class="container">
        <!-- 建议换成稳定图床，暂时先用你原图 -->
        <img class="photo" src="https://github.com/GAOYUAN200/our-story/blob/main/1ee8ea1eedae471666d7a9b6961ce1b7.jpg?raw=true" alt="我们">
        <div class="title">我们在一起的时间</div>
        <div class="timer">
            <div class="item">
                <div class="num" id="days-value">0</div>
                <div class="unit">天</div>
            </div>
            <div class="item">
                <div class="num" id="hours-value">00</div>
                <div class="unit">时</div>
            </div>
            <div class="item">
                <div class="num" id="minutes-value">00</div>
                <div class="unit">分</div>
            </div>
            <div class="item">
                <div class="num" id="seconds-value">00</div>
                <div class="unit">秒</div>
            </div>
        </div>
    </div>

<script>
// 修复2：只留一次防缩放，避免iOS卡死
document.addEventListener('touchstart', function(e) {
    if (e.touches.length > 1) e.preventDefault();
}, { passive: false });

// 修复3：起始时间（月份9=10月，小时22点）
var startDate = new Date(2025, 9, 5, 22, 23, 0).getTime();

// 修复4：不用箭头函数、不用padStart，兼容旧手机
function pad(num) {
    return num < 10 ? '0' + num : '' + num;
}

function updateTimer() {
    var now = new Date().getTime();
    var diff = now - startDate;

    var days = Math.floor(diff / (1000 * 60 * 60 * 24));
    var hours = Math.floor((diff % (1000 * 60 * 60 * 24)) / (1000 * 60 * 60));
    var minutes = Math.floor((diff % (1000 * 60 * 60)) / (1000 * 60));
    var seconds = Math.floor((diff % (1000 * 60)) / 1000);

    document.getElementById('days-value').innerText = days;
    document.getElementById('hours-value').innerText = pad(hours);
    document.getElementById('minutes-value').innerText = pad(minutes);
    document.getElementById('seconds-value').innerText = pad(seconds);
}

updateTimer();
setInterval(updateTimer, 1000);

document.addEventListener('visibilitychange', function() {
    if (!document.hidden) updateTimer();
});
</script>

</body>
</html>
