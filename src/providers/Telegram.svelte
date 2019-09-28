<script>
  import { onMount } from "svelte";
  export let href;
 	let postPath = '';

  onMount(() => {
    postPath = new URL(href).pathname
  });
</script>

<blockquote>
  <script
    async
    src="https://telegram.org/js/telegram-widget.js?7"
    data-telegram-post={postPath}
    data-width="100%">

  </script>
</blockquote>
