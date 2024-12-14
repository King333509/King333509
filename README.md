<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Auto-Spiel</title>
    <style>
        body {
            margin: 0;
            overflow: hidden;
            background-color: #333;
        }
        canvas {
            display: block;
            margin: 0 auto;
            background: #555;
        }
    </style>
</head>
<body>
    <canvas id="gameCanvas"></canvas>
    <script>
        const canvas = document.getElementById('gameCanvas');
        const ctx = canvas.getContext('2d');

        // Set canvas dimensions
        canvas.width = 400;
        canvas.height = 600;

        // Car properties
        const carWidth = 50;
        const carHeight = 100;
        let carX = canvas.width / 2 - carWidth / 2;
        const carY = canvas.height - carHeight - 20;
        const carSpeed = 5;

        // Obstacles
        const obstacles = [];
        const obstacleWidth = 50;
        const obstacleHeight = 100;
        const obstacleSpeed = 4;
        let score = 0;

        // Input keys
        let keys = {};

        // Game loop
        function gameLoop() {
            ctx.clearRect(0, 0, canvas.width, canvas.height);

            // Draw car
            ctx.fillStyle = 'red';
            ctx.fillRect(carX, carY, carWidth, carHeight);

            // Move car
            if (keys['ArrowLeft'] && carX > 0) {
                carX -= carSpeed;
            }
            if (keys['ArrowRight'] && carX < canvas.width - carWidth) {
                carX += carSpeed;
            }

            // Generate obstacles
            if (Math.random() < 0.02) {
                const obstacleX = Math.random() * (canvas.width - obstacleWidth);
                obstacles.push({ x: obstacleX, y: -obstacleHeight });
            }

            // Move and draw obstacles
            for (let i = 0; i < obstacles.length; i++) {
                const obstacle = obstacles[i];
                obstacle.y += obstacleSpeed;

                // Check collision
                if (
                    carX < obstacle.x + obstacleWidth &&
                    carX + carWidth > obstacle.x &&
                    carY < obstacle.y + obstacleHeight &&
                    carY + carHeight > obstacle.y
                ) {
                    alert(`Game Over! Dein Score: ${score}`);
                    document.location.reload();
                }

                // Remove off-screen obstacles and update score
                if (obstacle.y > canvas.height) {
                    obstacles.splice(i, 1);
                    score++;
                }

                // Draw obstacle
                ctx.fillStyle = 'black';
                ctx.fillRect(obstacle.x, obstacle.y, obstacleWidth, obstacleHeight);
            }

            // Draw score
            ctx.fillStyle = 'white';
            ctx.font = '20px Arial';
            ctx.fillText(`Score: ${score}`, 10, 30);

            requestAnimationFrame(gameLoop);
        }

        // Key events
        window.addEventListener('keydown', (e) => {
            keys[e.key] = true;
        });

        window.addEventListener('keyup', (e) => {
            keys[e.key] = false;
        });

        // Start game loop
        gameLoop();
    </script>
</body>
</html>
