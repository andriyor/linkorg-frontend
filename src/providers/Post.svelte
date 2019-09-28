<script>
  import Select from "svelte-select";
  
  import Twitter from "./Twitter.svelte";
  import Reddit from "./Reddit.svelte";
  import Telegram from "./Telegram.svelte";
  import Youtube from "./Youtube.svelte";

  export let post = [];
  export let availableTags = [];
</script>

{#if post.provider === 'twitter'}
  <Twitter href={post.href} />
{/if}
{#if post.provider === 'reddit'}
  <Reddit href={post.href} />
{/if}
{#if post.provider === 'telegram'}
  <Telegram href={post.href} />
{/if}
{#if post.provider === 'youtube'}
  <Youtube href={post.href} />
{/if}

<Select items={availableTags} selectedValue={post.tags} isMulti="{true}" />
