<script>
  import Scrolly from "./Scrolly.svelte";
  import { select } from "d3-selection";

  // Scroll iterator
  let value = 0;

  // Paragraph text for scrolly
  $: steps = [
    `<h1 class='step-title'>Seventh Generation</h1>
      <p>
       Seventh generation. Consoles include
       <ul>
         <li class="tooltip" data-title="Nintendo DS" data-img="/images/console_7_1.jpeg">
           Nintendo DS
         </li>
         <li class="tooltip" data-title="Nintendo 3DS" data-img="/images/console_7_2.jpeg">
           Nintendo 3DS
         </li>
         <li class="tooltip" data-title="Xbox 360" data-img="/images/console_7_3.jpeg">
           Xbox 360
         </li>
         <li class="tooltip" data-title="Playstation 3" data-img="/images/console_7_4.jpeg">
           Playstation 3
         </li>
         <li class="tooltip" data-title="Wii" data-img="/images/console_7_5.jpeg">
           Wii
         </li>
       </ul>
      </p>`,
    `<h1 class='step-title'>Step 2</h1>
      <p>
        Lorem ipsum dolor sit amet consectetur adipisicing elit. Velit sint aut corrupti ullam neque quia labore laborum perspiciatis, molestias amet at, voluptatem ratione quaerat in sit minima reprehenderit molestiae, nobis sed. Earum facere exercitationem sit rerum, expedita magni nihil alias?
      </p>`,
    `<h1 class='step-title'>Step 3</h1>
      <p>
        Lorem ipsum dolor sit amet consectetur adipisicing elit. Velit sint aut corrupti ullam neque quia labore laborum perspiciatis, molestias amet at, voluptatem ratione quaerat in sit minima reprehenderit molestiae, nobis sed. Earum facere exercitationem sit rerum, expedita magni nihil alias?
      </p>`,
    `<h1 class='step-title'>Step 4</h1>
      <p>
        Lorem ipsum dolor sit amet consectetur adipisicing elit. Velit sint aut corrupti ullam neque quia labore laborum perspiciatis, molestias amet at, voluptatem ratione quaerat in sit minima reprehenderit molestiae, nobis sed. Earum facere exercitationem sit rerum, expedita magni nihil alias?
      </p>`
  ];

  // Define images for each step
  const images = [
    {
      console: null,
      games: null,
      consoles: [
        "images/console_7_1.jpeg",
        "images/console_7_2.jpeg",
        "images/console_7_3.jpeg",
        "images/console_7_4.jpeg",
        "images/console_7_5.jpeg"
      ]
    },
    {
      console: "images/console_7_1.jpeg",
      games: [
        "images/console_7_1_game_1.jpeg",
        "images/console_7_1_game_2.jpeg",
        "images/console_7_1_game_3.jpeg"
      ]
    },
    {
      console: "images/console_7_2.jpeg",
      games: [
        "images/console_7_2_game_1.jpeg",
        "images/console_7_2_game_2.jpeg",
        "images/console_7_2_game_3.jpeg"
      ]
    },
    {
      console: "images/console_7_3.jpeg",
      games: [
        "images/console_7_3_game_1.jpeg",
        "images/console_7_3_game_2.jpeg",
        "images/console_7_3_game_3.jpeg"
      ]
    },
    {
      console: "images/console_7_4.jpeg",
      games: [
        "images/console_7_4_game_1.jpeg",
        "images/console_7_4_game_2.jpeg",
        "images/console_7_4_game_3.jpeg"
      ]
    },
    {
      console: "images/console_7_5.jpeg",
      games: [
        "images/console_7_5_game_1.jpeg",
        "images/console_7_5_game_2.jpeg",
        "images/console_7_5_game_3.jpeg"
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

<h2 class="body-header">3rd Generation: The Advancement of the Console Era</h2>
<p class="body-text">
  This is the third generation of gaming consoles.
</p>
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

