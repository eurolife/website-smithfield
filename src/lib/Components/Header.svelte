<script>
  import { theme, mobileMenuOpen } from '$lib/stores/theme';

  import Logo from '$lib/Components/Logo.svelte';
  import Nav from '$lib/Components/Nav.svelte';
  import Wrapper from './Wrapper.svelte';
  import Button from './Button.svelte';

  let sticky;
  let y = 0;
  $: sticky = y > 40;

  export let active;
</script>

<svelte:window bind:scrollY={y} />

<header class="c-site-header">
  <Wrapper type="x-wide">
    <div class="c-site-header__inner" class:sticky>
      <a class="c-site-header__logo" href="/">
        <Logo theme={sticky ? 'light' : $theme.header} />
      </a>

      <Button class="c-site-header__menu-button" color="dark-glow" size="cta" action={() => ($mobileMenuOpen = !$mobileMenuOpen)}>
        {#if $mobileMenuOpen}
          Close
        {:else}
          Menu
        {/if}
      </Button>

      <Nav theme={sticky ? 'light' : $theme.header} {active} open={$mobileMenuOpen} />
    </div>
  </Wrapper>
</header>

<style>
  .c-site-header {
    position: fixed;
    top: 16px;
    width: 100%;
    z-index: 100;
    transition: all 0.2s ease;
  }

  @media (max-width: 320px) {
    .c-site-header {
      padding: 8px;
    }
  }

  @media (min-width: 768px) {
    .c-site-header {
      top: 32px;
    }
  }

  .c-site-header__inner {
    display: flex;
    width: 100%;
    padding: 8px 16px;
    align-items: center;
    justify-content: space-between;
    border-radius: 60px;
    transition: all 0.3s ease;
    isolation: isolate;
  }

  @media (min-width: 321px) {
    .c-site-header__inner {
      padding: 16px 24px;
    }
  }

  .c-site-header__logo {
    display: inline-block;
    height: 40px;
    transition: all 0.15s ease;
  }

  @media (min-width: 321px) {
    .c-site-header__logo {
      height: 60px;
    }
  }

  .sticky {
    background-color: var(--color-sky);
  }

  .sticky .c-site-header__logo {
    height: 40px;
  }

  @media (min-width: 768px) {
   :global(.c-site-header__menu-button) {
      display: none !important;
    }
  }
</style>
