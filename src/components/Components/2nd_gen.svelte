<script>
  import Scrolly from "./Scrolly.svelte";
  import { select } from "d3-selection";

  // Scroll iterator
  let value = 0;

  // Paragraph text for scrolly
  $: steps = [
    `<h1 class='step-title'>Second Generation</h1>
      <p>
       The second generation of consoles marked the beginning of home gaming. Key consoles in this era include:
       <ul>
         <li class="tooltip" data-title="Game & Watch" data-img="/images/console_2_1.jpeg">
          Game & Watch
         </li>
         <li class="tooltip" data-title="Atari 2600" data-img="/images/console_2_2.jpeg">
          Atari 2600
         </li>
         <li class="tooltip" data-title=">Atari 5200" data-img="/images/console_2_3.jpeg">
           ColecoVision
         </li>
         <li class="tooltip" data-title="Intellivision" data-img="/images/console_2_4.jpeg">
          Intellivision
         </li>
         <li class="tooltip" data-title="ColecoVision" data-img="/images/console_2_5.jpeg">
          ColecoVision
         </li>
       </ul>
      </p>`,
    `<h1 class='step-title'>Game & Watch/h1>
      <p>
      </p>`,
    `<h1 class='step-title'>Atari 2600</h1>
      <p>
      </p>`,
    `<h1 class='step-title'>Atari 5200</h1>
      <p>
      </p>`,
    `<h1 class='step-title'>Intellivision</h1>
      <p>
      </p>`,
    `<h1 class='step-title'>ColecoVision</h1>
      <p>
      </p>`
  ];

  // Define images for each step
  const images = [
    {
      consoles: [
        "images/console_2_1.jpeg",
        "images/console_2_2.jpeg",
        "images/console_2_3.jpeg",
        "images/console_2_4.jpeg",
        "images/console_2_5.jpeg"
      ]
    },
    {
      console: "images/console_2_1.jpeg",
      games: [
        "images/console_2_1_game_1.jpeg",
        "images/console_2_1_game_2.jpeg",
        "images/console_2_1_game_3.jpeg"
      ]
    },
    {
      console: "images/console_2_2.jpeg",
      games: [
        "images/console_2_2_game_1.jpeg",
        "images/console_2_2_game_2.jpeg",
        "images/console_2_2_game_3.jpeg"
      ]
    },
    {
      console: "images/console_2_3.jpeg",
      games: [
        "images/console_2_2_game_1.jpeg",
        "images/console_2_2_game_2.jpeg",
        "images/console_2_2_game_3.jpeg"
      ]
    },
    {
      console: "images/console_2_4.jpeg",
      games: [
        "images/console_2_4_game_1.jpeg",
        "images/console_2_4_game_2.jpeg",
        "images/console_2_4_game_3.jpeg"
      ]
    },
    {
      console: "images/console_2_5.jpeg",
      games: [
        "images/console_2_5_game_1.jpeg",
        "images/console_2_5_game_2.jpeg",
        "images/console_2_5_game_3.jpeg"
      ]
    }
  ];

  $: currentImages = images[value] || images[0];

  // Tooltip content
  let tooltipContent = "";
  let tooltipImage = "";

  function showTooltip(event) {
    tooltipContent = event.target.getAttribute("data-title");
    tooltipImage = event.target.getAttribute("data-img");
  }

  function hideTooltip() {
    tooltipContent = "";
    tooltipImage = "";
  }
</script>

<h2 class="body-header">2nd Generation: The Rise of Home Gaming</h2>
<p class="body-text">
  This is the second generation of gaming consoles.
</p>
<section>
  <!-- Scroll container -->
  <div class="section-container">
    <div class="charts-container">
      {#if value === 0}
        <div class="all-consoles">
          {#if currentImages.consoles && currentImages.consoles[0]}<img src={currentImages.consoles[0]} alt="Console 1" class="console-image" />{/if}
          {#if currentImages.consoles && currentImages.consoles[1]}<img src={currentImages.consoles[1]} alt="Console 2" class="console-image" />{/if}
          {#if currentImages.consoles && currentImages.consoles[2]}<img src={currentImages.consoles[2]} alt="Console 3" class="console-image" />{/if}
          {#if currentImages.consoles && currentImages.consoles[3]}<img src={currentImages.consoles[3]} alt="Console 4" class="console-image" />{/if}
          {#if currentImages.consoles && currentImages.consoles[4]}<img src={currentImages.consoles[4]} alt="Console 5" class="console-image" />{/if}
        </div>
      {:else}
        <div class="console-image">
          <img src={currentImages.console} alt="Console Image" />
        </div>
        <div class="game-images">
          {#if currentImages.games && currentImages.games[0]}<img src={currentImages.games[0]} alt="Game Image 1" class="game-image" />{/if}
          {#if currentImages.games && currentImages.games[1]}<img src={currentImages.games[1]} alt="Game Image 2" class="game-image" />{/if}
          {#if currentImages.games && currentImages.games[2]}<img src={currentImages.games[2]} alt="Game Image 3" class="game-image" />{/if}
        </div>
      {/if}
    </div>
    <div class="steps-container">
      <Scrolly bind:value>
        {#each steps as text, i}
          <div class="step" class:active={value === i} on:mouseover={showTooltip} on:mouseout={hideTooltip}>
            <div class="step-content">{@html text}</div>
          </div>
        {/each}
        <div class="spacer" />
      </Scrolly>
    </div>
  </div>
  <br /><br />
</section>

{#if tooltipContent}
  <div class="tooltip-container">
    <div class="tooltip-content">
      <img src={tooltipImage} alt="Console Image" />
      <p>{tooltipContent}</p>
    </div>
  </div>
{/if}

<style>
  body {
    background: no-repeat center center fixed;
    background-size: cover;
  }

  .charts-container {
    position: sticky;
    top: 10%;
    display: flex;
    flex-direction: column;
    align-items: center;
    width: 50%;
    height: 85vh;
    border: 3px solid black;
  }

  .console-image img,
  .game-images img,
  .all-consoles img {
    max-width: 100%;
    height: auto;
  }

  .game-images {
    display: flex;
    justify-content: space-around;
    width: 100%;
    margin-top: 20px;
  }

  .game-image {
    width: 200px; /* Adjust as necessary */
    height: 280px; /* Adjust as necessary */
  }

  .all-consoles {
    display:
    flex;
      justify-content: space-around;
      width: 100%;
      margin-top: 20px;
      position: relative;
      height: 500px; /* Adjust as necessary */
    }
  
    .all-consoles img {
      position: absolute;
      width: 30%; /* Adjust as necessary */
      height: auto;
    }
  
    .all-consoles img:nth-child(1) {
      top: 0;
      left: 10%;
    }
  
    .all-consoles img:nth-child(2) {
      top: 0;
      right: 10%;
    }
  
    .all-consoles img:nth-child(3) {
      bottom: 10%;
      left: 5%;
    }
  
    .all-consoles img:nth-child(4) {
      bottom: 10%;
      right: 5%;
    }
  
    .all-consoles img:nth-child(5) {
      bottom: 0;
      left: 50%;
      transform: translateX(-50%);
    }
  
    .section-container {
      margin-top: 1em;
      text-align: center;
      transition: background 100ms;
      display: flex;
    }
  
    .step {
      height: 110vh;
      display: flex;
      place-items: center;
      justify-content: center;
    }
  
    .step-content {
      font-size: 18px;
      background: rgba(255, 255, 255, 0.8); /* Semi-transparent background */
      color: #000;
      border-radius: 1px;
      padding: 0.5rem 1rem;
      display: flex;
      flex-direction: column;
      justify-content: center;
      transition: background 500ms ease;
      text-align: left;
      width: 75%;
      margin: auto;
      max-width: 500px;
      font-family: var(--font-main);
      line-height: 1.3;
      border: 5px solid var(--default);
    }
  
    .step.active .step-content {
      background: rgba(255, 255, 255, 1); /* Fully opaque background */
      color: var(--squid-ink);
    }
  
    .steps-container {
      height: 100%;
    }
  
    .steps-container {
      flex: 1 1 40%;
      z-index: 10;
    }
  
    .tooltip-container {
      position: absolute;
      background-color: #333;
      color: #fff;
      padding: 10px;
      border-radius: 5px;
      box-shadow: 0 2px 5px rgba(0, 0, 0, 0.3);
      z-index: 1000;
      width: 250px;
      top: 50%;
      left: 50%;
      transform: translate(-50%, -50%);
    }
  
    .tooltip-content img {
      width: 100%;
      height: auto;
      margin-bottom: 10px;
    }
  
    .tooltip-content p {
      margin: 0;
      font-size: 14px;
    }
  </style>
  
  {#if tooltipContent}
    <div class="tooltip-container">
      <div class="tooltip-content">
        <img src={tooltipImage} alt="Console Image" />
        <p>{tooltipContent}</p>
      </div>
    </div>
  {/if}