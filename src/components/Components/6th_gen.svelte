<script>
  import Scrolly from "./Scrolly.svelte";
  import { select } from "d3-selection";

  // Scroll iterator
  let value = 0;

  // Paragraph text for scrolly
  const steps = [
    `<h1 class='step-title'>Fourth Generation</h1>
      <p>
       The fourth generation of consoles marked significant advancements in gaming. Key consoles in this era include:
       <ul>
         <li class="tooltip" data-title="Sega Genesis/Mega Drive" data-img="/images/console_4_1.jpeg">
           Sega Genesis/Mega Drive
         </li>
         <li class="tooltip" data-title="SNES/Super Famicom" data-img="/images/console_4_2.jpeg">
           SNES/Super Famicom
         </li>
         <li class="tooltip" data-title="Atari Lynx" data-img="/images/console_4_3.jpeg">
           Atari Lynx
         </li>
         <li class="tooltip" data-title="PC Engine/TurboGrafx-16" data-img="/images/console_4_4.jpeg">
           PC Engine/TurboGrafx-16
         </li>
         <li class="tooltip" data-title="PC Engine CD-ROM" data-img="/images/console_4_5.jpeg">
           PC Engine CD-ROM
         </li>
         <li class="tooltip" data-title="Philips CD-i" data-img="/images/console_4_6.jpeg">
           Philips CD-i
         </li>
         <li class="tooltip" data-title="Sega Pico" data-img="/images/console_4_7.jpeg">
           Sega Pico
         </li>
         <li class="tooltip" data-title="Sega Game Gear" data-img="/images/console_4_8.jpeg">
           Sega Game Gear
         </li>
       </ul>
      </p>`,
    `<h1 class='step-title'> Sega Genesis/Mega Drive </h1>
      <p>
        The Sega Genesis/Mega Drive as developed by Sega, and released in 1988 
        to 1989. It had a library of more than 900 games based on its ROM 
        cartridges. However, in Japan, it had poor market performance compared 
        with its competitors, Super Favicom.
      </p>`,
    `<h1 class='step-title'>SNES/Super Famicom</h1>
      <p>
        The SNES was developed by Nintendo and was released across 1990-1992. 
        This console introduced advanced graphics and sound capabilities 
        compared with other gaming consoles released at the same time period. 
        It was the best selling console of the 16-bit era.
      </p>`,
    `<h1 class='step-title'>Atari Lynx</h1>
      <p>
        The Atari Lynx was developed by Atari and was released from 1989-1990. 
        It featured the ability to be daisy-chained for up to 
        8 players at once for unique multiplayer experiences. While Nintendo 
        was clearly the most popular at the time, it still left a mark among 
        the gamers at the time.
      </p>`,
    `<h1 class='step-title'>PC Engine/TurboGrafx-16</h1>
      <p>
      </p>`,
    `<h1 class='step-title'>PC Engine CD-ROM</h1>
      <p>
      </p>`,
    `<h1 class='step-title'>Philips CD-i</h1>
      <p>
      </p>`,
    `<h1 class='step-title'>Sega Pico</h1>
      <p>
      </p>`,
    `<h1 class='step-title'>Sega Game Gear</h1>
      <p>
      </p>`
  ];

  // Define images for each step
  const images = [
    {
      console: null,
      games: null,
      consoles: [
        "images/console_6_1.jpeg",
        "images/console_6_2.jpeg",
        "images/console_6_3.jpeg",
        "images/console_6_4.jpeg",
        "images/console_6_5.jpeg",
        "images/console_6_6.jpeg",
        "images/console_6_7.jpeg",
        "images/console_6_8.jpeg"
      ]
    },
    {
      console: "images/console_6_1.jpeg",
      games: [
        "images/console_6_1_game_1.jpeg",
        "images/console_6_1_game_2.jpeg",
        "images/console_6_1_game_3.jpeg"
      ]
    },
    {
      console: "images/console_8_2.jpeg",
      games: [
        "images/console_6_2_game_1.jpeg",
        "images/console_6_2_game_2.jpeg",
        "images/console_6_2_game_3.jpeg"
      ]
    },
    {
      console: "images/console_8_3.jpeg",
      games: [
        "images/console_6_3_game_1.jpeg",
        "images/console_6_3_game_2.jpeg",
        "images/console_6_3_game_3.jpeg"
      ]
    },
    {
      console: "images/console_8_4.jpeg",
      games: [
        "images/console_6_4_game_1.jpeg",
        "images/console_6_4_game_2.jpeg",
        "images/console_6_4_game_3.jpeg"
      ]
    },
    {
      console: "images/console_8_5.jpeg",
      games: [
        "images/console_6_5_game_1.jpeg",
        "images/console_6_5_game_2.jpeg",
        "images/console_6_5_game_3.jpeg"
      ]
    },
    {
      console: "images/console_8_6.jpeg",
      games: [
        "images/console_6_6_game_1.jpeg",
        "images/console_6_6_game_2.jpeg",
        "images/console_6_6_game_3.jpeg"
      ]
    },
    {
      console: "images/console_8_7.jpeg",
      games: [
        "images/console_6_7_game_1.jpeg",
        "images/console_6_7_game_2.jpeg",
        "images/console_6_7_game_3.jpeg"
      ]
    },
    {
      console: "images/console_8_8.jpeg",
      games: [
        "images/console_6_8_game_1.jpeg",
        "images/console_6_8_game_2.jpeg",
        "images/console_6_8_game_3.jpeg"
      ]
    }

  ];

  $: currentImages = images[value] || images[0];

  // Tooltip content
  let tooltipContent = "";
  let tooltipImage = "";

  function showTooltip(event) {
    tooltipContent  = event.target.getAttribute("data-title");
    tooltipImage = event.target.getAttribute("data-img");
  }

  function hideTooltip() {
    tooltipContent = "";
    tooltipImage = "";
  }
</script>

<h2 class="body-header">4th Generation: The Advancement of Console Gaming</h2>
<p class="body-text">
  The fourth generation of console gaming saw significant advancements and the introduction of iconic gaming systems.
</p>

<section>
  <!-- Scroll container -->
  <div class="section-container">
    <div class="charts-container">
      {#if currentImages.console}
        <div class="console-image">
          <img src={currentImages.console} alt="Console Image" />
        </div>
        <div class="game-images">
          {#if currentImages.games}
            {#each currentImages.games as game, index}
              <img src={game} alt={`Game Image ${index + 1}`} class="game-image" />
            {/each}
          {/if}
        </div>
      {:else}
        <div class="all-consoles">
          {#if Array.isArray(currentImages.consoles)}
            {#each currentImages.consoles as consoleImage, index}
              <img src={consoleImage} alt={`Console ${index + 1}`} class="console-image" />
            {/each}
          {/if}
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
    display: flex;
    flex-wrap: wrap;
    justify-content: space-around;
    width: 100%;
    margin-top: 20px;
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
    width: 80%;
    height: auto;
    margin-bottom: 10px;
  }

  .tooltip-content p {
    margin: 0;
    font-size: 14px;
  }

  .all-consoles {
    position: relative;
    width: 100%;
    height: 500px; /* Adjust as necessary */
    margin-top: 20px;
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
    left: 35%;
  }

  .all-consoles img:nth-child(3) {
    top: 0;
    left: 60%;
  }

  .all-consoles img:nth-child(4) {
    top: 50%;
    left: 5%;
    transform: translateY(-50%);
  }

  .all-consoles img:nth-child(5) {
    top: 50%;
    left: 35%;
    transform: translateY(-50%);
  }

  .all-consoles img:nth-child(6) {
    top: 50%;
    left: 60%;
    transform: translateY(-50%);
  }

  .all-consoles img:nth-child(7) {
    bottom: 0;
    left: 25%;
    transform: translateY(50%);
  }

  .all-consoles img:nth-child(8) {
    bottom: 0;
    left: 50%;
    transform: translateY(50%);
  }
</style>
