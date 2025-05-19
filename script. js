const canvas = document.getElementById("gameCanvas");
  const ctx = canvas.getContext("2d");

  let bird, pipes, score, gameOver, frame;

  const pipeWidth = 50;
  const pipeGap = 120;

  function initGame() {
    bird = {
      x: 50,
      y: 150,
      width: 40,
      height: 30,
      gravity: 0.6,
      lift: -10,
      velocity: 0
    };
    pipes = [];
    score = 0;
    gameOver = false;
    frame = 0;

    document.getElementById("scoreDisplay").innerText = "0";
    document.getElementById("gameOverPanel").classList.add("d-none");
  }

  function drawBird() {
    const birdImg = document.getElementById("birdImg");
    ctx.drawImage(birdImg, bird.x, bird.y, bird.width, bird.height);
  }

  function drawPipe(pipe) {
    ctx.fillStyle = "green";
    ctx.fillRect(pipe.x, 0, pipeWidth, pipe.top);
    ctx.fillRect(pipe.x, pipe.bottom, pipeWidth, canvas.height - pipe.bottom);
  }

  function updateBird() {
    bird.velocity += bird.gravity;
    bird.y += bird.velocity;

    if (bird.y + bird.height > canvas.height || bird.y < 0) {
      gameOver = true;
    }
  }

  function updatePipes() {
    if (frame % 90 === 0) {
      const top = Math.random() * (canvas.height / 2);
      const bottom = top + pipeGap;
      pipes.push({ x: canvas.width, top, bottom });
    }

    pipes.forEach((pipe) => {
      pipe.x -= 2;

      if (
        bird.x + bird.width > pipe.x &&
        bird.x < pipe.x + pipeWidth &&
        (bird.y < pipe.top || bird.y + bird.height > pipe.bottom)
      ) {
        gameOver = true;
      }

      if (pipe.x + pipeWidth === bird.x) {
        score++;
        document.getElementById("scoreDisplay").innerText = score;
      }
    });

    pipes = pipes.filter(pipe => pipe.x + pipeWidth > 0);
  }

  function gameLoop() {
    ctx.clearRect(0, 0, canvas.width, canvas.height);

    if (!gameOver) {
      updateBird();
      updatePipes();
      drawBird();
      pipes.forEach(drawPipe);
      frame++;
      requestAnimationFrame(gameLoop);
    } else {
      document.getElementById("gameOverPanel").classList.remove("d-none");
      document.getElementById("finalScore").textContent = score;
    }
  }

  document.addEventListener("keydown", () => {
    if (!gameOver) {
      bird.velocity = bird.lift;
    }
  });

  function restartGame() {
    initGame();
    gameLoop();
  }

  // Mulai game saat halaman dibuka
  initGame();
  gameLoop();
