<script lang="ts">
  import marked from 'marked';
  // import katex from 'katex';
  import { onMount, tick } from 'svelte';

  let markdown: String = '';
  let darkTheme = false;

  onMount(async () => {
    try {
      const stream = await fetch('content.md');
      const string = await stream.text();
      markdown = marked(string);
      await tick();
      // const latexElements = document.getElementsByClassName('language-tex');
      // for (let i = 0; i < latexElements.length; i++) {
      //   latexElements[i].innerHTML = katex.renderToString(
      //     latexElements[i].innerHTML,
      //     { throwOnError: false }
      //   );
      // }
    } catch (e) {
      console.log(e);
    }
  });
</script>

<main class={darkTheme ? 'dark' : 'light'}>
  <button on:click={() => (darkTheme = !darkTheme)}>dark/light</button>
  <div class="body">
    {@html markdown}
  </div>
</main>

<!-- <svelte:head>
  <link
    rel="stylesheet"
    href="https://cdn.jsdelivr.net/npm/katex@0.13.2/dist/katex.min.css"
    integrity="sha384-Cqd8ihRLum0CCg8rz0hYKPoLZ3uw+gES2rXQXycqnL5pgVQIflxAUDS7ZSjITLb5"
    crossorigin="anonymous"
  />
</svelte:head> -->
<style lang="scss">
  :global(body) {
    margin: 0;
    padding: 0;
    display: grid;
  }
  main {
    position: relative;
    transition: 1s;
    display: grid;
    & :global(img) {
      width: 75%;
      display: block;
      margin: auto;
    }
  }
  button {
    position: absolute;
    right: 0;
  }
  .body {
    max-width: 240px;
    margin: 1rem;
    align-self: center;
    justify-self: center;

    & :global(a) {
      transition: 1s;
    }
  }

  .light {
    background-color: #fbf1c7;
    color: #654735;
    & :global(a) {
      color: #45707a;
    }

    & > button {
      background-color: #292828;
      color: #d4be98;
    }
  }

  .dark {
    background-color: #292828;
    color: #d4be98;
    & :global(a) {
      color: #7daea3;
    }

    & > button {
      color: #292828;
      background-color: #d4be98;
    }
  }
  button {
    transition: 1s;
    border-radius: 0;
    outline: none;
    border: none;
  }

  // h1 {
  //   color: #ff3e00;
  //   text-transform: uppercase;
  //   font-size: 4em;
  //   font-weight: 100;
  // }
  @media (min-width: 640px) {
    .body {
      max-width: none;
    }
  }
  @media (min-width: 992px) {
    .body {
      width: 50%;
    }
  }
</style>
