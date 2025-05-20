# biao <!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>❤️ 给最特别的你 ❤️</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            background: linear-gradient(45deg, #ff9a9e, #fad0c4);
            min-height: 100vh;
            overflow: hidden;
            font-family: '微软雅黑', sans-serif;
        }

        .container {
            position: relative;
            height: 100vh;
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
        }

        .heart {
            position: absolute;
            background: #ff3f3f;
            width: 50px;
            height: 50px;
            transform: rotate(-45deg);
            animation: heartbeat 1.2s infinite;
        }

        .heart::before,
        .heart::after {
            content: '';
            position: absolute;
            background: inherit;
            width: 50px;
            height: 50px;
            border-radius: 50%;
        }

        .heart::before {
            top: -25px;
            left: 0;
        }

        .heart::after {
            left: 25px;
            top: 0;
        }

        h1 {
            color: #fff;
            font-size: 3.5em;
            text-shadow: 2px 2px 4px rgba(0,0,0,0.3);
            margin-bottom: 20px;
            opacity: 0;
            animation: fadeIn 2s forwards;
        }

        .message {
            color: #fff;
            font-size: 1.8em;
            text-align: center;
            max-width: 600px;
            margin: 20px;
            opacity: 0;
            animation: fadeIn 2s 1s forwards;
        }

        .btn {
            padding: 15px 40px;
            background: #ff6b6b;
            border: none;
            border-radius: 30px;
            color: white;
            font-size: 1.2em;
            cursor: pointer;
            transition: transform 0.3s;
            margin-top: 30px;
            opacity: 0;
            animation: fadeIn 2s 2s forwards;
        }

        .btn:hover {
            transform: scale(1.1);
            background: #ff5252;
        }

        .hidden {
            display: none;
            margin-top: 30px;
            color: #fff;
            font-size: 1.5em;
        }

        @keyframes heartbeat {
            0% { transform: rotate(-45deg) scale(1); }
            50% { transform: rotate(-45deg) scale(1.2); }
            100% { transform: rotate(-45deg) scale(1); }
        }

        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(20px); }
            to { opacity: 1; transform: translateY(0); }
        }

        /* 飘落爱心效果 */
        .falling-hearts span {
            position: absolute;
            color: #ff3f3f;
            font-size: 1.2em;
            animation: falling 10s linear infinite;
        }

        @keyframes falling {
            0% {
                transform: translateY(-10vh) rotate(0deg);
                opacity: 1;
            }
            100% {
                transform: translateY(110vh) rotate(360deg);
                opacity: 0;
            }
        }
    </style>
</head>
<body>
    <div class="falling-hearts"></div>
    
    <div class="container">
        <div class="heart"></div>
        <h1>❤️ 我喜欢你 ❤️</h1>
        <p class="message">从第一次遇见你的那一刻起，<br>我的世界就充满了色彩</p >
        
        <button class="btn" onclick="showMessage()">点击查看悄悄话</button>
        <p id="secretMessage" class="hidden">你愿意让这个故事继续写下去吗？</p >
    </div>

    <script>
        // 创建飘落爱心
        function createHearts() {
            const container = document.querySelector('.falling-hearts');
            for(let i = 0; i < 30; i++) {
                const heart = document.createElement('span');
                heart.innerHTML = '❤️';
                heart.style.left = Math.random() * 100 + '%';
                heart.style.animationDelay = Math.random() * 10 + 's';
                container.appendChild(heart);
            }
        }

        function showMessage() {
            const message = document.getElementById('secretMessage');
            const btn = document.querySelector('.btn');
            
            message.style.display = 'block';
            message.style.animation = 'fadeIn 1s forwards';
            btn.innerHTML = "❤️ 我也喜欢你！ ❤️";
            btn.style.animation = 'none';
            btn.offsetHeight; // 触发重绘
            btn.style.animation = 'pulse 1s infinite';
        }

        // 初始化
        window.onload = () => {
            createHearts();
            // 添加点击特效
            document.body.addEventListener('click', function(e) {
                const x = e.pageX;
                const y = e.pageY;
                const heart = document.createElement('div');
                heart.className = 'heart';
                heart.style.position = 'absolute';
                heart.style.left = x + 'px';
                heart.style.top = y + 'px';
                document.body.appendChild(heart);
                setTimeout(() => heart.remove(), 1000);
            });
        }
    </script>
</body>
</html>
