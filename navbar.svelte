<!-- the full version of topbar for the hero. you gotta bind the scrollable part of your site to topbarEl (bind:this={topbarEl}) 
     keep in mind i made this in my first two weeks so im pretty proud of myself as i didn't know any of js/html/css -->

<script>
  import { onMount } from 'svelte';

  let registerDropdown = false;
  let scrolled = false;
  let topbarEl;

  function handleScroll() {
    if (window.scrollY > 10) {
      scrolled = true;
    } else {
      scrolled = false;
    }
  }

  onMount(() => {
    window.addEventListener('scroll', handleScroll, { passive: true });
    return () => window.removeEventListener('scroll', handleScroll);
  });
</script>

<style>
  .topbar {
    position: fixed;
    top: 0; left: 0;
    width: 100%;
    height: 50px;
    padding: 1px 24px 1px 24px;
    display: flex;
    align-items: center;
    justify-content: flex-end;
    background: #e2e7e7;
    gap: 16px;
    z-index: 100;
    box-shadow: 0 2px 6px transparent, inset 0 -1px transparent;
    border-bottom: 2px solid transparent;
    border-image: radial-gradient(circle at center, #555555 0%, #a7a7a8 55%, transparent 98%);
    border-image-slice: 1;
    will-change: background, height, width, border-bottom;
    transition: background 0.18s cubic-bezier(0.4, 0, 0.2, 1), 
      height 0.18s cubic-bezier(0.4, 0, 0.2, 1),
      border-bottom 0.18s cubic-bezier(0.4, 0, 0.2, 1),
      width 0.18s cubic-bezier(0.4, 0, 0.2, 1);
  }
  .topbar.scrolled {
    box-shadow: 0 2px 6px #0000001f, inset 0 -1px #dadce0;
    height: 55px;
    background: #ecedf0;
    border: none;
    width: 100%;
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
  .breadcrumbs {
    display: flex;
    flex-direction: row;
    align-items: center;
    justify-content: center;
    gap: 16px;
  }
  .faq {
    font-family: 'Roboto', sans-serif;
    color: rgba(0.5, 0.5, 0.5, 0.8);
    text-decoration: none;
    font-weight: 500;
    font-size: 14px;
    margin: 5px;
    cursor: pointer;
    position: relative;
    line-height: normal;
    padding-bottom: 2px;
  }
  .faq::after {
    content: '';
    position: absolute;
    left: 0;
    bottom: 0;
    width: 0;
    height: 2px;
    background: #334954;
    transition: width 0.2s ease-out;
  }
  .faq:hover::after {
    width: 100%;
    height: 2px;
    background: #102857;
    animation: slide 0.2s ease-out;
  }
  .login-link {
    font-family: 'Roboto', sans-serif;
    line-height: 38px;
    color: #1c3c7e !important;
    text-decoration: none;
    background: transparent;
    border-radius: 18px;
    cursor: pointer;
    width: clamp(80px, 10%, 9%);
    height: 35px;
    border: 1px solid rgb(57, 56, 63);
    text-align: center;
    font-size: clamp(10.5px, 1vw, 12px);
    font-weight: 485;
    box-sizing: border-box;
    transition: font-size 0.3s cubic-bezier(0.4, 0, 0.2, 1), 
      transform 0.3s cubic-bezier(0.4, 0, 0.2, 1),
      color 0.18s ease;
  }
  .login-link:hover {
    color: #334954 !important;
  }
  .btn-create-account {
    font-family: 'Roboto', sans-serif;
    line-height: 38px;
    color: white !important;
    text-decoration: none;
    background: linear-gradient(to bottom right, #1c3c7e, #557381);
    border-radius: 18px;
    cursor: pointer;
    width: clamp(110px, 12%, 11%);
    border: none;
    text-align: center;
    font-size: clamp(10.5px, 1vw, 12px);
    font-weight: 485;
    transition: font-size 0.3s cubic-bezier(0.4, 0, 0.2, 1), 
      transform 0.3s cubic-bezier(0.4, 0, 0.2, 1);
  }
  .btn-create-account:hover {
    background: linear-gradient(to bottom right, #0f2757, #3b5561);
  }
  .register-dropdown {
    position: absolute;
    top: 110%;
    right: 30px;
    width: fit-content;
    height: fit-content;
    border-radius: 6px;
    background: linear-gradient(to bottom , #e8e8ec, #d8d8da);
    box-shadow: 0 1px 2px rgba(60,64,67,0.3), 0 2px 6px rgba(60,64,67,0.15), 0 0 0 1px rgba(60,64,67,0.05);
    z-index: 110;
    padding: 8px;
    display: flex;
    flex-direction: column;
    transition: font-size 0.3s cubic-bezier(0.4, 0, 0.2, 1), 
      transform 0.3s cubic-bezier(0.4, 0, 0.2, 1);
  }
  .regs-link {
    width: calc(100% - 10px);
    padding: 5px;
    font-family: 'Roboto', sans-serif; 
    line-height: 45px; 
    color: #1c3c7e !important; 
    cursor: pointer; 
    text-decoration: none;
    border: none;
    border-radius: 6px;
    white-space: nowrap;
    transition: color 0.1s cubic-bezier(0.4, 0, 0.2, 1), background 0.1s cubic-bezier(0.4, 0, 0.2, 1);
    text-align: left;
    font-size: clamp(80%, 1.8vw, 1.15rem);
  }
  .regs-link:hover {
    color: #334954;
    background: rgba(111, 106, 112, 0.22);
  }
  @keyframes slide {
    0% { width: 0 }
    100% { width: 100% }
  }
</style>

<svelte:head>
  <link href="https://fonts.googleapis.com/css2?family=Material+Symbols+Outlined" rel="stylesheet" />
  <link href="https://fonts.googleapis.com/css2?family=Roboto:wght@100;300;400;500;700;900&display=swap" rel="stylesheet" />
</svelte:head>

<div class="topbar" class:scrolled={scrolled} bind:this={topbarEl}>
  <a href="/" class="logo-link">
    <img loading="lazy" class="logo-img" src="webLogoWindale.png" alt="logo" />
  </a>
  <div class="breadcrumbs">
    <a href="/docs" class="faq">Documentação</a>
    <a href="/about" class="faq">Sobre</a>
    <a href="/faq" class="faq">Perguntas frequentes</a>
  </div>
  <a href="/logIn" class="login-link">Fazer login</a>
  <button class="btn-create-account" on:click={() => registerDropdown = !registerDropdown}>Criar uma conta</button>
  {#if registerDropdown}
    <div class="register-dropdown">
      <a href="/register" class="regs-link" style="color:white;">Para uso pessoal</a>
      <a href="/registerComp" class="regs-link" style="color:white;">Para uma empresa ou negócio</a>
    </div>
  {/if}
</div>
