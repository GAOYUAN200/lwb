<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <!-- 关键：适配所有手机屏幕，解决显示错乱问题 -->
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>我们的故事</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, "Helvetica Neue", Arial, sans-serif;
            background-color: #000000;
            color: #ffffff;
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

        /* 优化照片样式 */
        .photo {
            width: 100%;
            border-radius: 20px;
            margin-bottom: 30px;
            box-shadow: 0 8px 30px rgba(255, 255, 255, 0.1);
            object-fit: cover;
        }

        .title {
            font-size: 26px;
            margin-bottom: 35px;
            font-weight: 600;
            letter-spacing: 1px;
        }

        /* 优化计时器布局和样式 */
        .timer {
            display: flex;
            justify-content: center;
            gap: 12px;
            flex-wrap: wrap;
        }

        .item {
            background: rgba(255, 255, 255, 0.12);
            padding: 18px 15px;
            border-radius: 12px;
            min-width: 80px;
            backdrop-filter: blur(10px);
        }

        .num {
            font-size: 32px;
            font-weight: 700;
            margin-bottom: 5px;
        }

        .unit {
            font-size: 14px;
            opacity: 0.75;
            letter-spacing: 2px;
        }

        /* 隐藏多余的代码文本 */
        code, pre {
            display: none;
        }
    </style>
</head>
<body>
    <div class="container">
        <!-- 这里替换成你的图片链接 -->
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
// 防止双指缩放，避免页面误触
document.addEventListener('touchstart', function(e) {
    if (e.touches.length > 1) e.preventDefault();
}, { passive: false });

// 修正时间：2025年10月5日 22:23（月份0-11，所以10月写9）
var startDate = new Date(2025, 9, 5, 22, 23, 0).getTime();

// 兼容旧手机的补零函数
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

// 初始化计时器并每秒更新
updateTimer();
setInterval(updateTimer, 1000);

// 页面切回时同步更新时间
document.addEventListener('visibilitychange', function() {
    if (!document.hidden) updateTimer();
});
</script>
</body>
</html>
