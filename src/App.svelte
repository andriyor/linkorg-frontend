<script>
  import { onMount } from "svelte";

  import Select from "svelte-select";

  import Post from "./providers/Post.svelte"

  let tags = [];
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
    fethPosts().then(l => {
      posts = l;
      console.log(posts);
    });
    fethTags().then(availableTags => (tags = availableTags));
  });
</script>

<style>
  h1 {
    color: purple;
  }
</style>

<Select items={tags} isMulti="{true}" />

{#each posts as post}
  <Post {post} />
{/each}

