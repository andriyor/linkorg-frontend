<script>
  import { onMount } from "svelte";

  import Select from "svelte-select";

  import Post from "./providers/Post.svelte"

  let availableTags = [];
  let posts = [];

  function fethPosts() {
    return fetch("http://localhost:3000/links", { method: "GET", mode: "cors" })
      .then(response => response.json())
      .then(myJson => myJson);
  }

  function fethTags() {
    return fetch("http://localhost:3000/tags", { method: "GET", mode: "cors" })
      .then(response => response.json())
      .then(myJson => myJson);
  }

  onMount(() => {
    fethPosts().then(p => posts = p);
    fethTags().then(tags => (availableTags = tags));
  });
</script>

<style>
  h1 {
    color: purple;
  }
</style>

<Select items={availableTags} isMulti="{true}" />

{#each posts as post}
  <Post {post} {availableTags} />
{/each}
