<script>
  import { onMount } from "svelte";

  export let href;

  let repoPath;

  onMount(() => {
    repoPath = new URL(href).pathname.replace("/", "");
    console.log(repoPath);
  });
</script>



{#if repoPath}
  <div>
    <script async src="https://cdn.jsdelivr.net/github-cards/latest/widget.js"></script>
    <div
    class="github-card"
    data-github={repoPath}
    data-width="400"
    data-height=""
    data-theme="default" />
  </div>
{/if}



