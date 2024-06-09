<script>
  import Scrolly from "./Scrolly.svelte";
  import { select } from "d3-selection";
  import Microsoft from "./Microsoft.svelte";
  import Event_4 from "./event_segaout.svelte";
  import Event_5 from "./event_central.svelte";

  // Scroll iterator
  let value = 0;

  // Paragraph text for scrolly
  const steps = [
    `<h1 class='step-title'> Sixth Generation </h1>
      <p>
        The 6th generation was full of utilization of internet in order for 
        users to have a complete gaming experience. Consoles include:
        <ul>
          <li class="tooltip" data-title="Dreamcast" data-img="images/gen6/dreamcast.jpeg">
            Dreamcast
          </li>
          <li class="tooltip" data-title="Wonderswan" data-img="images/gen6/wonderswan.jpeg">
            Wonderswan
          </li>
          <li class="tooltip" data-title="PlayStation 2" data-img="images/gen6/ps2.jpeg">
            PlayStation 2
          </li>
          <li class="tooltip" data-title="Gameboy Advance" data-img="images/gen6/gba.jpeg">
            Gameboy Advance
          </li>
          <li class="tooltip" data-title="Gamecube" data-img="images/gen6/gamecube.jpeg">
            Gamecube
          </li>
          <li class="tooltip" data-title="Xbox" data-img="images/gen6/xbox.jpeg">
            Xbox
          </li>
          <li class="tooltip" data-title="N-gage" data-img="images/gen6/ngage.jpeg">
            N-gage
          </li>
          <li class="tooltip" data-title="Playstation Portable" data-img="images/gen6/psp.jpeg">
            Playstation Portable
          </li>
        </ul>
      </p>`,
    `<h1 class='step-title'> Dreamcast </h1>
      <p>
        Dreamcast was developed by Sega and was released on November 27th, 1998. 
        It was designed to reduce costs from cheaper hardware, and avoided DVDs 
        as they were too expensive at the time. However, sales were not good as 
        compated with Sony's PlayStation 2, hence its production came to a halt.
      </p>`,
    `<h1 class='step-title'> WonderSwan </h1>
      <p>
        Wonderswan was developed by Bandai and was released on March 4th, 1999. 
        This console took advantace of a low price point and battery life, and 
        can be held both vertically and horizontally for games. It has a lot of 
        unique games from licensed anime and third party supports as well.
      </p>`,
    `<h1 class='step-title'> PlayStation 2 </h1>
      <p>
        PlayStation 2 was developed by Sony Computer Entertainment and was 
        released on March 4th, 2020. It is the best selling videogame console 
        of all time, and continued to remain popular even after later 
        generations are out, until Sony announced that it would be discontinued 
        after its twelveth year of production.
      </p>`,
    `<h1 class='step-title'> Gameboy Advance </h1>
      <p>
        Gameboy Advance was developed by Nintendo and was released on March 
        21st, 2001. It was developed because Nintendo felt the sales pressure 
        from other competitors in the industry, and has a different feature of 
        leaving the buttons on the sides of the device. 
      </p>`,
    `<h1 class='step-title'> Gamecube </h1>
      <p>
        The Gamecube was developed by Nintendo and was released on September 
        14th, 2001. Nintendo developed this console in collaboration with ArtX 
        to design a graphics processing unit. It is the first console that used 
        Nintendo's own optical disks instead of using ROM. However, it was 
        criticized for its lack for third party support.
      </p>`,
    `<h1 class='step-title'> Xbox </h1>
      <p>
        Xbox was developed by Microsoft and was released on November 15th, 
        2001. It was the first console to feature a built-in hard disk, and is 
        also one of the first which has Ethernet support. Moreover, the release 
        of Xbox Live, a free online-gaming service, made it a strong candidate 
        during this generation of consoles.
      </p>`,
    `<h1 class='step-title'> N-gage </h1>
      <p>
        N-Gage was developed by Nokia and was released on October 7th, 2004. 
        It was an attempt from Nokia to enter the gaming market, and they 
        intended to lure gamers away by the additional functionality of the 
        telephone functionalities. However, there were simply too many buttons 
        on the device so it was a commercial failure.
      </p>`,
    `<h1 class='step-title'> PlayStation Portable </h1>
      <p>
        PlayStation Portable was developed by Sony Computer Entertainment and 
        was released on December 12th, 2004. The advanced graphics made this a 
        popular mobile game choice, and also included many multimedia features. 
        It was fairly popular among gamers until the last Japanese factory 
        producing them closed in late 2016.
      </p>`
  ];

  // Define images for each step
  const images = [
    {
      console: null,
      games: null,
      consoles: [
        "images/gen6/dreamcast.jpeg",
        "images/gen6/wonderswan.jpeg",
        "images/gen6/ps2.jpeg",
        "images/gen6/gba.jpeg",
        "images/gen6/gamecube.jpeg",
        "images/gen6/xbox.jpeg",
        "images/gen6/ngage.jpeg",
        "images/gen6/psp.jpeg"
      ]
    },
    {
      console: "images/gen6/dreamcast.jpeg",
      games: [
        "images/gen6/dreamcast_game1.jpeg",
        "images/gen6/dreamcast_game2.jpeg",
        "images/gen6/dreamcast_game3.jpeg"
      ]
    },
    {
      console: "images/gen6/wonderswan.jpeg",
      games: [
        "images/gen6/wonderswan_game1.jpeg",
        "images/gen6/wonderswan_game2.jpeg",
        "images/gen6/wonderswan_game3.jpeg"
      ]
    },
    {
      console: "images/gen6/ps2.jpeg",
      games: [
        "images/gen6/ps2_game1.jpeg",
        "images/gen6/ps2_game2.jpeg",
        "images/gen6/ps2_game3.jpeg"
      ]
    },
    {
      console: "images/gen6/gba.jpeg",
      games: [
        "images/gen6/gba_game1.jpeg",
        "images/gen6/gba_game2.jpeg",
        "images/gen6/gba_game3.jpeg"
      ]
    },
    {
      console: "images/gen6/gamecube.jpeg",
      games: [
        "images/gen6/gamecube_game1.jpeg",
        "images/gen6/gamecube_game2.jpeg",
        "images/gen6/gamecube_game3.jpeg"
      ]
    },
    {
      console: "images/gen6/xbox.jpeg",
      games: [
        "images/gen6/xbox_game1.jpeg",
        "images/gen6/xbox_game2.jpeg",
        "images/gen6/xbox_game3.jpeg"
      ]
    },
    {
      console: "images/gen6/ngage.jpeg",
      games: [
        "images/gen6/ngage_game1.jpeg",
        "images/gen6/ngage_game2.jpeg",
        "images/gen6/ngage_game3.jpeg"
      ]
    },
    {
      console: "images/gen6/psp.jpeg",
      games: [
        "images/gen6/psp_game1.jpeg",
        "images/gen6/psp_game2.jpeg",
        "images/gen6/psp_game3.jpeg"
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

<h1 class="body-header"> 6th Generation: The Advancement of Console Gaming </h1>
<p class="body-text">
  The 6th generation was full of utilization of internet in order for users to 
  have a complete gaming experience.
</p>
<Microsoft />

<Event_4 />
<Event_5 />

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
