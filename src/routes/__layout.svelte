<script>
  import { page, navigating } from '$app/stores';
  import Header from '$lib/Components/Header.svelte';
  import Footer from '$lib/Components/Footer.svelte';
  import RequestModal from '$lib/Blocks/RequestModal.svelte';
  import PreloadingIndicator from '$lib/Components/PreloadingIndicator.svelte';
  import { modalStore, mobileMenuOpen } from '$lib/stores/theme';
  import '../global.css';
  import MediaQuery from '$lib/Components/MediaQuery.svelte';

  $: active = $page.path.split('/')[1];

  // When change url, close the nav
  $: $navigating, ($mobileMenuOpen = false);

  const handleEscapeKey = (e) => {
    if (e.key === 'Escape') {
      modalStore.closeAll();
      $mobileMenuOpen = false;
    }
  };
</script>

<svelte:body on:keydown={handleEscapeKey} />
<MediaQuery />

<a class="u-sr-only u-sr-only-focusable" href="#main"> Skip to content </a>

<Header {active} />

<main id="main">
  {#if $navigating}
    <PreloadingIndicator />
  {/if}

  <slot />

  <Footer {active} />
  <RequestModal open={$modalStore.cta} />
</main>

<style>
  main {
    display: flex;
    flex-direction: column;
    min-height: 100vh;
  }
</style>
