---
layout: post
title:  coin collect 
description: game
type: tangibles
courses: { compsci: {week: 2} }
---
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <style>
    canvas {
      border: 1px solid #000;
    }
  </style>
  <title>Sprite Sheet Game</title>
</head>
<body>
  <canvas id="gameCanvas" width="400" height="200"></canvas>
  <script>
    const canvas = document.getElementById('gameCanvas');
    const ctx = canvas.getContext('2d');
    // Load sprite sheet and coin image
    const characterImage = new Image();
    characterImage.src = '/team-game-real-/images/yuuji-removebg-preview.png'; // Replace with your sprite sheet URL
    const coinImage = new Image();
    coinImage.src = '/team-game-real-/images/cute-pink-bow-png-0-removebg-preview.png'; // Replace with your coin image URL
    // Game state
    let characterX = 50;
    let characterY = 150;
    let coinX = 300;
    let coinY = 150;
    let score = 0;
    // Handle keyboard input
    window.addEventListener('keydown', (e) => {
      // In a real game, you'd handle character movement here
    });
    // Update game state
    function update() {
      // Check for collision between character and coin
      if (
        characterX < coinX + 30 &&
        characterX + 30 > coinX &&
        characterY < coinY + 30 &&
        characterY + 30 > coinY
      ) {
        // Collision detected, increase score and reposition coin
        score += 100;
        coinX = Math.random() * (canvas.width - 30);
        coinY = Math.random() * (canvas.height - 30);
      }
    }
    // Render game objects
    function render() {
      // Clear the canvas
      ctx.clearRect(0, 0, canvas.width, canvas.height);
      // Draw character
      ctx.drawImage(characterImage, characterX, characterY, 30, 30);
      // Draw coin
      ctx.drawImage(coinImage, coinX, coinY, 30, 30);
      // Display score
      ctx.fillStyle = '#000';
      ctx.font = '20px Arial';
      ctx.fillText('Score: ' + score, 10, 20);
    }
    // Main game loop
    function gameLoop() {
      update();
      render();
      requestAnimationFrame(gameLoop);
    }
    // Start the game loop
    gameLoop();
  </script>
</body>
</html>
