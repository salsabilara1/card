<!DOCTYPE html>
<html>
<head>
    <style>
        body {
            margin: 0;
            height: 100vh;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            background-color: black;
            overflow: hidden;
            font-family: Arial, sans-serif;
        }

        #switch {
            cursor: pointer;
            background: #444;
            padding: 15px 30px;
            border-radius: 5px;
            color: white;
            font-size: 20px;
            transition: 0.3s;
        }

        #switch:hover {
            background: #666;
        }

        .balloon {
            position: absolute;
            width: 30px;
            height: 40px;
            background: red;
            border-radius: 50%;
            bottom: -50px;
            opacity: 0;
            animation: float 3s ease-in forwards;
        }

        @keyframes float {
            to {
                opacity: 1;
                transform: translateY(-100vh);
            }
        }

        #birthdayText {
            font-size: 48px;
            color: white;
            opacity: 0;
            position: relative;
            text-align: center;
        }

        #giftBox {
            width: 100px;
            height: 100px;
            background: #ff69b4;
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            display: none;
        }

        #cake {
            width: 150px;
            height: 150px;
            background: #8b4513;
            border-radius: 10px;
            position: absolute;
            display: none;
        }

        #cat {
            width: 50px;
            height: 50px;
            background: gray;
            position: absolute;
            display: none;
        }

        .confetti {
            width: 10px;
            height: 10px;
            position: absolute;
            animation: confettiFall 3s ease-in infinite;
        }

        @keyframes confettiFall {
            to {
                transform: translateY(100vh) rotate(360deg);
            }
        }
    </style>
</head>
<body>
    <div id="switch">Turn on the light</div>
    <div id="birthdayText"></div>
    <div id="giftBox"></div>
    <div id="cake"></div>
    <div id="cat"></div>
    
    <audio id="birthdayMusic" src="ibd.mp3"></audio>
    <audio id="haloMusic" src="Young_Folks.mp3"></audio>

    <script>
        const colors = ['#ff69b4', '#87CEEB', '#90EE90', '#FFD700', '#FF69B4'];
        let isLightOn = false;

        document.getElementById('switch').addEventListener('click', function() {
            if (!isLightOn) {
                isLightOn = true;
                this.style.display = 'none';
                document.body.style.backgroundColor = '#ffb6c1';
                document.getElementById('birthdayMusic').play();
                createBalloons();
                setTimeout(showBirthdayText, 2000);
                setTimeout(showGiftBox, 4000);
            }
        });

        function createBalloons() {
            for (let i = 0; i < 20; i++) {
                setTimeout(() => {
                    const balloon = document.createElement('div');
                    balloon.className = 'balloon';
                    balloon.style.left = Math.random() * window.innerWidth + 'px';
                    balloon.style.background = colors[Math.floor(Math.random() * colors.length)];
                    document.body.appendChild(balloon);
                }, i * 200);
            }
        }

        function showBirthdayText() {
            const text = document.getElementById('birthdayText');
            text.innerHTML = 'Happy Birthday C';
            text.style.opacity = '1';
            text.style.transition = 'opacity 2s';
        }

        function showGiftBox() {
            const giftBox = document.getElementById('giftBox');
            giftBox.style.display = 'block';
            setTimeout(() => {
                giftBox.style.display = 'none';
                showCake();
            }, 2000);
        }

        function showCake() {
            const cake = document.getElementById('cake');
            cake.style.display = 'block';
            setTimeout(showCat, 1000);
        }

        function showCat() {
            const cat = document.getElementById('cat');
            cat.style.display = 'block';
            setTimeout(lightCandle, 2000);
        }

        function lightCandle() {
            createConfetti();
            document.getElementById('birthdayMusic').pause();
            document.getElementById('haloMusic').play();
            document.getElementById('birthdayText').innerHTML = 'Time to Make A Wish C!';
        }

        function createConfetti() {
            for (let i = 0; i < 50; i++) {
                const confetti = document.createElement('div');
                confetti.className = 'confetti';
                confetti.style.left = Math.random() * window.innerWidth + 'px';
                confetti.style.background = colors[Math.floor(Math.random() * colors.length)];
                document.body.appendChild(confetti);
            }
        }
    </script>
</body>
</html>
