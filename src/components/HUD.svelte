<script>
  export let sections = [];
  export let activeSection = 0;

  function scrollToSection(index) {
    const element = document.getElementById(`section-${index}`);
    if (element) {
      element.scrollIntoView({ behavior: 'smooth' });
    }
  }
</script>

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

  .section {
    margin: 0.5rem 0;
    padding: 0.5rem;
    cursor: pointer;
    display: block;
  }

  .section.active {
    background-color: #ff5733;
  }
</style>

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
