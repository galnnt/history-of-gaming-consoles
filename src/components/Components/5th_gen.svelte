<script>
  import Scrolly from "./Scrolly.svelte";
  import { select } from "d3-selection";
  import Sony from "./sony.svelte";
  import Event_3 from "./event_doom.svelte";

  // Scroll iterator
  let value = 0;

  // Paragraph text for scrolly
  $: steps = [
    `<h1 class='step-title'> Fifth Generation: Playstation Joins the Party </h1>
      <p>
        The fifth generation is the first time the name "Playstation" appears in the list. Consoles include
        <ul>
          <li class="tooltip" data-title="Sega Saturn" data-img="images/gen5/saturn.jpeg">
            Sega Saturn
          </li>
          <li class="tooltip" data-title="Playstation" data-img="images/gen5/ps.jpeg">
            Playstation
          </li>
          <li class="tooltip" data-title="Nintendo 64" data-img="images/gen5/nintendo64.jpeg">
            Nintendo 64
          </li>
          <li class="tooltip" data-title="Game Boy Color" data-img="images/gen5/gbc.jpeg">
            Game Boy Color
          </li>
        </ul>
      </p>`,
    `<h1 class='step-title'> Sega Saturn </h1>
      <p>
        Sega Saturn was developed by Sega and released on November 22, 1994. It 
        was initially very successful in Japan but not in the United States. 
        Due to the product being not popular enough outside of Japan, it was 
        widely considered a commercial failure, and Sega's management was 
        heavily criticized for their commercial decisions.
      </p>`,
    `<h1 class='step-title'> PlayStation </h1>
      <p>
        PlayStation was developed by Sony Computer Entertainment and was 
        released on December 3rd, 1994. Sony began this whole series of 
        PlayStation consoles because they failed to venture with Nintendo in 
        the early 1990s. The first model already had an extensive library, low 
        retail price, and aggresive marketing which later proved to be very 
        successful.
      </p>`,
    `<h1 class='step-title'> Nintendo 64 </h1>
      <p>
        Nintendo 64 was developed by Nintendo and released on June 23, 
        1996. It was named the Machine of the Year in 1996, and its popularity 
        led to more color variants being developed later in the next year. It 
        was discontinued after the Gamecube was launched.
      </p>`,
    `<h1 class='step-title'> Game Boy Color </h1>
      <p>
        Game Boy Color was developed by Nintendo Research & Engineering and was 
        released on October 21, 1998. This version was made significantly 
        smaller than the original version of the Game Boy models. It was 
        questioned in the developed process due to it being a monochrome 
        handhelded device, but it had great portability and battery life, which 
        made it stand out in the competitive market.
      </p>`
  ];

  // Define images for each step
  const images = [
    {
      console: null,
      games: null,
      consoles: [
        "images/gen5/saturn.jpeg",
        "images/gen5/ps.jpeg",
        "images/gen5/nintendo64.jpeg",
        "images/gen5/gbc.jpeg"
      ]
    },
    {
      console: "images/gen5/saturn.jpeg",
      games: [
        "images/gen5/saturn_game1.jpeg",
        "images/gen5/saturn_game2.jpeg",
        "images/gen5/saturn_game3.jpeg"
      ]
    },
    {
      console: "images/gen5/ps.jpeg",
      games: [
        "images/gen5/ps_game1.jpeg",
        "images/gen5/ps_game2.jpeg",
        "images/gen5/ps_game3.jpeg"
      ]
    },
    {
      console: "images/gen5/nintendo64.jpeg",
      games: [
        "images/gen5/nintendo64_game1.jpeg",
        "images/gen5/nintendo64_game2.jpeg",
        "images/gen5/nintendo64_game3.jpeg"
      ]
    },
    {
      console: "images/gen5/gbc.jpeg",
      games: [
        "images/gen5/gbc_game1.jpeg",
        "images/gen5/gbc_game2.jpeg",
        "images/gen5/gbc_game3.jpeg"
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

<Event_3 />

<h1 class="body-header">Fifth Generation: Playstation Joins the Party</h1>
<Sony />
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
