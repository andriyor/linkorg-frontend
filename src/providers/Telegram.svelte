<script>
  import { onMount } from "svelte";
  import { beforeUpdate, afterUpdate } from "svelte";

  export let href;
  let postPath = "";

  $: postPath = `${href}?embed=1`;
</script>

<iframe
  id={href}
  src={postPath}
  width="100%"
  height=""
  frameborder="0"
  scrolling="no"
  style="border: none; overflow: hidden; min-width: 320px; height: 404px;" />
