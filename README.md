<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>¿Me Perdonas?</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            min-height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            overflow: hidden;
            position: relative;
        }

        .hearts {
            position: fixed;
            width: 100%;
            height: 100%;
            pointer-events: none;
            z-index: 1;
        }

        .heart {
            position: absolute;
            font-size: 30px;
            animation: float 6s infinite;
            opacity: 0;
        }

        .sparkle {
            position: fixed;
            font-size: 20px;
            animation: sparkleFloat 3s infinite;
            opacity: 0;
            pointer-events: none;
            z-index: 1000;
        }

        @keyframes float {
            0% {
                transform: translateY(100vh) rotate(0deg);
                opacity: 1;
            }
            100% {
                transform: translateY(-100vh) rotate(360deg);
                opacity: 0;
            }
        }

        @keyframes sparkleFloat {
            0% {
                transform: translateY(0) scale(0);
                opacity: 1;
            }
            50% {
                opacity: 1;
            }
            100% {
                transform: translateY(-100px) scale(1.5);
                opacity: 0;
            }
        }

        .container {
            background: white;
            padding: 50px;
            border-radius: 30px;
            box-shadow: 0 20px 60px rgba(0, 0, 0, 0.3);
            text-align: center;
            max-width: 500px;
            width: 90%;
            position: relative;
            z-index: 2;
            animation: slideIn 0.6s ease-out;
        }

        @keyframes slideIn {
            from {
                transform: scale(0.8);
                opacity: 0;
            }
            to {
                transform: scale(1);
                opacity: 1;
            }
        }

        h1 {
            color: #d946ef;
            font-size: 2.5em;
            margin-bottom: 20px;
            animation: pulse 2s infinite;
        }

        @keyframes pulse {
            0%, 100% {
                transform: scale(1);
            }
            50% {
                transform: scale(1.05);
            }
        }

        .question {
            font-size: 1.8em;
            color: #333;
            margin: 30px 0;
            font-weight: bold;
            min-height: 60px;
            display: flex;
            align-items: center;
            justify-content: center;
        }

        .buttons {
            display: flex;
            gap: 20px;
            justify-content: center;
            margin-top: 50px;
            padding-bottom: 20px;
        }

        button {
            padding: 15px 40px;
            font-size: 1.2em;
            border: none;
            border-radius: 50px;
            cursor: pointer;
            transition: all 0.3s ease;
            font-weight: bold;
            box-shadow: 0 4px 15px rgba(0, 0, 0, 0.2);
        }

        #btnSi {
            background: linear-gradient(135deg, #f093fb 0%, #f5576c 100%);
            color: white;
            position: relative;
            z-index: 10;
            transform-origin: center top;
        }

        #btnSi:hover {
            transform: scale(1.1);
            box-shadow: 0 6px 20px rgba(245, 87, 108, 0.4);
        }

        #btnNo {
            background: linear-gradient(135deg, #4facfe 0%, #00f2fe 100%);
            color: white;
        }

        #btnNo.moviendo {
            position: fixed;
            z-index: 1000;
            transition: all 0.3s ease;
        }

        .shake {
            animation: shake 0.5s;
        }

        @keyframes shake {
            0%, 100% { transform: translateX(0); }
            10%, 30%, 50%, 70%, 90% { transform: translateX(-10px); }
            20%, 40%, 60%, 80% { transform: translateX(10px); }
        }

        .mensaje {
            display: none;
            animation: fadeIn 1s ease-in;
        }

        @keyframes fadeIn {
            from {
                opacity: 0;
                transform: translateY(-20px);
            }
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }

        .mensaje-final {
            font-size: 1.5em;
            color: #d946ef;
            line-height: 1.6;
            margin-top: 20px;
        }

        .emoji {
            font-size: 3em;
            margin: 20px 0;
            display: inline-block;
            animation: bounce 1s infinite;
        }

        @keyframes bounce {
            0%, 100% {
                transform: translateY(0);
            }
            50% {
                transform: translateY(-10px);
            }
        }

        .contador {
            position: absolute;
            top: 20px;
            right: 20px;
            background: rgba(255, 255, 255, 0.9);
            padding: 10px 20px;
            border-radius: 20px;
            font-weight: bold;
            color: #d946ef;
            box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
        }

        .confetti {
            position: fixed;
            width: 10px;
            height: 10px;
            background: #f0f;
            animation: confettiFall 3s linear;
            z-index: 1000;
        }

        @keyframes confettiFall {
            to {
                transform: translateY(100vh) rotate(360deg);
                opacity: 0;
            }
        }

        .glow {
            animation: glow 1s ease-in-out infinite;
        }

        @keyframes glow {
            0%, 100% {
                box-shadow: 0 0 5px #f5576c, 0 0 10px #f5576c, 0 0 15px #f5576c;
            }
            50% {
                box-shadow: 0 0 10px #f5576c, 0 0 20px #f5576c, 0 0 30px #f5576c;
            }
        }
    </style>
</head>
<body>
    <div class="hearts" id="hearts"></div>
    
    <div class="container">
        <div class="contador" id="contador">Intentos: 0</div>
        
        <div id="contenidoPrincipal">
            <div class="emoji">💕</div>
            <h1>Mi Amor...</h1>
            <p class="question" id="pregunta">¿Me Perdonas?</p>
            
            <div class="buttons">
                <button id="btnSi" onclick="perdonado()">Sí ❤️</button>
                <button id="btnNo" onclick="moverBotonNo()">No</button>
            </div>
        </div>

        <div id="mensajeFinal" class="mensaje">
            <div class="emoji">💖</div>
            <h1>¡Gracias mi amor!</h1>
            <p class="mensaje-final">
                ¡Sabía que tu hermoso corazón me perdonaría! 🥰
                <br><br>
                Eres la persona más especial de mi vida y prometo ser mejor cada día. 
                Te amo más de lo que las palabras pueden expresar. 
                Gracias por darme otra oportunidad. 
                <br><br>
                Eres mi todo 💕✨🌟
            </p>
        </div>
    </div>

    <script>
        let intentos = 0;
        let tamañoBotonSi = 1;
        
        // Crear corazones flotantes
        function crearCorazon() {
            const hearts = document.getElementById('hearts');
            const heart = document.createElement('div');
            heart.className = 'heart';
            const emojis = ['💗', '💕', '💖', '💝', '💘', '❤️', '🌹'];
            heart.innerHTML = emojis[Math.floor(Math.random() * emojis.length)];
            heart.style.left = Math.random() * 100 + '%';
            heart.style.animationDelay = Math.random() * 5 + 's';
            heart.style.fontSize = (Math.random() * 20 + 20) + 'px';
            hearts.appendChild(heart);

            setTimeout(() => {
                heart.remove();
            }, 6000);
        }

        setInterval(crearCorazon, 300);

        const frases = [
            "¿Estás segura? Por favor, perdóname 🥺",
            "Dale, una oportunidad más, te lo ruego 💕",
            "Mi vida, ¿me das otra chance? 🙏",
            "Sin ti no soy nada, por favor 💔",
            "Prometo que no volverá a pasar 🌹",
            "Eres lo más importante para mí 💖",
            "Te necesito en mi vida, amor 🥺",
            "¿Y si lo pensamos mejor? 💗",
            "Dame una oportunidad de demostrártelo 🌟",
            "Por favor mi amor, perdóname 💕",
            "Haré lo que sea por tu perdón 🙏",
            "Eres mi todo, no me dejes así 💔",
            "Sé que puedo ser mejor, créeme 🌹",
            "Mi corazón es solo tuyo 💖",
            "¿Porfa porfa porfa? 🥺",
            "Te amo más que a nada, perdóname 💗",
            "Una última oportunidad, amor 💕",
            "Sin tu perdón no puedo seguir 🙏",
            "Eres mi razón de ser 💖",
            "Por favor, di que sí 🥺",
            "No puedo vivir sin tu perdón 😭",
            "Eres mi sol, mi luna y mis estrellas ✨",
            "Te necesito como el aire que respiro 💨",
            "¿Me das una oportunidad más? 🌈",
            "Haré todo por reconquistarte 👑",
            "Eres mi persona favorita 🌟",
            "No hay nadie como tú en este mundo 🌍",
            "Te prometo que cambiaré 💪",
            "Eres mi felicidad 😊",
            "¡Por favor, mi amor! 💝"
        ];

        function crearChispas(x, y) {
            for(let i = 0; i < 5; i++) {
                const sparkle = document.createElement('div');
                sparkle.className = 'sparkle';
                sparkle.innerHTML = '✨';
                sparkle.style.left = x + 'px';
                sparkle.style.top = y + 'px';
                sparkle.style.animationDelay = (i * 0.1) + 's';
                document.body.appendChild(sparkle);
                
                setTimeout(() => {
                    sparkle.remove();
                }, 3000);
            }
        }

        function moverBotonNo() {
            const btnNo = document.getElementById('btnNo');
            
            intentos++;
            document.getElementById('contador').textContent = `Intentos: ${intentos}`;
            
            // Cambiar frase
            const pregunta = document.getElementById('pregunta');
            pregunta.style.animation = 'none';
            setTimeout(() => {
                pregunta.style.animation = 'fadeIn 0.5s ease-in';
                pregunta.textContent = frases[intentos % frases.length];
            }, 10);
            
            // Hacer más grande el botón Sí
            const btnSi = document.getElementById('btnSi');
            tamañoBotonSi += 0.1;
            btnSi.style.transform = `scale(${tamañoBotonSi})`;
            
            // Agregar brillo al botón Sí después de 3 intentos
            if(intentos >= 3) {
                btnSi.classList.add('glow');
            }
            
            // Obtener posición actual del botón antes de moverlo
            const rect = btnNo.getBoundingClientRect();
            crearChispas(rect.left + rect.width/2, rect.top + rect.height/2);
            
            // Cambiar a posición fija para que se mueva por toda la pantalla
            btnNo.classList.add('moviendo');
            
            // Calcular nueva posición aleatoria en toda la ventana
            const btnWidth = btnNo.offsetWidth;
            const btnHeight = btnNo.offsetHeight;
            
            const maxX = window.innerWidth - btnWidth - 20;
            const maxY = window.innerHeight - btnHeight - 20;
            
            const randomX = Math.random() * maxX;
            const randomY = Math.random() * maxY;
            
            btnNo.style.left = randomX + 'px';
            btnNo.style.top = randomY + 'px';
            
            // Cambiar el texto del botón No ocasionalmente
            const textosNo = ['No', '¡No!', 'Nop', 'Nel', 'Nope', 'Nanai', '❌'];
            if(Math.random() > 0.7) {
                btnNo.textContent = textosNo[Math.floor(Math.random() * textosNo.length)];
            }
        }

        function crearConfetti() {
            const colors = ['#f093fb', '#f5576c', '#4facfe', '#00f2fe', '#feca57', '#ff6b6b', '#ee5a6f', '#a29bfe'];
            
            for(let i = 0; i < 100; i++) {
                setTimeout(() => {
                    const confetti = document.createElement('div');
                    confetti.className = 'confetti';
                    confetti.style.left = Math.random() * window.innerWidth + 'px';
                    confetti.style.top = '-10px';
                    confetti.style.background = colors[Math.floor(Math.random() * colors.length)];
                    confetti.style.width = (Math.random() * 10 + 5) + 'px';
                    confetti.style.height = confetti.style.width;
                    document.body.appendChild(confetti);
                    
                    setTimeout(() => {
                        confetti.remove();
                    }, 3000);
                }, i * 30);
            }
        }

        function perdonado() {
            crearConfetti();
            
            document.getElementById('contenidoPrincipal').style.display = 'none';
            const mensajeFinal = document.getElementById('mensajeFinal');
            mensajeFinal.style.display = 'block';
            
            // Más corazones cuando perdona
            for(let i = 0; i < 50; i++) {
                setTimeout(crearCorazon, i * 50);
            }
            
            // Cambiar el fondo
            document.body.style.background = 'linear-gradient(135deg, #f093fb 0%, #f5576c 100%)';
        }
    </script>
</body>
</html>
