<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>I Have Something to Say 💕</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: linear-gradient(135deg, #ff9a9e 0%, #fecfef 50%, #fecfef 100%);
            min-height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            overflow-x: hidden;
        }

        .container {
            background: rgba(255, 255, 255, 0.95);
            padding: 40px;
            border-radius: 25px;
            box-shadow: 0 20px 40px rgba(0, 0, 0, 0.1);
            text-align: center;
            max-width: 500px;
            width: 90%;
            backdrop-filter: blur(10px);
            animation: slideIn 0.8s ease-out;
        }

        @keyframes slideIn {
            from {
                opacity: 0;
                transform: translateY(50px);
            }
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }

        h1 {
            color: #e91e63;
            margin-bottom: 20px;
            font-size: 2.5em;
        }

        .heart {
            font-size: 2em;
            animation: heartbeat 1.5s infinite;
        }

        @keyframes heartbeat {
            0% { transform: scale(1); }
            14% { transform: scale(1.3); }
            28% { transform: scale(1); }
            42% { transform: scale(1.3); }
            70% { transform: scale(1); }
        }

        input[type="text"], input[type="button"] {
            width: 100%;
            padding: 15px;
            margin: 15px 0;
            border: none;
            border-radius: 15px;
            font-size: 1.1em;
            transition: all 0.3s ease;
        }

        input[type="text"] {
            background: #f8f9fa;
            box-shadow: inset 0 2px 5px rgba(0,0,0,0.1);
        }

        input[type="text"]:focus {
            outline: none;
            background: white;
            box-shadow: 0 0 20px rgba(233, 30, 99, 0.3);
            transform: scale(1.02);
        }

        input[type="button"] {
            background: linear-gradient(45deg, #e91e63, #f06292);
            color: white;
            font-weight: bold;
            cursor: pointer;
            text-transform: uppercase;
            letter-spacing: 1px;
        }

        input[type="button"]:hover {
            transform: translateY(-2px);
            box-shadow: 0 10px 25px rgba(233, 30, 99, 0.4);
        }

        .message {
            background: linear-gradient(45deg, #fff3e0, #ffe0b2);
            padding: 25px;
            border-radius: 20px;
            margin: 20px 0;
            box-shadow: 0 10px 30px rgba(0,0,0,0.1);
            font-size: 1.3em;
            line-height: 1.5;
            color: #d84315;
            animation: fadeInUp 0.6s ease-out;
        }

        @keyframes fadeInUp {
            from {
                opacity: 0;
                transform: translateY(30px);
            }
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }

        .love-question {
            font-size: 1.5em;
            color: #e91e63;
            margin: 30px 0;
        }

        .success {
            color: #4caf50;
            font-size: 2em;
            animation: bounce 0.6s infinite alternate;
        }

        @keyframes bounce {
            from { transform: translateY(0); }
            to { transform: translateY(-10px); }
        }

        .hidden {
            display: none;
        }

        .particles {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            pointer-events: none;
            z-index: -1;
        }

        .particle {
            position: absolute;
            font-size: 20px;
            animation: float 6s infinite linear;
        }

        @keyframes float {
            0% {
                transform: translateY(100vh) rotate(0deg);
                opacity: 1;
            }
            100% {
                transform: translateY(-100px) rotate(360deg);
                opacity: 0;
            }
        }
    </style>
</head>
<body>
    <div class="particles" id="particles"></div>
    
    <div class="container" id="container">
        <h1 class="heart">💕</h1>
        
        <div id="nameSection">
            <input type="text" id="nameInput" placeholder="Enter your name..." maxlength="20">
            <input type="button" value="Continue ❤️" onclick="getName()">
        </div>

        <div id="firstMessage" class="hidden">
            <div class="message">
                Hey <span id="userName"></span> ❤️<br>
                I just wanted to say something...
            </div>
            <input type="button" value="Press to Continue 💕" onclick="showLoveMessage()">
        </div>

        <div id="loveMessage" class="hidden">
            <div class="message">
                You are the most special person in my life 💕<br>
                And I really like you 😊
            </div>
            <div class="love-question">
                Do you love me?
            </div>
            <div style="margin: 20px 0;">
                <input type="button" value="Yes 😍" onclick="answerYes()" style="background: linear-gradient(45deg, #4caf50, #81c784); margin: 10px;">
                <input type="button" value="No 😏" onclick="answerNo()" style="background: linear-gradient(45deg, #ff9800, #ffb74d); margin: 10px;">
            </div>
        </div>

        <div id="successMessage" class="hidden">
            <div class="message success">
                Yayyy! I knew it 😍❤️
            </div>
        </div>

        <div id="retryMessage" class="hidden">
            <div class="message">
                Are you sure? Try again 😏
            </div>
            <div style="margin: 20px 0;">
                <input type="button" value="Yes 😍" onclick="answerYes()" style="background: linear-gradient(45deg, #4caf50, #81c784); margin: 10px;">
                <input type="button" value="No 😏" onclick="answerNo()" style="background: linear-gradient(45deg, #ff9800, #ffb74d); margin: 10px;">
            </div>
        </div>
    </div>

    <script>
        let userName = '';

        function getName() {
            userName = document.getElementById('nameInput').value.trim();
            if (userName) {
                document.getElementById('nameSection').classList.add('hidden');
                document.getElementById('userName').textContent = userName;
                document.getElementById('firstMessage').classList.remove('hidden');
            } else {
                alert('Please enter your name! 💕');
            }
        }

        function showLoveMessage() {
            document.getElementById('firstMessage').classList.add('hidden');
            document.getElementById('loveMessage').classList.remove('hidden');
        }

        function answerYes() {
            document.querySelectorAll('.message, .love-question').forEach(el => el.classList.add('hidden'));
            document.getElementById('successMessage').classList.remove('hidden');
            createHearts();
        }

        function answerNo() {
            document.getElementById('loveMessage').classList.add('hidden');
            document.getElementById('retryMessage').classList.remove('hidden');
        }

        // Enter key support
        document.addEventListener('keypress', function(e) {
            if (e.key === 'Enter') {
                if (!document.getElementById('nameSection').classList.contains('hidden')) {
                    getName();
                }
            }
        });

        // Floating hearts animation
        function createHearts() {
            const particles = document.getElementById('particles');
            for (let i = 0; i < 20; i++) {
                setTimeout(() => {
                    const heart = document.createElement('div');
                    heart.className = 'particle';
                    heart.innerHTML = ['💕', '❤️', '💖', '💗'][Math.floor(Math.random() * 4)];
                    heart.style.left = Math.random() * 100 + '%';
                    heart.style.animationDuration = (Math.random() * 3 + 3) + 's';
                    heart.style.animationDelay = Math.random() * 2 + 's';
                    particles.appendChild(heart);
                    
                    setTimeout(() => heart.remove(), 6000);
                }, i * 200);
            }
        }

        // Initial floating hearts
        setInterval(() => {
            const particle = document.createElement('div');
            particle.className = 'particle';
            particle.innerHTML = ['💕', '❤️'][Math.floor(Math.random() * 2)];
            particle.style.left = Math.random() * 100 + '%';
            particle.style.animationDuration = (Math.random() * 3 + 4) + 's';
            document.getElementById('particles').appendChild(particle);
            
            setTimeout(() => particle.remove(), 7000);
        }, 2000);
    </script>
</body>
</html>
