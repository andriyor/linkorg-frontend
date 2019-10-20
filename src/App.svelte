<script>
  import { onMount } from "svelte";

  import Select from "svelte-select";
  import Textfield, { Input, Textarea } from "@smui/textfield";
  import Icon from "@smui/textfield/icon";
  import IconButton from "@smui/icon-button";
  import Button, { Label } from "@smui/button";

  import Post from "./providers/Post.svelte";

  let providers = {
    twitter: RegExp("twitter"),
    reddit: RegExp("reddit"),
    youtube: RegExp("youtube"),
    github: RegExp("github"),
    instagram: RegExp("instagram"),
    telegram: RegExp("t.me"),
    telegram: RegExp("t.me"),
    image: RegExp(".(gif|jpg|jpeg|tiff|png)"),
    video: RegExp(".mp4")
  };
  let availableTags = [];
  let selectedTags = [];
  let posts = [];
  let loadedPosts = [];
  let postURL = "";
  let baseURL = "http://localhost:3030";

  function fethPosts() {
    return fetch(`${baseURL}/posts`, { method: "GET", mode: "cors" })
      .then(response => response.json())
      .then(myJson => myJson);
  }

  function fethTags() {
    return fetch(`${baseURL}/tags`, { method: "GET", mode: "cors" })
      .then(response => response.json())
      .then(myJson => myJson);
  }

  function handleSelect(selectedVal) {
    selectedTags = selectedVal.detail;
  }

  function handleFilterSelect(selectedVal) {
    const selectedFilterTags = selectedVal.detail;
    if (selectedFilterTags) {
      const filtrIds = selectedFilterTags.map(t => t.id);
      posts = loadedPosts.filter(p => p.tags.some(t => filtrIds.includes(t.id)));
    } else {
      posts = [...loadedPosts];
    }
  }

  function detectProvider(url) {}

  function sendPost(post) {
    return fetch(`${baseURL}/posts`, {
      method: "POST",
      body: JSON.stringify(post),
      headers: {
        "Content-Type": "application/json"
      }
    }).then(response => response.json());
  }

  function createPost() {
    const currentProvider = Object.keys(providers).find(provider =>
      providers[provider].test(postURL)
    );
    const post = {
      provider: currentProvider,
      href: postURL,
      tags: selectedTags
    };
    sendPost(post).then(newPost => (posts = [...posts, newPost]));
  }

  onMount(() => {
    fethPosts().then(p => {
      loadedPosts = p;
      posts = [...loadedPosts];
    });
    fethTags().then(tags => (availableTags = tags));
  });

  function deletePost(postId) {
    fetch(`${baseURL}/posts/${postId}`, {
      method: "DELETE"
    });
  }

  function handlePostDelete(event) {
    console.log(event.detail.postId);
    posts = posts.filter(p => event.detail.postId != p.id);
    deletePost(event.detail.postId);
    console.log(posts);
  }
</script>

<style>
  .post-adding {
    display: flex;
  }
  .filter-post {
    display: flex;
    margin: 10px;
  }
  .filter {
    margin-right: 10px;
  }
  .select-tag {
    margin: 0 10px 0 10px;
  }
</style>

<div class="post-adding">
  <Textfield
    withLeadingIcon
    bind:value={postURL}
    label="URL"
    input$aria-controls="helper-text-standard-a"
    input$aria-describedby="helper-text-standard-a">
    <Icon class="material-icons">playlist_add</Icon>
  </Textfield>

  <div class="select-tag">
    <Select items={availableTags} on:select={handleSelect} isMulti={true} />
  </div>

  <Button on:click={() => createPost()}>
    <Label>Add post</Label>
  </Button>
</div>

<div class="filter-post">
  <div class="filter">Filter</div>
  <Select items={availableTags} on:select={handleFilterSelect} isMulti={true} />
</div>

{#each posts as post, i}
  <Post {post} {availableTags} on:remove={handlePostDelete} />
{/each}
