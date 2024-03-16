<script lang="ts">
  // MADE THIS COMPONENT SO THAT EARLY DOWNLOAD PAGE DOESNT REDIRECT TO FORM, WILL BECOME OBSOLETE AT SOME POINT
  import {
    CHECK_OUT_FORM,
    LINUX_WAILIST_URL,
    YOUTUBE_MAIN_VIDEO_EMBEDED,
  } from "$lib/constants";
  import { onMount } from "svelte";

  import { writable } from "svelte/store";
  import Modal, { bind } from "$lib/components/Modal.svelte";
  import YoutubeVideo from "$lib/components/YoutubeVideo.svelte";
  const modal = writable(null);
  const showModal = () =>
    modal.set(
      bind(YoutubeVideo, {
        link: YOUTUBE_MAIN_VIDEO_EMBEDED,
      })
    );

  export let redirectToForm = true;

  const REPO_LINK = "https://github.com/PhotoFolder/OneFolder/releases/latest";
  const REPO_LINK_API =
    "https://api.github.com/repos/PhotoFolder/OneFolder/releases/latest";

  let windowsLink = REPO_LINK;
  let macLink = REPO_LINK;
  let linuxLink = REPO_LINK;

  let windowsLinkRaw =
    "https://github.com/OneFolderApp/OneFolder/releases/download/1.0.0/OneFolder-Setup-1.0.0.exe";
  let macLinkRaw =
    "https://github.com/OneFolderApp/OneFolder/releases/download/1.0.0/OneFolder-1.0.0.dmg";
  let linuxLinkRaw =
    "https://github.com/OneFolderApp/OneFolder/releases/download/1.0.0/OneFolder-1.0.0.AppImage";

  onMount(() => {
    setDownloadLinks();
  });

  async function setDownloadLinks() {
    const response = await fetch(REPO_LINK_API, {
      method: "GET",
      headers: {
        Accept: "application/vnd.github.v3+json",
      },
    });
    const json = await response.json();
    const assets = json.assets;
    for (let i = 0; i < assets.length; i++) {
      const asset = assets[i];
      if (
        asset.content_type.startsWith("application") &&
        asset.name.startsWith("OneFolder-")
      ) {
        if (asset.name.endsWith(".exe")) {
          windowsLink = asset.browser_download_url;
        } else if (asset.name.endsWith(".dmg")) {
          macLink = asset.browser_download_url;
        } else if (asset.name.endsWith(".AppImage")) {
          linuxLink = asset.browser_download_url;
        }
      }
    }
  }
</script>

<div
  class="flex flex-col items-center gap-6 max-w-md w-full m-auto text-[#333]"
>
  <a
    id="download-windows"
    href={windowsLinkRaw}
    on:click={() => {
      if (redirectToForm && window) {
        window?.open(CHECK_OUT_FORM, "_blank")?.focus();
      }
    }}
    class="cta-button w-full flex justify-center !text-white !no-underline px-3 py-3 text-xl hover:bg-[#ff5643e2] transition-all"
  >
    <img src="/windows.svg" alt="OneFolder logo" class="mr-1" />
    Download for Windows
  </a>
  <a
    class="cta-button w-full flex justify-center !text-white !no-underline px-3 py-3 text-xl hover:bg-[#ff5643e2] transition-all"
    id="download-mac"
    href={macLinkRaw}
    on:click={() => {
      if (redirectToForm && window) {
        window?.open(CHECK_OUT_FORM, "_blank")?.focus();
      }
    }}
  >
    <img src="/mac.svg" alt="OneFolder logo" class="mr-1" />

    Download for Mac
  </a>
  <a
    class="cta-button w-full flex justify-center !text-white !no-underline px-3 py-3 text-xl hover:bg-[#ff5643e2] transition-all"
    id="download-mac"
    href={linuxLinkRaw}
    on:click={() => {
      if (redirectToForm && window) {
        window?.open(CHECK_OUT_FORM, "_blank")?.focus();
      }
    }}
  >
    <img src="/linux.svg" alt="OneFolder logo" class="mr-1" />
    Download for Linux
  </a>
</div>
