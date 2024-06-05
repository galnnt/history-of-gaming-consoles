<script>
  import Scrolly from "./Scrolly.svelte";
  import { select } from "d3-selection";

  // Scroll iterator
  let value = 0;

  // Paragraph text for scrolly
  $: steps = [
    `<h1 class='step-title'> Eighth Generation </h1>
      <p>
        The eighth generation was heavily influenced by the growth of the mobile 
        gaming industry. Most improved on their hardwares for a better gaming 
        experience. Consoles include
        <ul>
          <li class="tooltip" data-title="Playstation Vita" data-img="images/gen8/psvita.jpeg">
           Playstation Vita
          </li>
          <li class="tooltip" data-title="Playstation 4" data-img="images/gen8/ps4.jpeg">
            Playstation 4
          </li>
          <li class="tooltip" data-title="Wii U" data-img="images/gen8/wiiu.jpeg">
            Wii U
          </li>
          <li class="tooltip" data-title="Xbox One" data-img="images/gen8/xboxone.jpeg">
            Xbox One
          </li>
          <li class="tooltip" data-title="Nintendo Switch" data-img="images/gen8/switch.jpeg">
            Nintendo Switch
          </li>
       </ul>
      </p>`,
    `<h1 class='step-title'> Playstation Vita </h1>
    <p>
      Playstation Vita was developed by Sony Computer Entertainment, and was 
      released on December 17, 2011. It acted as a successor to Playstation 
      Portable, to follow the ongoing trend of popular mobile games. It had a 
      lot of support in JRPGs, visual novels, and indie games.
    </p>`,
    `<h1 class='step-title'> Playstation 4 </h1>
      <p>
        Playstation 4 was developed by Sony Computer Entertainment, and was 
        released on November 15, 2013. It had included an AMD Accelerated 
        Processing Unit, which they claimed was the "most powerful" APU they 
        had at the time. This generation had an increasing emphasis on social 
        interactino including remote play, etc.
      </p>`,
    `<h1 class='step-title'> Wii U </h1>
      <p>
        Wii U was developed by Nintendo and was released in late 2012. It 
        included a gamepad and a screen. The screen could be used as the main 
        display or as a supplement. One of the things that were criticized 
        upon the release was the short span of the battery life, which was 
        considered an important factor for the gaming experience.
      </p>`,
    `<h1 class='step-title'> Xbox One </h1>
      <p>
        Xbox one was developed by Microsoft and released during November 2013. 
        From its last generation, it improve on motion tracking and voice 
        recognition in its "Kinect" feature, adn put an increasing emphasis on 
        cloud computing and social networking, including features like 
        livestreaming and recording videoclips of games.
      </p>`,
    `<h1 class='step-title'> Nintendo Switch </h1>
      <p>
        The Nintendo Switch was developed by Nintendo and was released on March 
        3rd, 2017. It is a tablet that can either be put onto a dock or used as 
        a portable device, depending on the usage. It as very popular for its 
        Joy-Con controllers to support local multiplayer game modes.
      </p>`
  ];
  // Define images for each step
  const images = [
    {
      console: null,
      games: null,
      consoles: [
        "images/gen8/psvita.jpeg",
        "images/gen8/ps4.jpeg",
        "images/gen8/wiiu.jpeg",
        "images/gen8/xboxone.jpeg",
        "images/gen8/switch.jpeg"
      ]
    },
    {
      console: "images/gen8/psvita.jpeg",
      games: [
        "images/gen8/psvita_game1.jpeg",
        "images/gen8/psvita_game2.jpeg",
        "images/gen8/psvita_game3.jpeg"
      ]
    },
    {
      console: "/images/gen8/ps4.jpeg",
      games: [
        "images/gen8/ps4_game1.jpeg",
        "images/gen8/ps4_game2.jpeg",
        "images/gen8/ps4_game3.jpeg"
      ]
    },
    {
      console: "images/gen8/wiiu.jpeg",
      games: [
        "images/gen8/wiiu_game1.jpeg",
        "images/gen8/wiiu_game2.jpeg",
        "images/gen8/wiiu_game3.jpeg"
      ]
    },
    {
      console: "images/gen8/xboxone.jpeg",
      games: [
        "images/gen8/xboxone_game1.jpeg",
        "images/gen8/xboxone_game2.jpeg",
        "images/gen8/xboxone_game3.jpeg"
      ]
    },
    {
      console: "images/gen8/switch.jpeg",
      games: [
        "images/gen8/switch_game1.jpeg",
        "images/gen8/switch_game2.jpeg",
        "images/gen8/switch_game3.jpeg"
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

<h2 class="body-header"> 8th Generation: The Advancement of the Console Era </h2>
<p class="body-text">
  This is the eighth generation of gaming consoles.
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

"""