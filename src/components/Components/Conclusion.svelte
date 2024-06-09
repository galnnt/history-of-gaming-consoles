<script>
  import Final_chart from "./final_chart.svelte";
</script>

<section id="conclusion">
  <h1 class="body-header">Conclusion</h1>
  <div class="conclusion-content">
    <Final_chart />
    <div class="body-text">
      <h2>
        Through generations of fierce competition, we may have finally reached the conclusion of the long-standing console war. Today, only three companies—Nintendo, Microsoft, and Sony—remain active in the console market. With recent news suggesting that Microsoft might be "stepping down" from the race, it seems the competition may soon be dominated solely by Sony and Nintendo. The ninth generation of consoles could very well mark the end of this decades-long rivalry.
      </h2>
      <h2>
        However, this shift might not be detrimental to the gaming industry. Over the years, gaming has evolved and expanded across various platforms such as PCs and smartphones, making it more accessible to a wider audience. This evolution paints a picture of a more vibrant and diverse gaming market, full of opportunities and innovations. The end of the console war may simply signify the beginning of a new era in gaming, where the possibilities are boundless and the future looks brighter than ever.
      </h2>
    </div>
  </div>
</section>

<style>
  #conclusion {
    background: linear-gradient(to right, #e66465, #9198e5);
   
    color: #fff;
  }

  .conclusion-content {
    display: flex;
    align-items: flex-start;
    justify-content: space-between;
    padding: 2rem;
    background: rgba(255, 255, 255, 0.2); /* Slightly transparent background */
    border-radius: 10px;
  }

  .conclusion-content > :first-child {
    flex: 1;
    margin-right: 2rem;
  }

  .conclusion-content .body-text {
    flex: 2;
    margin-top: 1rem; /* Move the text down a bit */
    margin-left: 10px; /* Move the text rightward by 10px */
  }

  .body-header {
    font-size: 2.5rem;
    margin-bottom: 1rem;
    color: #fff;
    text-align: center;
  }

  .body-text h2 {
    font-size: 1.2rem;
    color: #fff;
    font-family: 'Georgia', serif;
    line-height: 1.6;
  }

  @media screen and (max-width: 950px) {
    .conclusion-content {
      flex-direction: column;
      align-items: center;
    }

    .conclusion-content > :first-child {
      margin-right: 0;
      margin-bottom: 1rem;
    }

    .body-text h2 {
      text-align: center;
    }
  }
</style>
