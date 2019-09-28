<script>
  import Select from "svelte-select";
  
  import Twitter from "./Twitter.svelte";
  import Reddit from "./Reddit.svelte";
  import Telegram from "./Telegram.svelte";
  import Youtube from "./Youtube.svelte";
  import Image from "./Image.svelte";
  import Video from "./Video.svelte";
  import Github from "./Github.svelte";

  export let post = [];
  export let availableTags = [];

  let providers = {
    'twitter': Twitter,
    'reddit': Reddit,
    'telegram': Telegram,
    'youtube': Youtube,
    'image': Image,
    'github': Github,
    'video': Video,
  }
  const ComponentName = providers[post.provider];
</script>

<svelte:component  this={ComponentName} href={post.href}/>

<Select items={availableTags} selectedValue={post.tags} isMulti="{true}" />
