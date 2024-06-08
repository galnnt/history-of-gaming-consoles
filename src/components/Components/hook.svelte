<script>
  import { Textfield } from 'svelte-mui';

  let value = '';
  let error = '';
  let message = 'Please enter the name of the console';

  // Define your validation criteria
  function validateInput(val) {
    if (val === '') {
      message = 'Please enter the name of the console';
      error = '';
    } else if (val !== 'PS2') {
      message = 'Incorrect! You will find the answer in this article';
      error = 'Incorrect! You will find the answer in this article';
    } else {
      message = 'Correct! Use the HUD on the left to navigate to any generations or just skip to the conclusion';
      error = '';
    }
  }

  // Watch the value and validate
  $: validateInput(value);
</script>

<div class="hook-container">
  <h1 class="hook-header">Welcome to this project</h1>
  <h2 class="hook-subheader">First, let's answer this question: What is the most Popular Console of All Time?</h2>

  <Textfield
    autocomplete="off"
    label="Enter Console Name"
    required
    bind:value
    message={message}
    error={error}
    class="hook-textfield"
  />
</div>

<style>
  .hook-container {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    padding: 2rem;
    background-color: #f0f4f8;
    border-radius: 10px;
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
  }

  .hook-header {
    font-size: 2rem;
    color: #333;
    margin-bottom: 1rem;
    text-align: center;
  }

  .hook-subheader {
    font-size: 1.5rem;
    color: #666;
    margin-bottom: 1.5rem;
    text-align: center;
  }

  .hook-textfield {
    width: 100%;
    max-width: 400px;
  }
</style>
