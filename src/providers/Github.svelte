<script>
  import { onMount } from "svelte";
  import { onDestroy } from "svelte";
  import { beforeUpdate, afterUpdate } from "svelte";

  export let href;
  let repoPath;

  $: repoPath = new URL(href).pathname.replace("/", "");
  
</script>

<div>
  <script async src="https://cdn.jsdelivr.net/github-cards/latest/widget.js">  </script> 
  <div
    class="github-card"
    data-github={repoPath}
    data-width="400"
    data-height=""
    data-theme="default" />
</div>
