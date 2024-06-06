<script>
  export let title = "Nintendo";
  export let imageUrl = "images/nintendo.png";
  export let description = "Nintendo is a Japanese multinational consumer electronics and video game company headquartered in Kyoto, Japan.";
</script>

<section class="company-introduction">
  <h1 class="company-title">{title}</h1>
  <div class="company-content">
    <img class="company-image" src={imageUrl} alt={title} />
    <p class="company-description">{description}</p>
  </div>
</section>

<style>
  .company-introduction {
    max-width: 800px;
    margin: 2rem auto;
    padding: 2rem;
    background-color: #f5f5f5;
    border-radius: 10px;
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
    text-align: left;
  }

  .company-title {
    font-size: 2.5rem;
    margin-bottom: 1rem;
    color: #333;
    font-family: 'Helvetica Neue', sans-serif;
  }

  .company-content {
    display: flex;
    flex-direction: row;
    align-items: flex-start;
  }

  .company-image {
    width: 200px;
    height: auto;
    margin-right: 2rem;
    border-radius: 10px;
  }

  .company-description {
    font-size: 1.2rem;
    color: #666;
    font-family: 'Georgia', serif;
    line-height: 1.6;
  }

  @media screen and (max-width: 950px) {
    .company-content {
      flex-direction: column;
      align-items: center;
    }

    .company-image {
      margin-right: 0;
      margin-bottom: 1rem;
    }

    .company-description {
      text-align: center;
    }
  }
</style>
