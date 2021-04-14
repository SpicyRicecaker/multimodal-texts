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

<main class={darkTheme ? 'light' : 'dark'}>
  <button on:click={() => (darkTheme = !darkTheme)}>dark/light</button>
  <div>
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
  :global(body, html) {
    margin: 0;
    padding: 0;
    width: 100%;
    height: 100%;
  }
  main {
    width: 100%;
    height: 100%;
    position: relative;
    transition: 1s;
  }
  button {
    position: absolute;
    right: 0;
  }
  .light {
    background-color: #fbf1c7;
    color: #654735;
    & :global(a) {
      color: #45707a;
    }
  }

  .dark {
    background-color: #292828;
    color: #d4be98;
    & :global(a) {
      color: #7daea3;
    }
  }
  div {
    width: 100%;
    height: 100%;
    padding: 1em;
    max-width: 240px;
    margin: 0 auto;
  }

  // h1 {
  //   color: #ff3e00;
  //   text-transform: uppercase;
  //   font-size: 4em;
  //   font-weight: 100;
  // }
  @media (min-width: 640px) {
    div {
      max-width: none;
    }
  }
  @media (min-width: 992px) {
    div {
      width: 50%;
    }
  }
</style>
