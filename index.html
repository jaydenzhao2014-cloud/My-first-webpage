<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>2D Battle Royale</titl e>
    <style>
        * {
            margin: 0;
            : 0;
            box-sizing: border-box;
        }

        body {
            background: #1a1a2e;
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
            font-family: 'Arial', sans-serif;
            color: white;
        }

        #gameContainer {
            position: relative;
        }

        canvas {
            border: 3px solid #00ff41;
            background: #0f3460;
            display: block;
        }

        #ui {
            position: absolute;
            top: 10px;
            left: 10px;
            background: rgba(0, 0, 0, 0.7);
            padding: 15px;
            border-radius: 5px;
            min-width: 200px;
        }

        #weaponSelect {
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            background: rgba(0, 0, 0, 0.9);
            padding: 30px;
            border-radius: 10px;
            text-align: center;
        }

        .weapon-btn {
            display: block;
            width: 250px;
            margin: 10px auto;
            padding: 15px;
            font-size: 16px;
            background: #00ff41;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            font-weight: bold;
            transition: all 0.3s;
        }

        .weapon-btn:hover {
            background: #00cc33;
            transform: scale(1.05);
        }

        #gameOver {
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            background: rgba(0, 0, 0, 0.9);
            padding: 40px;
            border-radius: 10px;
            text-align: center;
            display: none;
        }

        #restartBtn {
            margin-top: 20px;
            padding: 15px 30px;
            font-size: 18px;
            background: #00ff41;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            font-weight: bold;
        }

        .stat {
            margin: 5px 0;
            font-size: 14px;
        }

        h2 {
            margin-bottom: 20px;
            color: #00ff41;
        }
    </style>
</head>
<body>
    <div id="gameContainer">
        <canvas id="gameCanvas"></canvas>

        <div id="weaponSelect">
            <h2>Choose Your Weapon</h2>
            <button class="weapon-btn" onclick="selectWeapon('pistol')">Pistol - Fast fire, low damage</button>
            <button class="weapon-btn" onclick="selectWeapon('rifle')">Assault Rifle - Balanced</button>
            <button class="weapon-btn" onclick="selectWeapon('shotgun')">Shotgun - Close range, high damage</button>
            <button class="weapon-btn" onclick="selectWeapon('sniper')">Sniper - Long range, very high damage</button>
            <button class="weapon-btn" onclick="selectWeapon('smg')">SMG - Very fast, spray and pray</button>
        </div>

        <div id="ui" style="display: none;">
            <div class="stat">Health: <span id="health">100</span></div>
            <div class="stat">Weapon: <span id="weapon">None</span></div>
            <div class="stat">Enemies: <span id="enemies">5</span></div>
            <div class="stat">Zone Damage: <span id="zoneDamage">0</span>/s</div>
            <div class="stat">Map Size: <span id="mapSize">100</span>%</div>
        </div>

        <div id="gameOver">
            <h2 id="gameOverText">Game Over</h2>
            <p id="finalStats"></p>
            <button id="restartBtn" onclick="location.reload()">Play Again</button>
        </div>
    </div>

    <script>
        const canvas = document.getElementById('gameCanvas');
        const ctx = canvas.getContext('2d');
        canvas.width = 800;
        canvas.height = 600;

        // Game state
        let gameStarted = false;
        let gameRunning = false;
        let player = null;
        let enemies = [];
        let bullets = [];
        let particles = [];
        let safeZone = { x: 400, y: 300, radius: 350 };
        let targetZone = { x: 400, y: 300, radius: 350 };
        let shrinkTimer = 0;
        let kills = 0;

        // Weapon configurations
        const weapons = {
            pistol: {
                name: 'Pistol',
                damage: 15,
                fireRate: 300,
                bulletSpeed: 8,
                bulletSize: 3,
                spread: 0.05,
                color: '#ffff00'
            },
            rifle: {
                name: 'Assault Rifle',
                damage: 20,
                fireRate: 150,
                bulletSpeed: 10,
                bulletSize: 4,
                spread: 0.1,
                color: '#ff8800'
            },
            shotgun: {
                name: 'Shotgun',
                damage: 12,
                fireRate: 800,
                bulletSpeed: 7,
                bulletSize: 5,
                pellets: 6,
                spread: 0.3,
                color: '#ff0000'
            },
            smg: {
                name: 'SMG',
                damage: 10,
                fireRate: 100,
                bulletSpeed: 9,
                bulletSize: 3,
                spread: 0.15,
                color: '#00ffff'
            },
            sniper: {
                name: 'Sniper',
                damage: 60,
                fireRate: 1200,
                bulletSpeed: 15,
                bulletSize: 5,
                spread: 0.02,
                color: '#00ff00'
            }
        };

        // Player class
        class Player {
            constructor(x, y, isAI = false) {
                this.x = x;
                this.y = y;
                this.radius = 15;
                this.health = 100;
                this.maxHealth = 100;
                this.speed = 3;
                this.weapon = null;
                this.lastShot = 0;
                this.isAI = isAI;
                this.color = isAI ? '#ff0000' : '#00ff41';
                this.targetEnemy = null;
                this.moveTimer = 0;
                this.targetX = x;
                this.targetY = y;
            }

            update() {
                if (this.isAI) {
                    this.updateAI();
                } else {
                    this.updatePlayer();
                }

                // Check if outside safe zone
                const dist = Math.hypot(this.x - safeZone.x, this.y - safeZone.y);
                if (dist > safeZone.radius) {
                    const damage = 0.3;
                    this.health -= damage;

                    if (!this.isAI) {
                        document.getElementById('zoneDamage').textContent = damage.toFixed(1);
                    }
                } else if (!this.isAI) {
                    document.getElementById('zoneDamage').textContent = '0';
                }
            }

            updatePlayer() {
                // Movement
                if (keys['w'] || keys['ArrowUp']) this.y -= this.speed;
                if (keys['s'] || keys['ArrowDown']) this.y += this.speed;
                if (keys['a'] || keys['ArrowLeft']) this.x -= this.speed;
                if (keys['d'] || keys['ArrowRight']) this.x += this.speed;

                // Boundary
                this.x = Math.max(this.radius, Math.min(canvas.width - this.radius, this.x));
                this.y = Math.max(this.radius, Math.min(canvas.height - this.radius, this.y));

                // Auto-fire if mouse down
                if (mouse.down && this.weapon) {
                    this.shoot(mouse.x, mouse.y);
                }
            }

            updateAI() {
                this.moveTimer++;

                // Find nearest enemy (player or other AI)
                let nearestEnemy = player;
                let nearestDist = Math.hypot(this.x - player.x, this.y - player.y);

                enemies.forEach(enemy => {
                    if (enemy !== this) {
                        const dist = Math.hypot(this.x - enemy.x, this.y - enemy.y);
                        if (dist < nearestDist) {
                            nearestEnemy = enemy;
                            nearestDist = dist;
                        }
                    }
                });

                // Decide on movement target
                const distToZoneCenter = Math.hypot(this.x - safeZone.x, this.y - safeZone.y);

                if (this.moveTimer > 60 || distToZoneCenter > safeZone.radius * 0.8) {
                    this.moveTimer = 0;

                    if (distToZoneCenter > safeZone.radius * 0.8) {
                        // Move towards safe zone
                        const angle = Math.atan2(safeZone.y - this.y, safeZone.x - this.x);
                        this.targetX = this.x + Math.cos(angle) * 100;
                        this.targetY = this.y + Math.sin(angle) * 100;
                    } else {
                        // Random movement within zone
                        const angle = Math.random() * Math.PI * 2;
                        const dist = Math.random() * 100;
                        this.targetX = this.x + Math.cos(angle) * dist;
                        this.targetY = this.y + Math.sin(angle) * dist;
                    }
                }

                // Move towards target
                const dx = this.targetX - this.x;
                const dy = this.targetY - this.y;
                const dist = Math.hypot(dx, dy);

                if (dist > 5) {
                    this.x += (dx / dist) * this.speed * 0.8;
                    this.y += (dy / dist) * this.speed * 0.8;
                }

                // Keep in bounds
                this.x = Math.max(this.radius, Math.min(canvas.width - this.radius, this.x));
                this.y = Math.max(this.radius, Math.min(canvas.height - this.radius, this.y));

                // Shoot at nearest enemy
                if (nearestDist < 300 && Math.random() < 0.05) {
                    this.shoot(nearestEnemy.x, nearestEnemy.y);
                }
            }

            shoot(targetX, targetY) {
                const now = Date.now();
                if (now - this.lastShot < this.weapon.fireRate) return;

                this.lastShot = now;
                const angle = Math.atan2(targetY - this.y, targetX - this.x);

                const pellets = this.weapon.pellets || 1;

                for (let i = 0; i < pellets; i++) {
                    const spread = (Math.random() - 0.5) * this.weapon.spread;
                    const bulletAngle = angle + spread;

                    bullets.push({
                        x: this.x,
                        y: this.y,
                        vx: Math.cos(bulletAngle) * this.weapon.bulletSpeed,
                        vy: Math.sin(bulletAngle) * this.weapon.bulletSpeed,
                        damage: this.weapon.damage,
                        size: this.weapon.bulletSize,
                        owner: this,
                        color: this.weapon.color
                    });
                }
            }

            draw() {
                // Draw player
                ctx.fillStyle = this.color;
                ctx.beginPath();
                ctx.arc(this.x, this.y, this.radius, 0, Math.PI * 2);
                ctx.fill();

                // Draw health bar
                const barWidth = this.radius * 2;
                const barHeight = 4;
                ctx.fillStyle = '#ff0000';
                ctx.fillRect(this.x - barWidth/2, this.y - this.radius - 10, barWidth, barHeight);
                ctx.fillStyle = '#00ff00';
                ctx.fillRect(this.x - barWidth/2, this.y - this.radius - 10, barWidth * (this.health / this.maxHealth), barHeight);
            }
        }

        // Input handling
        const keys = {};
        const mouse = { x: 0, y: 0, down: false };

        window.addEventListener('keydown', e => keys[e.key] = true);
        window.addEventListener('keyup', e => keys[e.key] = false);

        canvas.addEventListener('mousemove', e => {
            const rect = canvas.getBoundingClientRect();
            mouse.x = e.clientX - rect.left;
            mouse.y = e.clientY - rect.top;
        });

        canvas.addEventListener('mousedown', () => mouse.down = true);
        canvas.addEventListener('mouseup', () => mouse.down = false);

        // Weapon selection
        function selectWeapon(weaponType) {
            player = new Player(canvas.width / 2, canvas.height / 2);
            player.weapon = weapons[weaponType];

            document.getElementById('weaponSelect').style.display = 'none';
            document.getElementById('ui').style.display = 'block';
            document.getElementById('weapon').textContent = player.weapon.name;

            // Create AI enemies
            enemies = [];
            const aiWeapons = Object.keys(weapons);
            for (let i = 0; i < 5; i++) {
                const angle = (i / 5) * Math.PI * 2;
                const dist = 200;
                const enemy = new Player(
                    canvas.width / 2 + Math.cos(angle) * dist,
                    canvas.height / 2 + Math.sin(angle) * dist,
                    true
                );
                enemy.weapon = weapons[aiWeapons[Math.floor(Math.random() * aiWeapons.length)]];
                enemies.push(enemy);
            }

            gameStarted = true;
            gameRunning = true;
            gameLoop();
        }

        // Game loop
        function gameLoop() {
            if (!gameRunning) return;

            ctx.clearRect(0, 0, canvas.width, canvas.height);

            // Update safe zone
            shrinkTimer++;
            if (shrinkTimer > 180) { // Shrink every 3 seconds
                shrinkTimer = 0;
                targetZone.radius = Math.max(100, targetZone.radius * 0.9);
                targetZone.x = canvas.width / 2 + (Math.random() - 0.5) * 100;
                targetZone.y = canvas.height / 2 + (Math.random() - 0.5) * 100;
            }

            // Smoothly move safe zone to target
            safeZone.radius += (targetZone.radius - safeZone.radius) * 0.01;
            safeZone.x += (targetZone.x - safeZone.x) * 0.01;
            safeZone.y += (targetZone.y - safeZone.y) * 0.01;

            // Draw danger zone
            ctx.fillStyle = 'rgba(255, 0, 0, 0.1)';
            ctx.fillRect(0, 0, canvas.width, canvas.height);

            // Draw safe zone
            ctx.fillStyle = 'rgba(15, 52, 96, 0.8)';
            ctx.beginPath();
            ctx.arc(safeZone.x, safeZone.y, safeZone.radius, 0, Math.PI * 2);
            ctx.fill();

            // Draw safe zone border
            ctx.strokeStyle = '#00ff41';
            ctx.lineWidth = 3;
            ctx.beginPath();
            ctx.arc(safeZone.x, safeZone.y, safeZone.radius, 0, Math.PI * 2);
            ctx.stroke();

            // Update and draw bullets
            for (let i = bullets.length - 1; i >= 0; i--) {
                const bullet = bullets[i];
                bullet.x += bullet.vx;
                bullet.y += bullet.vy;

                // Remove if out of bounds
                if (bullet.x < 0 || bullet.x > canvas.width || bullet.y < 0 || bullet.y > canvas.height) {
                    bullets.splice(i, 1);
                    continue;
                }

                // Check collision with player
                if (bullet.owner !== player) {
                    const dist = Math.hypot(bullet.x - player.x, bullet.y - player.y);
                    if (dist < player.radius) {
                        player.health -= bullet.damage;
                        bullets.splice(i, 1);
                        createParticles(bullet.x, bullet.y, bullet.color);
                        continue;
                    }
                }

                // Check collision with enemies
                for (let j = enemies.length - 1; j >= 0; j--) {
                    if (bullet.owner === enemies[j]) continue;

                    const dist = Math.hypot(bullet.x - enemies[j].x, bullet.y - enemies[j].y);
                    if (dist < enemies[j].radius) {
                        enemies[j].health -= bullet.damage;
                        bullets.splice(i, 1);
                        createParticles(bullet.x, bullet.y, bullet.color);

                        if (enemies[j].health <= 0) {
                            if (bullet.owner === player) kills++;
                            enemies.splice(j, 1);
                        }
                        break;
                    }
                }

                // Draw bullet
                ctx.fillStyle = bullet.color;
                ctx.beginPath();
                ctx.arc(bullet.x, bullet.y, bullet.size, 0, Math.PI * 2);
                ctx.fill();
            }

            // Update and draw particles
            for (let i = particles.length - 1; i >= 0; i--) {
                const p = particles[i];
                p.x += p.vx;
                p.y += p.vy;
                p.life--;

                if (p.life <= 0) {
                    particles.splice(i, 1);
                    continue;
                }

                ctx.fillStyle = p.color;
                ctx.globalAlpha = p.life / 30;
                ctx.fillRect(p.x, p.y, 3, 3);
                ctx.globalAlpha = 1;
            }

            // Update and draw player
            if (player) {
                player.update();
                player.draw();
            }

            // Update and draw enemies
            enemies.forEach(enemy => {
                enemy.update();
                enemy.draw();
            });

            // Update UI
            if (player) {
                document.getElementById('health').textContent = Math.max(0, Math.floor(player.health));
                document.getElementById('enemies').textContent = enemies.length;
                document.getElementById('mapSize').textContent = Math.floor((safeZone.radius / 350) * 100);
            }

            // Check game over
            if (player && player.health <= 0) {
                endGame(false);
            } else if (enemies.length === 0) {
                endGame(true);
            } else {
                requestAnimationFrame(gameLoop);
            }
        }

        function createParticles(x, y, color) {
            for (let i = 0; i < 8; i++) {
                particles.push({
                    x: x,
                    y: y,
                    vx: (Math.random() - 0.5) * 4,
                    vy: (Math.random() - 0.5) * 4,
                    life: 30,
                    color: color
                });
            }
        }

        function endGame(won) {
            gameRunning = false;
            document.getElementById('gameOver').style.display = 'block';
            document.getElementById('gameOverText').textContent = won ? 'Victory!' : 'Defeated!';
            document.getElementById('finalStats').textContent = `Kills: ${kills} | Survived: ${Math.floor((Date.now() - gameStartTime) / 1000)}s`;
        }

        let gameStartTime = Date.now();
    </script>
</body>
</html>