<script>
    import { onMount } from 'svelte';
  
    // List of colors
    const colors = ['Red', 'Blue', 'Yellow', 'Green', 'Orange', 'Purple', 'Pink', 'White'];
  
    // Game state
    let gameStarted = false;
    let countdown = 5;
    let currentColorIndex = 0;
    let intervalId;
    let showColor = false;
  
    // Start the game
    function startGame() {
      gameStarted = true;
      currentColorIndex = 0;
      startCountdown();
    }
  
    // Start the countdown
    function startCountdown() {
      countdown = 5;
      showColor = false;
  
      intervalId = setInterval(() => {
        countdown -= 1;
  
        if (countdown === 0) {
          clearInterval(intervalId);
          showColor = true;
  
          // Move to the next color after 2 seconds
          setTimeout(() => {
            if (currentColorIndex < colors.length - 1) {
              currentColorIndex += 1;
              startCountdown();
            } else {
              // End of game
              gameStarted = false;
            }
          }, 2000);
        }
      }, 1000);
    }
  
    // Reset the game
    function resetGame() {
      clearInterval(intervalId);
      gameStarted = false;
      showColor = false;
      countdown = 5;
      currentColorIndex = 0;
    }
  </script>
  
  <main style:background-color={showColor ? colors[currentColorIndex].toLowerCase() : 'white'}>
    <h1>Color Sequence Game</h1>
  
    {#if !gameStarted}
      <button on:click={startGame}>Start Game</button>
    {:else}
      {#if !showColor}
        <h2 style="color: black;">Countdown: {countdown}</h2>
      {:else}
        <h2 style="color: black;">{colors[currentColorIndex]}</h2>
      {/if}
    {/if}
    
  </main>
  
  <style>
    main {
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      height: 100vh;
      font-family: Arial, sans-serif;
      transition: background-color 0.5s ease;
    }
  
    button {
      margin-top: 20px;
      padding: 10px 20px;
      font-size: 16px;
      cursor: pointer;
      background-color: white;
      border: 2px solid black;
      color: black;
    }
  
    h1, h2 {
      color: black;
    }
  </style>