<script>
  export let title = "XBOX signals retrieving from the competition";
  export let imageUrl = "images/xbox_out.png";
  export let description = `Microsoft may be signaling an exit from the console wars, leaving Sony and Nintendo to compete. Some analysts are concerned about the industry's long-term prospects, but Serkan Toto, head of Kantan Games, suggests that the industry may return to the 1990s, when Japanese consoles were the only viable options`;
</script>

<section class="news-item">
  <div class="news-image-container">
    <img class="news-image" src={imageUrl} alt={title} />
  </div>
  <div class="news-content">
    <h1 class="news-title">{title}</h1>
    <p class="news-description">{description}</p>
  </div>
</section>

<style>
  .news-item {
    max-width: 800px;
    margin: 2rem auto;
    padding: 2rem;
    background: linear-gradient(135deg, #f6d365 0%, #fda085 100%);
    border-radius: 15px;
    box-shadow: 0 6px 10px rgba(0, 0, 0, 0.1);
    display: flex;
    flex-direction: row;
    align-items: center;
    transition: transform 0.3s ease-in-out;
  }

  .news-item:hover {
    transform: translateY(-5px);
    box-shadow: 0 8px 16px rgba(0, 0, 0, 0.2);
  }

  .news-image-container {
    flex-shrink: 0;
  }

  .news-image {
    width: 150px;
    height: auto;
    border-radius: 15px;
    margin-right: 1.5rem;
  }

  .news-content {
    max-width: 600px;
  }

  .news-title {
    font-size: 2rem;
    margin-bottom: 0.5rem;
    color: #333;
    font-family: 'Helvetica Neue', sans-serif;
  }

  .news-description {
    font-size: 1.1rem;
    color: #555;
    font-family: 'Georgia', serif;
    line-height: 1.6;
  }

  @media screen and (max-width: 950px) {
    .news-item {
      flex-direction: column;
      align-items: center;
      text-align: center;
    }

    .news-image {
      margin-right: 0;
      margin-bottom: 1rem;
    }

    .news-content {
      max-width: 100%;
    }
  }
</style>
