<script setup>
  import logo from '@/assets/images/snjezna-dolina-logo-text.svg'
  import phoneIcon from '@/assets/images/home/phone-icon.svg'
  import hamburgerMenu from '@/assets/images/home/hamburger-menu.svg'
  
</script>

<template>
  <header class="header-main">
    <a href="#">
      <img
        :src="logo"
        alt="Snjezna Dolina logo"
        class="logo"/>
    </a>
    <div class="icon-holder">
      <a href="tel:+1234567890">
        <img 
          :src="phoneIcon" 
          alt="Phone icon" 
          class="phone-icon"/>
      </a>
      <a href="#">
        <img 
          :src="hamburgerMenu" 
          alt="Hamburger menu" 
          class="hamburger-menu"/>
      </a>
    </div>
  </header>
</template>

<style scoped>
  .header-main {
    display: flex;
    justify-content: space-between;
    align-items: center;
    gap: 16px;
    .logo {
      max-width: 100%;
    }
    .icon-holder {
      display: flex;
      gap: 8px;
    }
  }
</style>