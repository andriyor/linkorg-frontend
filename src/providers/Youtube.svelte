<script>
  import { onMount } from "svelte";
  export let href;
  let embedUrl = "";

  onMount(() => {
    const usrlSearch= new URL(href).search;
    const searchParams = new URLSearchParams(usrlSearch);
    const uid = searchParams.get("v");
    embedUrl = `https://www.youtube.com/embed/${uid}`
  });
</script>

<iframe
  id="ytplayer"
  type="text/html"
  width="640"
  height="360"
  src={embedUrl}
  frameborder="0" />
