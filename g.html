<!DOCTYPE html>
<html lang="vi">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>RIALO Shooter — HTML5</title>
  <style>
    html, body { height: 100%; margin: 0; background: #0f1420; color: #e5f0ff; font-family: system-ui, -apple-system, Segoe UI, Roboto, Helvetica, Arial, sans-serif; }
    .wrap { display: flex; align-items: center; justify-content: center; height: 100%; }
    canvas { background: #004477; background: linear-gradient(45deg, #003366, #003a6b); border-radius: 16px; box-shadow: 0 10px 30px rgba(0,0,0,.35); width: min(92vw, 520px); height: min(92vh, 780px); touch-action: none; }
    .help { position: fixed; bottom: 14px; left: 50%; transform: translateX(-50%); font-size: 12px; opacity: .8; }
    .help kbd { background: #1c2b45; padding: 2px 6px; border-radius: 6px; box-shadow: inset 0 0 0 1px #21375f; }
  </style>
</head>
<body>
  <div class="wrap">
    <canvas id="game" width="480" height="720" aria-label="RIALO Shooter game canvas"></canvas>
  </div>
  <div class="help">Di chuột để ngắm • Nhấp/Chạm để bắn • Bắn chữ theo thứ tự <strong>R → I → A → L → O</strong> • Nhấn <kbd>Space</kbd> để chơi lại</div>

  <script>
  (function(){
    const canvas = document.getElementById('game');
    const ctx = canvas.getContext('2d');
    const W = canvas.width, H = canvas.height;

    // ---------- Utils ----------
    const clamp = (v,a,b) => Math.max(a, Math.min(b, v));
    const rand = (a,b) => a + Math.random() * (b - a);

    // Circle-rect collision
    function circleRect(cx, cy, cr, rx, ry, rw, rh) {
      const dx = Math.abs(cx - rx);
      const dy = Math.abs(cy - ry);
      if (dx > rw / 2 + cr || dy > rh / 2 + cr) return false;
      if (dx <= rw / 2 || dy <= rh / 2) return true;
      const cx2 = (dx - rw / 2), cy2 = (dy - rh / 2);
      return (cx2 * cx2 + cy2 * cy2) <= cr * cr;
    }

    // ---------- Game state ----------
    const WORD = 'RIALO';
    const lettersPool = WORD.split(''); // Chỉ R, I, A, L, O
    const state = {
      running: false,
      gameOver: false,
      win: false,
      lives: 3,
      progress: 0, // Chữ cần bắn tiếp theo
      time: 0,
      score: 0,
      level: 1,
    };

    const player = {
      x: W / 2, y: H - 64, base: 40, gunLen: 28, cooldown: 0, fireRate: 0.22
    };

    const mouse = { x: W / 2, y: H / 2, down: false };

    const bullets = []; // {x, y, vx, vy, r}
    const targets = []; // {x, y, w, h, vy, txt}

    let spawnTimer = 0;

    // ---------- Input ----------
    function pointerPos(e) {
      const r = canvas.getBoundingClientRect();
      const x = (e.clientX - r.left) * (W / r.width);
      const y = (e.clientY - r.top) * (H / r.height);
      return { x, y };
    }
    canvas.addEventListener('pointermove', (e) => { const p = pointerPos(e); mouse.x = p.x; mouse.y = p.y; });
    canvas.addEventListener('pointerdown', (e) => { mouse.down = true; if (!state.running) startGame(); });
    canvas.addEventListener('pointerup', () => { mouse.down = false; });
    canvas.addEventListener('pointerleave', () => { mouse.down = false; });

    window.addEventListener('keydown', (e) => {
      if (e.code === 'Space') { if (state.gameOver || !state.running) startGame(); }
    });

    // ---------- Core ----------
    function startGame() {
      state.running = true; state.gameOver = false; state.win = false; state.lives = 3; state.progress = 0; state.time = 0; state.score = 0;
      bullets.length = 0; targets.length = 0; spawnTimer = 0; player.cooldown = 0; player.x = W / 2;
      if (state.level === 2) {
        state.level = 2;
        state.time = 0;
        state.score = 0;
      }
    }

    function fire() {
      if (player.cooldown > 0) return;
      player.cooldown = player.fireRate;
      // Hướng bắn từ nòng súng đến con trỏ
      let dx = mouse.x - player.x; let dy = mouse.y - player.y;
      const len = Math.hypot(dx, dy) || 1;
      dx /= len; dy /= len;
      // Luôn bắn lên
      if (dy > -0.2) dy = -0.2;
      const speed = 520;
      bullets.push({ x: player.x, y: player.y - 20, vx: dx * speed, vy: dy * speed, r: 6 });
    }

    function spawnTarget() {
      const txt = lettersPool[(Math.random() * lettersPool.length) | 0];
      const w = 48, h = 48;
      const x = rand(30, W - 30);
      const vy = 70 + Math.min(220, state.time * 6);
      targets.push({ x, y: -h, w, h, vy, txt });
    }

    function collideAndResolve() {
      // Bullet vs Target
      for (let bi = bullets.length - 1; bi >= 0; bi--) {
        const b = bullets[bi];
        for (let ti = targets.length - 1; ti >= 0; ti--) {
          const t = targets[ti];
          if (circleRect(b.x, b.y, b.r, t.x, t.y, t.w, t.h)) {
            // Loại bỏ viên đạn và mục tiêu
            bullets.splice(bi, 1); bi = -1; // break outer
            targets.splice(ti, 1);

            const nextChar = WORD[state.progress];
            if (t.txt.toUpperCase() === nextChar) {
              state.progress++;
              state.score += 100;
              if (state.progress === WORD.length) {
                // Display "YOU WIN" and level up
                state.win = true; state.gameOver = true; state.running = false;
                setTimeout(() => {
                  state.level = 2; // Chuyển sang level 2
                  state.progress = 0;
                  state.score = 0;
                  spawnTimer = 0;
                  startGame();
                }, 2000); // Delay 2s để hiển thị "YOU WIN"
              }
            } else {
              // Bắn nhầm chữ
              state.lives--; flash(200);
              if (state.lives <= 0) { state.gameOver = true; state.running = false; }
            }
            break;
          }
        }
      }

      // Remove targets that fall off the screen (without losing lives)
      for (let ti = targets.length - 1; ti >= 0; ti--) {
        const t = targets[ti];
        if (t.y - t.h / 2 > H + 40) {
          // Chỉ bỏ qua mà không mất mạng
          targets.splice(ti, 1);
        }
      }
    }

    // Screen flash when wrong
    let flashTimer = 0;
    function flash(ms) { flashTimer = ms / 1000; }

    // ---------- Rendering helpers ----------
    function drawRoundedRect(x, y, w, h, r) {
      const rr = Math.min(r, w / 2, h / 2);
      ctx.beginPath();
      ctx.moveTo(x - w / 2 + rr, y - h / 2);
      ctx.arcTo(x + w / 2, y - h / 2, x + w / 2, y + h / 2, rr);
      ctx.arcTo(x + w / 2, y + h / 2, x - w / 2, y + h / 2, rr);
      ctx.arcTo(x - w / 2, y + h / 2, x - w / 2, y - h / 2, rr);
      ctx.arcTo(x - w / 2, y - h / 2, x + w / 2, y - h / 2, rr);
      ctx.closePath();
      ctx.fill();
    }

    function glowText(text, x, y, size = 28, color = '#e5f0ff', align = 'center') {
      ctx.font = `700 ${size}px system-ui, -apple-system, Segoe UI, Roboto, Helvetica, Arial`;
      ctx.textAlign = align; ctx.textBaseline = 'middle';
      ctx.fillStyle = 'rgba(229,240,255,0.95)';
      ctx.shadowColor = color; ctx.shadowBlur = 18; ctx.fillText(text, x, y); ctx.shadowBlur = 0;
    }

    function drawHeart(x, y) {
      ctx.save();
      ctx.translate(x, y); ctx.scale(0.9, 0.9); ctx.fillStyle = '#ff7b8a';
      ctx.beginPath(); ctx.moveTo(0, -6);
      ctx.bezierCurveTo(4, -18, 22, -18, 22, 0);
      ctx.bezierCurveTo(22, 14, 12, 20, 0, 28);
      ctx.bezierCurveTo(-12, 20, -22, 14, -22, 0);
      ctx.bezierCurveTo(-22, -18, -4, -18, 0, -6);
      ctx.closePath(); ctx.fill();
      ctx.restore();
    }

    // ---------- Loop ----------
    let last = performance.now();
    function loop(now) {
      const dt = Math.min(0.033, (now - last) / 1000); last = now;

      // Update
      if (state.running && !state.gameOver) {
        state.time += dt; player.cooldown = Math.max(0, player.cooldown - dt);

        // Player follow mouse a bit smooth
        const lerp = 0.18; player.x += (mouse.x - player.x) * lerp;
        player.x = clamp(player.x, 24, W - 24);
        if (mouse.down) fire();

        // Spawn targets
        const interval = 0.9 - Math.min(0.55, state.time * 0.01);
        spawnTimer += dt; if (spawnTimer >= interval) { spawnTimer = 0; spawnTarget(); }

        // Move targets
        for (let i = targets.length - 1; i >= 0; i--) {
          const t = targets[i]; t.y += t.vy * dt;
          if (t.y - t.h / 2 > H + 40) {
            // Rơi khỏi màn hình → không mất mạng
            targets.splice(i, 1);
          }
        }

        // Move bullets
        for (let i = bullets.length - 1; i >= 0; i--) {
          const b = bullets[i]; b.x += b.vx * dt; b.y += b.vy * dt;
          if (b.x < -20 || b.x > W + 20 || b.y < -30 || b.y > H + 30) bullets.splice(i, 1);
        }

        collideAndResolve();
      }

      // Render
      ctx.clearRect(0, 0, W, H);

      // Subtle stars
      ctx.save(); ctx.globalAlpha = 0.12; ctx.fillStyle = '#9cc2ff';
      for (let i = 0; i < 60; i++) { const x = (i * 79 + (last * 0.03) % W) % W, y = (i * 131 + (last * 0.05) % H) % H; ctx.fillRect(x, y, 2, 2); }
      ctx.restore();

      // Targets (letter blocks)
      for (const t of targets) {
        ctx.fillStyle = '#ffb86b';
        drawRoundedRect(t.x, t.y, t.w, t.h, 10);
        glowText(t.txt, t.x, t.y + 2, 28, '#fff');
      }

      // Bullets
      ctx.fillStyle = '#74f0a7';
      for (const b of bullets) { ctx.beginPath(); ctx.arc(b.x, b.y, b.r, 0, Math.PI * 2); ctx.fill(); }

      // Player base & barrel
      ctx.fillStyle = '#6ee7ff'; drawRoundedRect(player.x, player.y, player.base, 18, 8);

      // Gun direction (barrel)
      let dx = mouse.x - player.x, dy = mouse.y - player.y; const len = Math.hypot(dx, dy) || 1;
      dx /= len; dy /= len; if (dy > -0.15) dy = -0.15;
      const bx1 = player.x + dx * 10, by1 = player.y + dy * 10;
      const bx2 = player.x + dx * (player.gunLen + 14), by2 = player.y + dy * (player.gunLen + 14);
      ctx.strokeStyle = '#6ee7ff'; ctx.lineWidth = 6; ctx.lineCap = 'round';
      ctx.beginPath(); ctx.moveTo(bx1, by1); ctx.lineTo(bx2, by2); ctx.stroke();

      // UI: word progress
      const gap = 38; const startX = W / 2 - (WORD.length - 1) * gap / 2; const y = 34;
      for (let i = 0; i < WORD.length; i++) {
        const ch = WORD[i]; const color = (i < state.progress ? '#74f0a7' : (i === state.progress ? '#e5f0ff' : '#96a2b8'));
        glowText(ch, startX + i * gap, y, 26, color);
      }

      // Lives
      for (let i = 0; i < state.lives; i++) { drawHeart(28 + i * 24, 32); }

      // Flash overlay
      if (flashTimer > 0) { flashTimer -= dt; ctx.save(); ctx.fillStyle = 'rgba(255,70,70,0.18)'; ctx.fillRect(0, 0, W, H); ctx.restore(); }

      // Title / status
      if (!state.running) {
        ctx.save(); ctx.fillStyle = 'rgba(0,0,0,.45)'; ctx.fillRect(0, 0, W, H); ctx.restore();
        glowText('RIALO Shooter', W / 2, H / 2 - 52, 42);
        if (state.gameOver && state.win) { glowText('Hoàn thành từ RIALO! ✨', W / 2, H / 2, 22); }
        else if (state.gameOver) { glowText('Hết mạng rồi 😅', W / 2, H / 2, 22); }
        else { glowText('Bắn các chữ theo đúng thứ tự', W / 2, H / 2, 20); }
        glowText('Nhấp chuột hoặc nhấn Space để chơi', W / 2, H / 2 + 42, 16);
      }

      requestAnimationFrame(loop);
    }

    // kickoff
    requestAnimationFrame((t) => { last = t; loop(t); });

    // Start on first click/space
    canvas.addEventListener('pointerdown', () => { if (!state.running) startGame(); }, { once: true });
    window.addEventListener('keydown', (e) => { if (e.code === 'Space' && !state.running) startGame(); }, { once: true });
  })();
  </script>
</body>
</html>
