<script>
  import Scrolly from "./Scrolly.svelte";
  import { select } from "d3-selection";
  import Coleco from "./Coleco.svelte";
  import Intellivision from "./Intellivision.svelte";
  // Scroll iterator
  let value = 0;

  // Paragraph text for scrolly
  $: steps = [
    `<h1 class='step-title'>Second Generation</h1>
      <p>
        The second generation of consoles marked the beginning of home gaming. Key consoles in this era include:
        <ul>
          <li class="tooltip" data-title="Atari 2600" data-img="images/gen2/a2600.jpeg">
          Atari 2600
          </li>
          <li class="tooltip" data-title="Intellivision" data-img="images/gen2/iv.jpeg">
           Intellivision
          </li>
          <li class="tooltip" data-title="Game & Watch" data-img="images/gen2/gw.jpeg">
           Game & Watch
          </li>
          <li class="tooltip" data-title="ColecoVision" data-img="images/gen2/cv.jpeg">
           ColecoVision
          </li>
          <li class="tooltip" data-title=">Atari 5200" data-img="images/gen2/a5200.jpeg">
            Atari 5200
          </li>
        </ul>
      </p>`,
    `<h1 class='step-title'> Atari 2600 </h1>
      <p>
        Atari 2600 was developed by Atari Inc., and was released in September 
        1977. The game Pacman first appeared on this system. However, the poor 
        managerial decisions from the Atari corporation damaged the repuration 
        of both the console and the company, which eventually led to the 
        videogame crash in 1983.
      </p>`,
    `<h1 class='step-title'> Intellivision </h1>
      <p>
        Intellivision was developed by Mattel Electronics and was released in 
        late 1979. It had a Gi chipset in the console, but had reliability 
        issues because the chips needed three different supply voltages to work. 
        Overheating was a major issue for Intellivision, but nevertheless it 
        still posed a major challenge to companies like Atari.
      </p>`,
    `<h1 class='step-title'> Game & Watch </h1>
      <p>
        Game & Watch was developed by Nintendo and was released on April 28, 
        1980. It was mainly the idea of designer Gunpei Yokoi, who thought of 
        the idea when he was playing with an LCD calculator on the Shinkansen. 
        The first game on Game & Watch, Ball, was a major game hit in the 
        Nintendo gaming industry.
      </p>`,
    `<h1 class='step-title'> ColecoVision </h1>
      <p>
        Colecovision was developed by CBS Electronics, and was released in 
        August 1982. Coleco almost became bankrupt while developing this game 
        console, but eventually got the job done. In fact, this was the console 
        where Donkey Kong first appears in. 
      </p>`,
    `<h1 class='step-title'> Atari 5200 </h1>
      <p>
        Atari 5200 was developed by Atari Inc., and was released in November 
        1982. It had a controller with an analog joystick on the controller. 
        This was one of the major points of criticism for the product, as it 
        failed to translate human action into a linear acceleration. In the end, 
        not many Atari 5200s were sold because of the poor design.
      </p>`
  ];

  // Define images for each step
  const images = [
    {
      consoles: [
        "images/gen2/a2600.jpeg",
        "images/gen2/iv.jpeg",
        "images/gen2/gw.jpeg",
        "images/gen2/cv.jpeg",
        "images/gen2/a5200.jpeg"
      ]
    },
    {
      console: "images/gen2/a2600.jpeg",
      games: [
        "images/gen2/a2600_game1.jpeg",
        "images/gen2/a2600_game2.jpeg",
        "images/gen2/a2600_game3.jpeg"
      ]
    },
    {
      console: "images/gen2/iv.jpeg",
      games: [
        "images/gen2/iv_game1.jpeg",
        "images/gen2/iv_game2.jpeg",
        "images/gen2/iv_game3.jpeg"
      ]
    },
    {
      console: "images/gen2/gw.jpeg",
      games: [
        "images/gen2/gw_game1.jpeg",
        "images/gen2/gw_game2.jpeg",
        "images/gen2/gw_game3.jpeg"
      ]
    },
    {
      console: "images/gen2/cv.jpeg",
      games: [
        "images/gen2/cv_game1.jpeg",
        "images/gen2/cv_game2.jpeg",
        "images/gen2/cv_game3.jpeg"
      ]
    },
    {
      console: "images/gen2/a5200.jpeg",
      games: [
        "images/gen2/a5200_game1.jpeg",
        "images/gen2/a5200_game2.jpeg",
        "images/gen2/a5200_game3.jpeg"
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

<h1 class="body-header">2nd Generation: The Rise of Home Gaming</h1>
<h2 class="body-text">
  As time progresses, more firms step into the game:
</h2>
<div class="company-container">
  <Coleco />
  <Intellivision />
</div>
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

    .company-introduction {
    max-width: 800px;
    margin: 2rem auto;
    padding: 2rem;
    background-color: #f5f5f5;
    border-radius: 10px;
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
    text-align: left;
    }

    .company-container {
    display: flex;
    justify-content: space-around;
    align-items: flex-start;
    margin-bottom: 2rem;
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
