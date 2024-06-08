<script>
  export let sections = [];
  export let activeSection = 0;
  import { Ripple } from 'svelte-mui';

  let hudVisible = false;

  function scrollToSection(index) {
    const element = document.getElementById(`section-${index}`);
    if (element) {
      element.scrollIntoView({ behavior: 'smooth' });
    }
  }

  function toggleHUD() {
    hudVisible = !hudVisible;
  }
</script>

<!-- Toggle Button -->
<button class="toggle-button" on:click={toggleHUD}>
  {hudVisible ? 'Close TOC' : 'Open TOC'}
</button>

<!-- HUD -->
{#if hudVisible}
  <div class="hud">
    {#each sections as section, index}
      <button 
        type="button"
        class="section {index === activeSection ? 'active' : ''}" 
        on:click={() => scrollToSection(index)}
        aria-label={`Scroll to section ${section}`}>
        {section}
      </button>
    {/each}
  </div>
{/if}

<style>
  .hud {
    position: fixed;
    top: 50%;
    left: 0;
    transform: translateY(-50%);
    background-color: rgba(0, 0, 0, 0.7);
    color: white;
    padding: 1rem;
    border-radius: 0 10px 10px 0;
    font-family: Arial, sans-serif;
    z-index: 1000;
  }

  .hud :global(.Ripple) {
    border-radius: 0 !important;
  }

  .section {
    margin: 0.5rem 0;
    padding: 0.5rem;
    cursor: pointer;
    display: block;
  }

  .section.active {
    background-color: #ff5733;
  }

  .toggle-button {
    position: fixed;
    top: 10px;
    left: 10px;
    z-index: 1001;
    padding: 0.5rem 1rem;
    font-size: 1rem;
    font-weight: bold;
    color: #ffffff;
    background-color: #5492d0;
    border: none;
    border-radius: 5px;
    cursor: pointer;
    box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
    transition: background-color 0.3s, transform 0.3s;
  }

  .toggle-button:hover {
    background-color: #1565c0;
  }

  .toggle-button:active {
    transform: scale(0.95);
  }
</style>
