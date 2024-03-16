<script lang="ts">
  // import { base } from '$app/paths';
  import LandingBlock from "$lib/components/LandingBlock.svelte";
  import LearnMoreBlock from "$lib/components/LearnMoreBlock.svelte";
  import {
    CTA_URL,
    CANNY_URL,
    YOUTUBE_CHANNEL_URL,
    GITHUB_LINK,
    YOUTUBE_MAIN_VIDEO_EMBEDED,
  } from "$lib/constants";

  import YoutubeThumbnail from "$lib/components/YoutubeThumbnail.svelte";
  import DowloadPage from "$lib/DowloadPage.svelte";
</script>

<svelte:head>
  <title>Metatagger AI - File Explorer</title>
</svelte:head>

<br />

<!-- HERO -->
<!-- HERO -->
<!-- HERO -->
<img
  class="fixed top-0 -z-10"
  src="/cover-image.png"
  alt="a screenshot of the app"
/>
<div class="flex mt-5 m-auto justify-center">
  <div class="md:-mt-4 m-auto text-center">
    <p class=" text-7xl px-4 mt-5 space-mono-bold tracking-tighter">
      File explorer <br /> for
      <span class="space-mono-regular-italic custom-font-shadow"
        >AI artists</span
      >

      <br />
      <br />
      <YoutubeThumbnail />
    </p>
  </div>
</div>

<br />
<br />
<br />

<div class="max-w-lg m-auto text-center text-xl">
  <p>
    MetaTagger is a open source desktop app that reads images from your
    computer.
  </p>
  <br />
  <p>View the prompt and parameters used to generate the image.</p>
  <br />
  <p>Search and tag images.</p>
</div>

<br />
<br />

<a href="">Join Discord</a>
<a href="">Check Github</a>

<DowloadPage />

<style>
  .figma_video-button {
    display: inline-flex;
    padding: 10px var(--Section-Margin, 24px);

    justify-content: center;
    align-items: center;
    gap: var(--Element-Spacing, 8px);
    border-radius: 32px;
    border: 1px solid var(--Colors-Grey-400, #bcc3c8);
    box-shadow: 0px 0px 4px 2px rgba(22, 22, 22, 0.057),
      0px -1px 2px 2px rgba(22, 22, 22, 0.08) inset,
      0px 1px 2px 2px rgba(255, 255, 255, 0.12) inset;
  }
</style>
