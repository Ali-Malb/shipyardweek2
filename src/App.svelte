<script>
  let started = false;
  let distractions = 0;
  let passivedistractions = 1;
  let upgradeCost = 10;
  let upgradeCount = 0;
  let workclicks = 0;
  /**
   @type {any[]}
   */
  let brainrotpopups=[];
  setInterval(function(){
    if (started){
      distractions = distractions + passivedistractions
    }
  }, 1000);

  function buyupgrade() {
    if (distractions>=upgradeCost) {
      distractions = distractions - upgradeCost
      passivedistractions +=1
      upgradeCount +=1
      upgradeCost = Math.floor(upgradeCost*1.5)
    }
  }
  function startWorking () {
    started = true
    distractions  = distractions + 1 
    workclicks +=1
  }
  function openTikTok () {
    distractions  +=5
    brainrotpopups = [...brainrotpopups, {
      id: Math.random(),
      top:Math.floor(Math.random()*60)+10,
      left: Math.floor(Math.random()*70)+10
    }];
  }
  function openYT () {
    distractions +=3
  }
</script>
<main>
<h1> The Procrrastination Machine. started: {started}</h1>
<div class="status-board">
{#if started}
  <h2>Your now procrastinating</h2>
  {:else}   
  <h2>Ready to focus?</h2>
{/if}
<h2 class="score">proctastinations: {distractions}</h2>
<h3>Passive Brain Rot: {passivedistractions} per second</h3>
</div>

<div class="actions">
  <button class="primary" on:click={startWorking}>start working </button>
{#if workclicks >=5}
  <button on:click={openYT}>Open YT</button>
{/if}
{#if workclicks >=50}
  <button on:click={openTikTok}>Open Tiktok</button>
{/if}
</div>

{#if started}
<div class="shop">
  <button class="upgrade" on:click={buyupgrade}>Upgrade passive distractions | Upgrade Cost {upgradeCost} | Owned: {upgradeCount}</button>
</div>
{/if}
</main>
{#each brainrotpopups as popup}
  <div class="floating-video" style="top: {popup.top}%; left: {popup.left}%;">
    <div class="tiktok-logo">🎵 TikTok</div>
    <iframe 
      src="https://www.youtube.com/embed/X2q7X7q9pC4?autoplay=1&mute=1&loop=1&controls=0" 
      title="Brainrot" 
      frameborder="0" 
      allow="autoplay; encrypted-media">
    </iframe>
  </div>
{/each}
<!-- Used AI for CSS and video logic-->
<style>
  /* Centers everything and sets a dark gaming aesthetic */
  :global(body) {
    background-color: #0d0d12;
    color: #e0e0e0;
    font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
    margin: 0;
    display: flex;
    justify-content: center;
    align-items: center;
    min-height: 100vh;
  }

  main {
    background: #1a1a24;
    padding: 2rem 3rem;
    border-radius: 12px;
    box-shadow: 0 8px 32px rgba(0, 0, 0, 0.5);
    text-align: center;
    max-width: 500px;
    width: 100%;
    border: 1px solid #2a2a35;
  }

  h1 {
    color: #ffffff;
    font-size: 2rem;
    margin-bottom: 1.5rem;
    text-transform: uppercase;
    letter-spacing: 2px;
  }

  .status-board {
    background: #000000;
    padding: 1.5rem;
    border-radius: 8px;
    margin-bottom: 2rem;
    border-left: 4px solid #ff2a2a;
  }

  h2 {
    margin: 0.5rem 0;
    font-size: 1.2rem;
    color: #a0a0b0;
  }

  h2.active {
    color: #ff2a2a;
  }

  .score span {
    font-size: 2rem;
    color: #ffffff;
    font-weight: bold;
  }

  h3 {
    color: #00ffcc;
    font-size: 1rem;
    margin-top: 1rem;
  }

  .actions {
    display: flex;
    flex-direction: column;
    gap: 10px;
    margin-bottom: 2rem;
  }

  /* Button Styling */
  button {
    background: #2a2a35;
    color: white;
    border: none;
    padding: 12px 20px;
    font-size: 1rem;
    font-weight: bold;
    border-radius: 6px;
    cursor: pointer;
    transition: all 0.2s ease;
    text-transform: uppercase;
  }

  button:hover {
    background: #3a3a4a;
    transform: translateY(-2px);
  }

  button:active {
    transform: translateY(1px);
  }

  button.primary {
    background: #ff2a2a;
    color: #fff;
    padding: 16px;
    font-size: 1.2rem;
  }

  button.primary:hover {
    background: #ff4a4a;
    box-shadow: 0 0 15px rgba(255, 42, 42, 0.4);
  }

  .shop button.upgrade {
    width: 100%;
    background: #ffd700;
    color: #000;
    padding: 15px;
  }

  .shop button.upgrade:hover {
    background: #ffea00;
  }
  
  small {
    display: block;
    margin-top: 5px;
    font-size: 0.8rem;
    opacity: 0.8;
  }
/* Makes the videos float on top of the screen */
  .floating-video {
    position: fixed;
    width: 250px;
    height: 400px;
    background: #000;
    border: 3px solid #ff0050; 
    border-radius: 12px;
    z-index: 100;
    box-shadow: 0 10px 30px rgba(0,0,0,0.8);
    pointer-events: none; /* Lets you click through the video to hit your buttons! */
  }

  .tiktok-logo {
    position: absolute;
    top: 10px;
    left: 10px;
    background: rgba(0,0,0,0.7);
    color: white;
    padding: 5px 10px;
    border-radius: 20px;
    font-weight: bold;
    font-size: 0.8rem;
    z-index: 101;
  }

  .floating-video iframe {
    width: 100%;
    height: 100%;
    pointer-events: none;
  }</style>