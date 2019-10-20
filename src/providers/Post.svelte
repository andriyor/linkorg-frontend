<script>
  import { createEventDispatcher } from "svelte";

  import Select from "svelte-select";
  import Icon from "@smui/textfield/icon";
  import IconButton from "@smui/icon-button";

  import Twitter from "./Twitter.svelte";
  import Reddit from "./Reddit.svelte";
  import Telegram from "./Telegram.svelte";
  import Youtube from "./Youtube.svelte";
  import Image from "./Image.svelte";
  import Video from "./Video.svelte";
  import Github from "./Github.svelte";
  import Instagram from "./Instagram.svelte";

  export let post;
  export let availableTags;

  const dispatch = createEventDispatcher();
  let postComponent;
  let providers = {
    twitter: Twitter,
    reddit: Reddit,
    telegram: Telegram,
    youtube: Youtube,
    image: Image,
    github: Github,
    video: Video,
    instagram: Instagram
  };
  const ComponentName = providers[post.provider.name];

  function removePost(postId) {
    // postComponent.$destroy()
    dispatch("remove", { postId });
  }

</script>

<style>
  .post {
    display: flex;
  }

  .post-actions {
    display: flex;
    flex-direction: column;
  }

  .selected-tags {
    margin: 10px;
  }
</style>

<div bind:this={postComponent}>
  <div class="post">
    <svelte:component this={ComponentName} href={post.href} />
    <div class="post-actions">
      <IconButton class="material-icons" on:click={() => removePost(post.id)}>
        clear
      </IconButton>
      <IconButton class="material-icons" on:click={() => navigator.clipboard.writeText(post.href)}>
        content_copy
      </IconButton>
    </div>
  </div>

  <div class="selected-tags">
    <Select items={availableTags} selectedValue={post.tags} isMulti={true} />
  </div>
</div>