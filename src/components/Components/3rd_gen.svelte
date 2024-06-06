<script>
    import Scrolly from "./Scrolly.svelte";
    import { select } from "d3-selection";
    import Sega from "./Sega.svelte";

    // Scroll iterator
    let value = 0;
  
    // Paragraph text for scrolly
    $: steps = [
      `<h1 class='step-title'>Third Generation</h1>
        <p>
          The third generation of consoles marked a significant advancement in 
          gaming. Key consoles in this era include:
          <ul>
            <li class="tooltip" data-title="Nintendo Entertainment System (NES)" data-img="images/gen3/nes.jpeg">
              NES
            </li>
            <li class="tooltip" data-title="Sega Master System" data-img="images/gen3/sms.jpeg">
              Sega Master System
            </li>
            <li class="tooltip" data-title="Famicom Disk System" data-img="images/gen3/fds.jpeg">
              Famicom Disk System
            </li>
            <li class="tooltip" data-title="Atari 7800" data-img="images/gen3/a7800.jpeg">
              Atari 7800
            </li>
            <li class="tooltip" data-title="Game Boy" data-img="images/gen3/gameboy.jpeg">
              Game Boy
            </li>
          </ul>
        </p>`,
      `<h1 class='step-title'> Nintendo Entertainment System (NES) </h1>
        <p>
          The NES was developed by Nintendo and was released on July 15th, 1983. 
          It was first launched in Japan, then was imported into the US after 
          its early sucess. In fact, it was one of the most influential consoles 
          in the US of all time, as it helped revitalize the US gaming industry 
          from the videogame crash in 1983, and also helped set up a standard 
          business model for licencing.  
        </p>`,
      `<h1 class='step-title'> Sega Master System </h1>
        <p>
          The Master System was developed by Sega, and was released on October 
          20th, 1985. It mostly uses Sega cards to load games, and also has 
          a light gun and 3D glasses that are compatible with specially designed 
          game systems. It failed to compete with Nintendo in Japan, but had 
          significant success in other regions, including the US, Brazil, and 
          Europe.
        </p>`,
      `<h1 class='step-title'> Famicom Disk System </h1>
        <p>
          The Famicom Disk System was developed by Nintendo and was released 
          on February 21st, 1986. This console was only ever sold in Japan, 
          helped boost the market in developing videogames, including the 
          very popular ones such as Legend of Zelda, Super Mario Bros 2, etc.
        </p>`,
      `<h1 class='step-title'> Atari 7800 </h1>
        <p>
          Atari 7800 Prosystem was developed by Atari Corporation and released 
          in May 1986. It was in fact designed by an outside company called 
          General Computer Corporation. It aimed for mostly arcade games, but 
          was frequently complained for the slow release of new games hence only 
          hanged on until 1992 when it was discontinued.
        </p>`,      
      `<h1 class='step-title'>Game Boy</h1>
        <p>
          Gameboy was developed by Nintendo, and was released on April 21, 1989. 
          Although critics had skepticism on its monochromatic graphics and the 
          larger size, it outsold almost all of its competitors. It had many 
          variants after the initial development, which continues all the way 
          into the early 2000s.  
        </p>`,
    ];
  
    // Define images for each step
    const images = [
      {
        console: null,
        games: null,
        consoles: [
          "images/gen3/nes.jpeg",
          "images/gen3/sms.jpeg",
          "images/gen3/fds.jpeg",
          "images/gen3/a7800.jpeg",
          "images/gen3/gameboy.jpeg"
        ]
      },
      {
        console: "images/gen3/nes.jpeg", // Sega Master System
        games: [
          "images/gen3/nes_game1.jpeg", //Rocketboy
          "images/gen3/nes_game2.jpeg",
          "images/gen3/nes_game3.jpeg" //https://www.cbr.com/10-sega-master-system-games-that-went-head-to-head-with-nintendo/
        ]
      },
      {
        console: "images/gen3/sms.jpeg", // Atari 7800
        games: [
          "images/gen3/sms_game1.jpeg", //https://www.blockfort.com/game-lists/atari7800/ Joust
          "images/gen3/sms_game2.jpeg", // Centipede
          "images/gen3/sms_game3.jpeg" // Food Fight
        ]
      },
      {
        console: "images/gen3/fds.jpeg",//NES
        games: [
          "images/gen3/fds_game1.jpeg",
          "images/gen3/fds_game2.jpeg",
          "images/gen3/fds_game3.jpeg" //Contra
        ]
      },
      {
        console: "images/gen3/a7800.jpeg", // Famicom Disk System
        games: [
          "images/gen3/a7800_game1.jpeg",
          "images/gen3/a7800_game2.jpeg",
          "images/gen3/a7800_game3.jpeg"
        ]
      },
      {
        console: "images/gen3/gameboy.jpeg", // Game Boy
        games: [
          "images/gen3/gameboy_game1.jpeg",
          "images/gen3/gameboy_game2.jpeg",
          "images/gen3/gameboy_game3.jpeg"
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
  <h1 class="body-header">3rd Generation: The Advancement of the Console Era</h1>
  <p class="body-text">
    This is the third generation of gaming consoles.
    
  </p>
  <Sega />
  <section>
    <!-- Scroll container -->
    <div class="section-container">
      <div class="charts-container">
        {#if value < 1}
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
      display: flex;
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
      width: 100%;
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
      width: 30%; /* Adjust the width as necessary */
      height: auto;
    }
  
    .all-consoles img:nth-child(1) {
      top: 0;
      left: 20%;
      transform: translateX(-50%);
    }
  
    .all-consoles img:nth-child(2) {
      top: 0;
      left: 40%;
      transform: translateX(-50%);
    }
  
    .all-consoles img:nth-child(3) {
      top: 0;
      left: 60%;
      transform: translateX(-50%);
    }
  
    .all-consoles img:nth-child(4) {
      top: 0;
      left: 80%;
      transform: translateX(-50%);
    }
  
    .all-consoles img:nth-child(5) {
      bottom: 0;
      left: 50%;
      transform: translateX(-50%);
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

