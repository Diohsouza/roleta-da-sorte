<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Roleta da New Life</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }
        
        body {
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
            background: linear-gradient(135deg, #1a2a6c, #b21f1f, #fdbb2d);
            padding: 20px;
            overflow-x: hidden;
        }
        
        .container {
            background: rgba(255, 255, 255, 0.95);
            border-radius: 20px;
            box-shadow: 0 15px 40px rgba(0, 0, 0, 0.4);
            width: 100%;
            max-width: 1000px;
            padding: 30px;
            text-align: center;
        }
        
        .header {
            margin-bottom: 25px;
            position: relative;
        }
        
        h1 {
            color: #1a2a6c;
            font-size: 3rem;
            margin-bottom: 10px;
            text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.1);
        }
        
        .subtitle {
            color: #444;
            font-size: 1.3rem;
            margin-bottom: 10px;
            font-weight: 500;
        }
        
        .jackpot {
            background: linear-gradient(45deg, #ffd700, #ff9800);
            color: #8b0000;
            padding: 8px 20px;
            border-radius: 30px;
            font-weight: bold;
            font-size: 1.2rem;
            display: inline-block;
            margin-top: 10px;
            box-shadow: 0 4px 10px rgba(0, 0, 0, 0.2);
        }
        
        .game-container {
            display: flex;
            flex-wrap: wrap;
            justify-content: center;
            gap: 40px;
            margin: 30px 0;
        }
        
        .wheel-container {
            position: relative;
            width: 450px;
            height: 450px;
            flex-shrink: 0;
        }
        
        .wheel {
            width: 100%;
            height: 100%;
            border-radius: 50%;
            position: relative;
            overflow: hidden;
            border: 10px solid #2c3e50;
            box-shadow: 0 0 25px rgba(0, 0, 0, 0.4);
            transition: transform 5s cubic-bezier(0.2, 0.8, 0.2, 1);
            background: #f5f5f5;
        }
        
        .wheel-section {
            position: absolute;
            width: 50%;
            height: 50%;
            transform-origin: bottom right;
            left: 0;
            top: 0;
            display: flex;
            align-items: center;
            justify-content: center;
            color: white;
            font-weight: bold;
            font-size: 0; /* Inicialmente escondido */
            transition: font-size 0.3s;
            clip-path: polygon(0 0, 100% 0, 100% 100%);
        }
        
        .wheel-section:hover {
            font-size: 1.1rem;
            z-index: 100;
        }
        
        .pointer {
            position: absolute;
            top: -35px;
            left: 50%;
            transform: translateX(-50%);
            width: 50px;
            height: 80px;
            background: #ff5722;
            clip-path: polygon(50% 100%, 0 0, 100% 0);
            z-index: 10;
            box-shadow: 0 0 15px rgba(0, 0, 0, 0.7);
            border-top: 5px solid #ff8c00;
        }
        
        .pointer::after {
            content: "";
            position: absolute;
            top: 5px;
            left: 5px;
            right: 5px;
            height: 15px;
            background: #ffd700;
            clip-path: polygon(50% 100%, 0 0, 100% 0);
        }
        
        .controls {
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            gap: 25px;
            width: 350px;
        }
        
        .spin-btn {
            background: linear-gradient(to right, #1a2a6c, #4a00e0);
            color: white;
            border: none;
            padding: 18px 50px;
            font-size: 1.8rem;
            font-weight: bold;
            border-radius: 60px;
            cursor: pointer;
            box-shadow: 0 8px 20px rgba(26, 42, 108, 0.6);
            transition: all 0.3s;
            width: 100%;
            position: relative;
            overflow: hidden;
        }
        
        .spin-btn::before {
            content: "";
            position: absolute;
            top: -10px;
            left: -100%;
            width: 60%;
            height: 200%;
            background: linear-gradient(
                to right,
                rgba(255, 255, 255, 0) 0%,
                rgba(255, 255, 255, 0.4) 50%,
                rgba(255, 255, 255, 0) 100%
            );
            transform: rotate(25deg);
        }
        
        .spin-btn:hover {
            transform: translateY(-5px);
            box-shadow: 0 12px 25px rgba(26, 42, 108, 0.8);
        }
        
        .spin-btn:hover::before {
            animation: shine 1.5s ease;
        }
        
        .spin-btn:active {
            transform: translateY(2px);
        }
        
        .spin-btn:disabled {
            background: #cccccc;
            cursor: not-allowed;
            transform: none;
            box-shadow: none;
        }
        
        .result-container {
            background: linear-gradient(135deg, #f0f8ff, #e6f7ff);
            border-radius: 20px;
            padding: 25px;
            min-height: 180px;
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            border: 3px solid #1a2a6c;
            width: 100%;
            box-shadow: inset 0 0 15px rgba(0, 0, 0, 0.1);
            position: relative;
            overflow: hidden;
        }
        
        .result-container::before {
            content: "";
            position: absolute;
            top: -50%;
            left: -50%;
            width: 200%;
            height: 200%;
            background: radial-gradient(circle, rgba(255,255,255,0.2) 0%, rgba(255,255,255,0) 70%);
            z-index: 1;
        }
        
        .result-title {
            color: #333;
            font-size: 1.4rem;
            margin-bottom: 15px;
            font-weight: 600;
            z-index: 2;
        }
        
        .result-value {
            font-size: 3.5rem;
            font-weight: bold;
            color: #e44d26;
            text-shadow: 3px 3px 6px rgba(0, 0, 0, 0.2);
            transition: all 0.5s;
            z-index: 2;
        }
        
        .instructions {
            background: #e3f2fd;
            border-radius: 15px;
            padding: 25px;
            margin-top: 30px;
            text-align: left;
            border-left: 6px solid #2196f3;
            position: relative;
            overflow: hidden;
        }
        
        .instructions::before {
            content: "🎯";
            position: absolute;
            top: 10px;
            right: 20px;
            font-size: 3rem;
            opacity: 0.1;
        }
        
        .instructions h2 {
            color: #1a2a6c;
            margin-bottom: 20px;
            font-size: 1.8rem;
            border-bottom: 2px dashed #2196f3;
            padding-bottom: 10px;
        }
        
        .instructions ul {
            padding-left: 25px;
        }
        
        .instructions li {
            margin-bottom: 12px;
            line-height: 1.6;
            font-size: 1.1rem;
            position: relative;
        }
        
        .instructions li::before {
            content: "•";
            color: #2196f3;
            font-weight: bold;
            display: inline-block;
            width: 1em;
            margin-left: -1em;
        }
        
        .prizes-distribution {
            display: flex;
            flex-wrap: wrap;
            justify-content: center;
            gap: 12px;
            margin-top: 25px;
            max-width: 800px;
            margin-left: auto;
            margin-right: auto;
        }
        
        .prize-item {
            background: linear-gradient(135deg, #4caf50, #2e7d32);
            color: white;
            padding: 10px 18px;
            border-radius: 25px;
            font-weight: bold;
            font-size: 1.1rem;
            display: flex;
            align-items: center;
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
        }
        
        .special-prize {
            background: linear-gradient(135deg, #ffd700, #ff9800);
            color: #8b0000;
            font-weight: 800;
            transform: scale(1.1);
            z-index: 5;
        }
        
        @keyframes shine {
            to {
                left: 150%;
            }
        }
        
        @keyframes pulse {
            0% { transform: scale(1); }
            50% { transform: scale(1.1); }
            100% { transform: scale(1); }
        }
        
        @keyframes confettiFall {
            0% { transform: translateY(-100px) rotate(0deg); opacity: 1; }
            100% { transform: translateY(100vh) rotate(360deg); opacity: 0; }
        }
        
        .pulse {
            animation: pulse 0.7s ease-in-out;
        }
        
        .jackpot-animation {
            animation: pulse 0.5s infinite alternate;
        }
        
        .stats {
            display: flex;
            justify-content: center;
            gap: 30px;
            margin-top: 25px;
            font-size: 1.2rem;
            color: #333;
            font-weight: 500;
        }
        
        .stat-box {
            background: #f8f9fa;
            padding: 15px 25px;
            border-radius: 15px;
            box-shadow: 0 4px 8px rgba(0,0,0,0.1);
            min-width: 150px;
        }
        
        .stat-value {
            font-size: 1.8rem;
            font-weight: bold;
            color: #1a2a6c;
            margin-top: 5px;
        }
        
        .footer {
            margin-top: 30px;
            color: #666;
            font-size: 0.9rem;
            padding-top: 15px;
            border-top: 1px solid #eee;
        }
        
        @media (max-width: 900px) {
            .game-container {
                flex-direction: column;
                align-items: center;
            }
            
            .wheel-container {
                width: 320px;
                height: 320px;
            }
            
            .controls {
                width: 100%;
                max-width: 400px;
            }
            
            h1 {
                font-size: 2.2rem;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <div class="header">
            <h1><i class="fas fa-life-ring"></i> Roleta da New Life</h1>
            <p class="subtitle">Cada contrato vendido = 1 giro na roleta</p>
            <div class="jackpot">Prêmio máximo: R$100,00</div>
        </div>
        
        <div class="game-container">
            <div class="wheel-container">
                <div class="pointer"></div>
                <div class="wheel" id="wheel">
                    <!-- As seções serão geradas por JavaScript -->
                </div>
            </div>
            
            <div class="controls">
                <button class="spin-btn" id="spinBtn">
                    <i class="fas fa-sync-alt"></i> GIRAR ROLETA
                </button>
                
                <div class="result-container">
                    <div class="result-title">PRÊMIO SORTEADO</div>
                    <div class="result-value" id="result">R$00</div>
                </div>
                
                <div class="stats">
                    <div class="stat-box">
                        <div>Total de Giros</div>
                        <div class="stat-value" id="totalSpins">0</div>
                    </div>
                    <div class="stat-box">
                        <div>Maior Prêmio</div>
                        <div class="stat-value" id="maxPrize">R$0</div>
                    </div>
                </div>
            </div>
        </div>
        
        <div class="prizes-distribution">
            <div class="prize-item">11x R$10</div>
            <div class="prize-item">11x R$15</div>
            <div class="prize-item">11x R$20</div>
            <div class="prize-item">11x R$25</div>
            <div class="prize-item">11x R$30</div>
            <div class="prize-item">11x R$35</div>
            <div class="prize-item">11x R$40</div>
            <div class="prize-item">11x R$45</div>
            <div class="prize-item">11x R$50</div>
            <div class="prize-item special-prize">1x R$100</div>
        </div>
        
        <div class="instructions">
            <h2><i class="fas fa-info-circle"></i> Como Funciona a Roleta</h2>
            <ul>
                <li>A roleta possui <strong>100 seções</strong> com valores de prêmios variados</li>
                <li><strong>11 seções</strong> para cada valor entre R$10 e R$50</li>
                <li><strong>1 seção especial</strong> com o prêmio máximo de R$100</li>
                <li>Clique no botão "GIRAR ROLETA" para sortear seu prêmio</li>
                <li>O valor sorteado será exibido no painel de resultados</li>
                <li>A probabilidade de ganhar R$100 é de apenas 1%!</li>
                <li>Os valores são pagos imediatamente após o sorteio</li>
            </ul>
        </div>
        
        <div class="footer">
            Roleta da New Life &copy; 2023 - Sistema de bônus para equipe de vendas
        </div>
    </div>

    <script>
        document.addEventListener('DOMContentLoaded', function() {
            const wheel = document.getElementById('wheel');
            const spinBtn = document.getElementById('spinBtn');
            const resultDisplay = document.getElementById('result');
            const totalSpinsDisplay = document.getElementById('totalSpins');
            const maxPrizeDisplay = document.getElementById('maxPrize');
            
            // Definir a distribuição de prêmios
            const prizes = [];
            const prizeValues = [10, 15, 20, 25, 30, 35, 40, 45, 50];
            
            // Adicionar 11 seções para cada valor de prêmio
            prizeValues.forEach(value => {
                for (let i = 0; i < 11; i++) {
                    prizes.push(value);
                }
            });
            
            // Adicionar a seção especial de R$100
            prizes.push(100);
            
            // Cores para os prêmios (R$100 terá cor especial)
            const colors = [
                '#FF5252', '#FF9800', '#FFEB3B', '#4CAF50', 
                '#2196F3', '#3F51B5', '#9C27B0', '#E91E63', '#607D8B'
            ];
            
            // Criar as seções da roleta
            prizes.forEach((prize, index) => {
                const section = document.createElement('div');
                section.className = 'wheel-section';
                
                // Determinar a cor com base no valor do prêmio
                let colorIndex = prizeValues.indexOf(prize);
                if (colorIndex === -1) colorIndex = 0; // Fallback
                
                section.style.backgroundColor = prize === 100 ? '#FFD700' : colors[colorIndex];
                
                // Posicionamento das seções
                const rotation = (360 / prizes.length) * index;
                section.style.transform = `rotate(${rotation}deg)`;
                section.dataset.value = prize;
                
                wheel.appendChild(section);
            });
            
            // Variáveis de controle
            let isSpinning = false;
            let currentRotation = 0;
            let totalSpins = 0;
            let maxPrize = 0;
            
            // Função para girar a roleta
            spinBtn.addEventListener('click', () => {
                if (isSpinning) return;
                
                isSpinning = true;
                spinBtn.disabled = true;
                resultDisplay.textContent = "GIRANDO...";
                resultDisplay.style.color = "#1a2a6c";
                
                // Sorteia um prêmio (0 a 99)
                const prizeIndex = Math.floor(Math.random() * prizes.length);
                const selectedPrize = prizes[prizeIndex];
                
                // Atualizar estatísticas
                totalSpins++;
                totalSpinsDisplay.textContent = totalSpins;
                
                if (selectedPrize > maxPrize) {
                    maxPrize = selectedPrize;
                    maxPrizeDisplay.textContent = `R$${maxPrize}`;
                }
                
                // Calcula o ângulo de parada
                const sectionAngle = 360 / prizes.length;
                const extraRotations = 8; // 8 voltas completas
                const targetRotation = 360 * extraRotations + (360 - (prizeIndex * sectionAngle)) - (sectionAngle / 2);
                
                // Aplica a rotação
                currentRotation += targetRotation;
                wheel.style.transform = `rotate(${currentRotation}deg)`;
                
                // Mostra o resultado após a rotação
                setTimeout(() => {
                    resultDisplay.textContent = `R$${selectedPrize}`;
                    resultDisplay.style.color = selectedPrize === 100 ? '#c00' : '#e44d26';
                    resultDisplay.classList.add('pulse');
                    
                    // Animação especial para o prêmio máximo
                    if (selectedPrize === 100) {
                        createConfetti();
                        resultDisplay.classList.add('jackpot-animation');
                        setTimeout(() => {
                            resultDisplay.classList.remove('jackpot-animation');
                        }, 3000);
                    }
                    
                    setTimeout(() => {
                        resultDisplay.classList.remove('pulse');
                        isSpinning = false;
                        spinBtn.disabled = false;
                    }, 1000);
                    
                    // Efeito de confete para qualquer prêmio
                    createConfetti();
                }, 5000);
            });
            
            // Efeito de confete
            function createConfetti() {
                const confettiCount = 70;
                const container = document.querySelector('.container');
                
                for (let i = 0; i < confettiCount; i++) {
                    const confetti = document.createElement('div');
                    confetti.style.position = 'absolute';
                    confetti.style.width = '15px';
                    confetti.style.height = '15px';
                    confetti.style.backgroundColor = getRandomColor();
                    confetti.style.borderRadius = '50%';
                    confetti.style.top = '-30px';
                    confetti.style.left = `${Math.random() * 100}%`;
                    confetti.style.opacity = '0.9';
                    confetti.style.zIndex = '9999';
                    
                    container.appendChild(confetti);
                    
                    // Animação
                    const animation = confetti.animate([
                        { 
                            transform: `translate(0, 0) rotate(0deg)`,
                            opacity: 1
                        },
                        { 
                            transform: `translate(${(Math.random() - 0.5) * 200}px, ${window.innerHeight}px) rotate(${Math.random() * 360}deg)`,
                            opacity: 0
                        }
                    ], {
                        duration: 2000 + Math.random() * 2000,
                        easing: 'cubic-bezier(0.1, 0.8, 0.2, 1)',
                    });
                    
                    // Remove o confete após a animação
                    animation.onfinish = () => {
                        confetti.remove();
                    };
                }
            }
            
            function getRandomColor() {
                const colors = [
                    '#FF5252', '#FF9800', '#FFEB3B', '#4CAF50', 
                    '#2196F3', '#3F51B5', '#9C27B0', '#E91E63',
                    '#FFD700', '#00BCD4', '#8BC34A'
                ];
                return colors[Math.floor(Math.random() * colors.length)];
            }
        });
    </script>
</body>
</html>
