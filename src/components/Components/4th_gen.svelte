<script>
    import Scrolly from "./Scrolly.svelte";
    import { select } from "d3-selection";
  
    // Scroll iterator
    let value = 0;
  
    // Paragraph text for scrolly
    const steps = [
      `<h1 class='step-title'> Fourth Generation </h1>
        <p>
          The fourth generation of consoles marked significant advancements in gaming. Key consoles in this era include:
          <ul>
            <li class="tooltip" data-title="PC Engine/TurboGrafx-16" data-img="images/gen4/turbo.jpeg">
             PC Engine/TurboGrafx-16
            </li>
            <li class="tooltip" data-title="Sega Genesis/Mega Drive" data-img="images/gen4/sg.jpeg">
              Sega Genesis/Mega Drive
            </li>
            <li class="tooltip" data-title="PC Engine CD-ROM" data-img="images/gen4/cdrom.jpeg">
              PC Engine CD-ROM
            </li>
            <li class="tooltip" data-title="Atari Lynx" data-img="images/gen4/lynx.jpeg">
              Atari Lynx
            </li>
            <li class="tooltip" data-title="Sega Game Gear" data-img="images/gen4/gamegear.jpeg">
              Sega Game Gear
            </li>
            <li class="tooltip" data-title="SNES/Super Famicom" data-img="images/gen4/snes.jpeg">
              SNES/Super Famicom
            </li>
            <li class="tooltip" data-title="Philips CD-i" data-img="images/gen4/cdi.jpeg">
              Philips CD-i
            </li>
            <li class="tooltip" data-title="Sega Pico" data-img="images/gen4/pico.jpeg">
              Sega Pico
            </li>
          </ul>
        </p>`,
      `<h1 class='step-title'>PC Engine/TurboGrafx-16</h1>
        <p>
          The TurboGrafx-16 was developed by Hudson Soft and was released on 
          October 30, 1987. Despite it being developed in North America, it was 
          mainly successful in its marketing in Japan and failed miserably in 
          the United States. However, its later models were not as successful 
          so its operations got shut down relatively shortly after.
        </p>`,
      `<h1 class='step-title'> Sega Genesis/Mega Drive </h1>
        <p>
          Sega Genesis was developed by Sega and was released on October 29th, 
          1988. It had two network services to support the Genesis. It was 
          mostly successful in the United States and had poor sales in Japan. 
          Its success was mostly due to the Sonic the Hedgehog series, and 
          aggressive marketing towards adolescents.
        </p>`,
      `<h1 class='step-title'> PC Engine CD-ROM </h1>
        <p>
          This is the add-on version to TurboGrafx-16 that was released in 
          Japan only on December 4th, 1988. This is the first videogame console 
          that uses CD-ROM to store media. 
        </p>`,
      `<h1 class='step-title'> Atari Lynx </h1>
        <p>
          The Atari Lynx was developed by Epyx and as released on September 1st, 
          1989. While developing this console, the developers actively tried to 
          seek for collaboration, but got rejected by the major companies. It 
          was fairly successful until the release of Sega Saturn, effectively 
          shutting down the whole business.
        </p>`,
      `<h1 class='step-title'>Sega Game Gear</h1>
        <p>
          Game Gear was developed by Sega and released on October 6th, 1990. 
          Although it is considered a rush product by Sega, it has a unique 
          game library and price point. However, Sega gave little financial 
          support after its release, and, together with its low battery life, 
          caused its discontinuation in 1997.
        </p>`,
      `<h1 class='step-title'> SNES/Super Famicom </h1>
        <p>
          Super Nintendo Entertainment System (SNES) was developed by Nintendo 
          and was released in November 21, 1990. This is the second home 
          console that is programmable, and was the best selling console of the 
          16-bit era after launching. It still remained popular into the 32-bit 
          era until it was discontinued in 2023.
        </p>`,
      `<h1 class='step-title'> Philips CD-i </h1>
        <p>
          The CD-i was co-developed by Sony and Philips and was released in 
          early 1991. In additional to gaming purposed, the CD-i also included 
          features such as interactive encyclopedias, and even museum tours, 
          while also having internet access for emails and downloading. 
          However, it did not find much success in the market and was abandoned 
          by Philips a few years after.
        </p>`,
      `<h1 class='step-title'>Sega Pico</h1>
        <p>
          Sega Pico was developed by Sega and released in June 1993. This 
          gaming console was primarily targeting children between 3-7 years old, 
          andd was mostly focued on education instead of gaming. It acheived 
          success in Japan but not in Europe and the US.
        </p>`
    ];
  
    // Define images for each step
    const images = [
      {
        console: null,
        games: null,
        consoles: [
          "images/gen4/turbo.jpeg",
          "images/gen4/sg.jpeg",
          "images/gen4/cdrom.jpeg",
          "images/gen4/lynx.jpeg",
          "images/gen4/gamegear.jpeg",
          "images/gen4/snes.jpeg",
          "images/gen4/cdi.jpeg",
          "images/gen4/pico.jpeg"
        ]
      },
      {
        console: "images/gen4/turbo.jpeg", // Sega Genesis/Mega Drive
        games: [
          "images/gen4/turbo_game1.jpeg", // Streets Of Rage II
          "images/gen4/turbo_game2.jpeg", // Sonic The Hedgehog 2
          "images/gen4/turbo_game3.jpeg" // Golden Axe
        ]
      },
      {
        console: "images/gen4/sg.jpeg", // SNES/Super Famicom
        games: [
          "images/gen4/sg_game1.jpeg",
          "images/gen4/sg_game2.jpeg",
          "images/gen4/sg_game3.jpeg"
        ]
      },
      {
        console: "images/gen4/cdrom.jpeg", // Atari Lynx
        games: [
          "images/gen4/cdrom_game1.jpeg", // https://indiegamerchick.com/2023/08/07/atari-lynx-the-definitive-review-part-one/
          "images/gen4/cdrom_game2.jpeg",
          "images/gen4/cdrom_game3.jpeg"
        ]
      },
      {
        console: "images/gen4/lynx.jpeg", // PC Engine/TurboGrafx-16
        games: [
          "images/gen4/lynx_game1.jpeg", //https://www.blockfort.com/game-lists/turbografx/
          "images/gen4/lynx_game2.jpeg",
          "images/gen4/lynx_game3.jpeg"
        ]
      },
      {
        console: "images/gen4/gamegear.jpeg", // PC Engine CD-ROM
        games: [
          "images/gen4/gamegear_game1.jpeg", //https://cdrom.ca/games/2023/06/29/first-cdrom-games.html#:~:text=First%20CD%2DROM%20game%2C%20any,(PC%20Engine%20CD%2C%201988)
          "images/gen4/gamegear_game2.jpeg",
          "images/gen4/gamegear_game3.jpeg"
        ]
      },
      {
        console: "images/gen4/snes.jpeg", // Philips CD-i https://www.gamesradar.com/best-philips-cdi-games/
        games: [
          "images/gen4/snes_game1.jpeg", // Secret Mission
          "images/gen4/snes_game2.jpeg", // Mutant Rampage: Bodyslam
          "images/gen4/snes_game3.jpeg" // Ram Raid
        ]
      },
      {
        console: "images/gen4/cdi.jpeg", // Sega Pico https://segaretro.org/A_Year_at_Pooh_Corner
        games: [
          "images/gen4/cdi_game1.jpeg",
          "images/gen4/cdi_game2.jpeg",
          "images/gen4/cdi_game3.jpeg"
        ]
      },
      {
        console: "images/gen4/pico.jpeg", // Sega Game Gear
        games: [
          "images/gen4/pico_game1.jpeg", // sonic drift
          "images/gen4/pico_game2.jpeg",
          "images/gen4/pico_game3.jpeg"
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
  