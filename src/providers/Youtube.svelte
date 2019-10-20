<script>
  import { onMount, afterUpdate } from "svelte";

  export let href;
  let embedUrl = "";

  function updateURL(href) {
    const usrlSearch= new URL(href).search;
    const searchParams = new URLSearchParams(usrlSearch);
    const uid = searchParams.get("v");
    return `https://www.youtube.com/embed/${uid}`;
  }

  $: embedUrl = updateURL(href);
</script>


<iframe
  id="ytplayer"
  type="text/html"
  width="640"
  height="360"
  title=""
  src={embedUrl}
  frameborder="0" />
