<script>
  import { onMount } from 'svelte';

  let registerDropdown = false;
  let scrolled = false;
  let contentEl;

  function handleScroll() {
    scrolled = contentEl.scrollTop > 0;
	console.log(scrolled);
  }

  onMount(() => {
    contentEl.addEventListener('scroll', handleScroll);
    handleScroll();
    return () => contentEl.removeEventListener('scroll', handleScroll);
  });
</script>

<style>
  .screen {
    position: absolute;
    top: 0; left: 0;
    width: 100%; height: 100%;
    margin: 0;
    background: #e8e8ec;
  }

  .topbar {
    position: fixed;
    top: 0; left: 0;
    width: 100%;
    height: 50px;
    padding: 1px 24px;
    display: flex;
    align-items: center;
    justify-content: flex-end;
    box-sizing: border-box;
    background: transparent;
    gap: 16px;
    z-index: 100;
    box-shadow: 0 2px 6px transparent, inset 0 -1px transparent;
    border-bottom: 2px solid transparent;
    border-image: radial-gradient(circle at center, #929292 0%, #afafaf 10%, transparent 100%);
    border-image-slice: 1;
	  will-change: background, height, transform, border-bottom;
	  transition: background 0.18s cubic-bezier(0.4, 0, 0.2, 1), 
	    height 0.18s cubic-bezier(0.4, 0, 0.2, 1),
	    border-bottom 0.18s cubic-bezier(0.4, 0, 0.2, 1);
  }
  .topbar.scrolled {
	  box-shadow: 0 2px 6px #0000001f, inset 0 -1px #dadce0;
	  height: 55px;
	  background: #F1F3F4;
    border: none;
  }

  .content {
    position: absolute;
    top: 45px; left: 0; right: 0; bottom: 0;
    overflow-y: auto;
    padding: 15px;
    gap: 40px;
    background: linear-gradient(to bottom , #e8e8ec, #d8d8da);
	  transition: top 0.05s ease;
  }

  .login-link {
    font-family: 'Roboto', sans-serif;
    line-height: 38px;
    color: #254a94 !important;
    text-decoration: none;
    background: transparent;
    border-radius: 18px;
    cursor: pointer;
    width: clamp(7%, 12%, 20%);
    height: 38px;
    border: 1px solid rgb(57, 56, 63);
    text-align: center;
    font-size: clamp(9px, 1.2vw, 14px);
    font-weight: 485;
	  transition: color 0.18s ease;
    box-sizing: border-box;
    transition: font-size 0.3s cubic-bezier(0.4, 0, 0.2, 1), 
      transform 0.3s cubic-bezier(0.4, 0, 0.2, 1), 
      top 0.3s ease, 
      left 0.3s ease, 
      right 0.3s ease, 
      bottom 0.3s ease;
  }
  .login-link:hover {
	  color: #132d61 !important;
  }

  .btn-create-account {
    font-family: 'Roboto', sans-serif;
    line-height: 38px;
    color: white !important;
    text-decoration: none;
    background: linear-gradient(to bottom right, #254a94, #5754a5);
    border-radius: 18px;
    cursor: pointer;
    width: clamp(7%, 15%, 25%);
    height: 38px;
    border: none;
    text-align: center;
    font-size: clamp(9px, 1.2vw, 14px);
    font-weight: 485;
	  transition: font-size 0.3s cubic-bezier(0.4, 0, 0.2, 1), 
      transform 0.3s cubic-bezier(0.4, 0, 0.2, 1), 
      top 0.3s ease, 
      left 0.3s ease, 
      right 0.3s ease, 
      bottom 0.3s ease;
  }
  .btn-create-account:hover {
	  background: linear-gradient(to bottom right, #214283, rgb(79, 77, 139));
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

  .register-dropdown {
    transition: opacity 0.1s ease-in-out;
    position: fixed;
    top: 12%;
    right: 30px;
    width: fit-content;
    height: 14%;
    border-radius: 6px;
    background: linear-gradient(to bottom , #e8e8ec, #d8d8da);
    box-shadow: 0 1px 2px rgba(60,64,67,0.3), 0 2px 6px rgba(60,64,67,0.15), 0 0 0 1px rgba(60,64,67,0.05);
    z-index: 10;
    padding: 8px;
    display: flex;
    flex-direction: column;
    transition: font-size 0.3s cubic-bezier(0.4, 0, 0.2, 1), 
      transform 0.3s cubic-bezier(0.4, 0, 0.2, 1), 
      top 0.3s ease, 
      left 0.3s ease, 
      right 0.3s ease, 
      bottom 0.3s ease;
  }

  .visit-link {
    width: fit-content;
    padding: 5px;
    padding-top: 0; padding-bottom: 0;
    font-family: 'Roboto', sans-serif; 
    line-height: 45px; 
    color: #254a94 !important; 
    cursor: pointer; 
    text-decoration: none;
    border: none;
    border-radius: 6px;
    white-space: nowrap;
    transition: color 0.1s cubic-bezier(0.4, 0, 0.2, 1), background 0.1s cubic-bezier(0.4, 0, 0.2, 1);
    text-align: center;
    font-size: clamp(80%, 1.8vw, 1.15rem);
  }
  .visit-link:hover {
    color: #122a5a;
    background: rgba(111, 106, 112, 0.22);
  }
  .regs-link {
    width: fit-content;
    padding: 5px;
    padding-top: 0; padding-bottom: 0;
    font-family: 'Roboto', sans-serif; 
    line-height: 45px; 
    color: #254a94 !important; 
    cursor: pointer; 
    text-decoration: none;
    border: none;
    border-radius: 6px;
    white-space: nowrap;
    transition: color 0.1s cubic-bezier(0.4, 0, 0.2, 1), background 0.1s cubic-bezier(0.4, 0, 0.2, 1);
    text-align: center;
    font-size: clamp(80%, 1.8vw, 1.15rem);
  }
  .regs-link:hover {
    color: #122a5a;
    background: rgba(111, 106, 112, 0.22);
  }

  @media (max-width: 700px) {
    .visit-link {
      display: none !important;
    }
  }
</style>

<svelte:head>
  <!-- Material Symbols & Roboto -->
  <link href="https://fonts.googleapis.com/css2?family=Material+Symbols+Outlined" rel="stylesheet" />
  <link href="https://fonts.googleapis.com/css2?family=Roboto:wght@100;300;400;500;700;900&display=swap" rel="stylesheet" />
</svelte:head>

<div class="screen">
  <div class="topbar" class:scrolled={scrolled}>
    <a href="/" class="logo-link" style="transform: {!scrolled ? "scale(0.86)" : "none"}; transform-origin: top left;">
      <img class="logo-img" src="webLogoWindale.png" alt="logo" style="transform: {!scrolled ? "translate(9%, 16%) scale(0.82);" : "none"}; transform-origin: top left;"/>
    </a>
    <a
      href="/main"
      class="visit-link"
      style:font-size={!scrolled ? 'clamp(11px, 1.1vw, 14px)' : null}
      style:height={!scrolled ? '35px' : null}
      style:line-height={!scrolled ? '35px' : null}
      >Entre como um visitante
    </a>
    <a href="/logIn" class="login-link" style="{scrolled ? "" : "width: clamp(100px, 9%, 25%); font-size: clamp(10.5px, 1vw, 12px); height: 35px; line-height: 35px;"}">Fazer login</a>
    <button style="{scrolled ? "" : "width: clamp(100px, 9%, 25%); font-size: clamp(10.5px, 1vw, 12px); height: 35px; line-height: 35px;"}" class="btn-create-account" on:click={() => registerDropdown = !registerDropdown}>Criar uma conta</button>
  </div>

  <div class="content" bind:this={contentEl} style="top: {scrolled ? '55px;' : '0px; padding-top: 50px;'}">
    <div role="menu" class="register-dropdown" style="opacity: {registerDropdown ? 1 : 0}; top: {!scrolled ? '10%' : '12%'}">
      <a href="/register" class="regs-link" style="color:white;">Para uso pessoal</a>
      <a href="/registerComp" class="regs-link" style="color:white;">
        Para uma empresa ou negócio
      </a>
    </div>
  </div>
</div>
