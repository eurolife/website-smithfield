<script>
  import { modalStore, mobileMenuOpen } from '$lib/stores/theme';
  import Badge from './Badge.svelte';
  import Button from './Button.svelte';

  export let theme;
  export let active;
</script>

<nav
  class="c-primary-nav c-primary-nav--{theme}"
  class:is-open={$mobileMenuOpen}
  role="navigation"
  aria-label="Main"
>
  <a sveltekit:prefetch href="/about" class:is-active={active === 'about'}> About </a>
  <a sveltekit:prefetch href="/jobs" class:is-active={active === 'jobs'}>
    Jobs
    <Badge color="blue">3</Badge>
  </a>
  <a sveltekit:prefetch href="/contact" class:is-active={active === 'contact'}>Contact</a>
  <Button color="dark-glow" size="cta" action={() => ($modalStore.cta = true)}>
    Request early access
  </Button>
</nav>

<style>
  .c-primary-nav--dark a {
    color: #fff;
  }

  nav {
    font-size: 16px;
    font-weight: 500;
  }

  /* Mobile Nav */
  @media (max-width: 767px) {
    nav {
      display: none;
    }

    nav.is-open {
      position: fixed;
      display: flex;
      flex-direction: column;
      align-items: flex-start;
      padding: 2rem;
      top: 120px;
      width: calc(100% - 48px);
      height: 300px;
      left: 50%;
      transform: translateX(-50%);
      background-color: var(--color-sky);
      border-radius: 30px;
      isolation: isolate;
      z-index: 1;
      box-shadow: 0 0 14px rgba(164, 205, 251, 0.7);
    }

    nav.is-open a {
      color: var(--color-indigo);
    }

    nav.is-open a + a {
      margin-top: 2rem;
    }

    :global(nav .c-button--cta) {
      margin-top: auto;
      margin-bottom: 0;
      width: 100%;
    }
  }

  @media (min-width: 768px) {
    nav {
      display: flex;
      align-items: center;
    }

    a + a,
    :global(.c-primary-nav a + .c-button) {
      margin-left: 4rem;
    }
  }

  a {
    position: relative;
    color: var(--color-indigo);
    text-decoration: none;
  }

  a.is-active {
    color: var(--color-blue);
  }
</style>
