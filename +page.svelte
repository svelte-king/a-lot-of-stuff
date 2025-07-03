<!-- simple auth navbar, no buttons, just the logo + link for main page -->

<script>
  import { onMount } from 'svelte';
  let scrolled = false;
  let registerDropdown = false;

  function handleScroll() {
    scrolled = window.scrollY > 10;
  }

  onMount(() => {
    window.addEventListener('scroll', handleScroll);
    handleScroll();
    return () => window.removeEventListener('scroll', handleScroll);
  });
</script>

<style>
  .topbar {
    position: fixed;
    top: 0; left: 0;
    width: calc(100% - 0px);
    height: 50px;
    padding: 1px 24px;
    padding-right: 8px;
    display: flex;
    align-items: center;
    justify-content: flex-end;
    box-sizing: border-box;
    background: transparent;
    gap: 16px;
    z-index: 100;
    box-shadow: 0 2px 6px transparent, inset 0 -1px transparent;
    border-bottom: 2px solid transparent;
    border-image: radial-gradient(circle at center, #696969 0%, #606063 10%, transparent 100%);
    border-image-slice: 1;
	  will-change: background, height, width, border-bottom;
	  transition: background 0.18s cubic-bezier(0.4, 0, 0.2, 1), 
	  height 0.18s cubic-bezier(0.4, 0, 0.2, 1),
	  border-bottom 0.18s cubic-bezier(0.4, 0, 0.2, 1),
      width 0.18s cubic-bezier(0.4, 0, 0.2, 1);
  }

  .logo-link {
    align-items: center;
    width: 180px;
    height: 50px;
    margin-right: auto;
  }

  .logo-img {
    width: 180px;
    height: 50px;
  }

</style>

<div class="topbar" class:scrolled={scrolled}>
  <a href="/" class="logo-link" style="transform: {!scrolled ? 'scale(0.86)' : 'none'}; transform-origin: top left;">
    <img loading="lazy" class="logo-img" src="webLogoWindale.png" alt="logo" style="transform: {!scrolled ? 'translate(9%, 16%) scale(0.82)' : 'none'}; transform-origin: top left;" />
  </a>
</div>
