<script setup>
  import { ref } from 'vue';
  import logo from '@/assets/images/snjezna-dolina-logo-text.svg'
  import phoneIcon from '@/assets/images/home/phone-icon.svg'
  import hamburgerMenu from '@/assets/images/home/hamburger-menu.svg'
  import hamburgerMenuClose from '@/assets/images/home/hamburger-menu-close.svg'
  import mobileMenuImg from '@/assets/images/home/mobile-navigation.webp'
  
  const mobileMenuOpen = ref(false);

  const toggleMenu = () => {
    mobileMenuOpen.value = !mobileMenuOpen.value;
    console.log("toggle menu", mobileMenuOpen.value);
  }

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
      <a class="phone-icon" href='tel:+38162204003'>
        <img 
          :src="phoneIcon" 
          alt="Phone icon" 
          />
      </a>
      <a 
        class="hamburger-menu-btn"
          
        aria-label="Menu"
        @click="toggleMenu">

        <img v-if="!mobileMenuOpen"
          :src="hamburgerMenu" 
          alt="Hamburger menu" 
          class="hamburger-menu"/>

        <img v-else
          :src="hamburgerMenuClose" 
          alt="Hamburger menu close icon" 
          class="hamburger-menu"/>
      </a>
    </div>

    <div class="mobile-menu-holder" v-if="mobileMenuOpen">
      <ul class="mobile-nav-list">
        <li class="mobile-nav-list-item">
          <a class="mobile-nav-list-item-holder" href="#hero">
            <p class="nav-name">Pogodnosti <br>
              <span>Zašto naši apartmani...</span>
            </p>
            <svg class="nav-icon" width="20" height="20" viewBox="0 0 20 20" fill="none" xmlns="http://www.w3.org/2000/svg">
              <path d="M7.5 5L12.5 10L7.5 15" stroke="white" stroke-width="1.5"/>
            </svg>
          </a>
        </li>
        <li class="mobile-nav-list-item">
          <a class="mobile-nav-list-item-holder" href="#apts">
            <p class="nav-name">Apartmani <br>
              <span>Izaberi apartman...</span>
            </p>
            <svg class="nav-icon" width="20" height="20" viewBox="0 0 20 20" fill="none" xmlns="http://www.w3.org/2000/svg">
              <path d="M7.5 5L12.5 10L7.5 15" stroke="white" stroke-width="1.5"/>
            </svg>
          </a>
        </li>
        <li class="mobile-nav-list-item">
          <a class="mobile-nav-list-item-holder" href="#characteristics">
            <p class="nav-name">Opremljenost <br>
              <span>Sve što vam treba...</span>
            </p>
            <svg class="nav-icon" width="20" height="20" viewBox="0 0 20 20" fill="none" xmlns="http://www.w3.org/2000/svg">
              <path d="M7.5 5L12.5 10L7.5 15" stroke="white" stroke-width="1.5"/>
            </svg>
          </a>
        </li>
        <li class="mobile-nav-list-item">
          <a class="mobile-nav-list-item-holder" href="#reviews">
            <p class="nav-name">Recenzije <br>
              <span>Utisci naših gostiju...</span>
            </p>
            <svg class="nav-icon" width="20" height="20" viewBox="0 0 20 20" fill="none" xmlns="http://www.w3.org/2000/svg">
              <path d="M7.5 5L12.5 10L7.5 15" stroke="white" stroke-width="1.5"/>
            </svg>
          </a>
        </li>
        <li class="mobile-nav-list-item">
          <a class="mobile-nav-list-item-holder" href="#faq">
            <p class="nav-name">Informacije <br>
              <span>Šta treba da znaš...</span>
            </p>
            <svg class="nav-icon" width="20" height="20" viewBox="0 0 20 20" fill="none" xmlns="http://www.w3.org/2000/svg">
              <path d="M7.5 5L12.5 10L7.5 15" stroke="white" stroke-width="1.5"/>
            </svg>
          </a>
        </li>
        <li class="mobile-nav-list-item">
          <a class="mobile-nav-list-item-holder" href="#location">
            <p class="nav-name">Lokacija <br>
              <span>U srcu jahorine...</span>
            </p>
            <svg class="nav-icon" width="20" height="20" viewBox="0 0 20 20" fill="none" xmlns="http://www.w3.org/2000/svg">
              <path d="M7.5 5L12.5 10L7.5 15" stroke="white" stroke-width="1.5"/>
            </svg>
          </a>
        </li>
      </ul>
      <div class="mobile-img-holder">
        <a href="#apts" class="book-now-cta">
          Rezerviši odmah
          <svg width="17" height="24" viewBox="0 0 17 24" fill="none" xmlns="http://www.w3.org/2000/svg">
            <path d="M0.707291 19.3053H15.3178V4.69475M15.3178 19.3053L0.707291 4.69475" stroke="white" stroke-width="2"/>
          </svg>
        </a>
      </div>
    </div>
  </header>
</template>

<style scoped>
  .header-main {
    position: relative;
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
      .phone-icon, .hamburger-menu {
        transition: .3s ease;
        border-radius: 50%;
        border: 1px solid transparent;
        &:hover {
          transform: scale(1.05);
          cursor: pointer;
          border: 1px solid #2FB6EF;
        }
      }
    }
    .mobile-menu-holder {
      position: absolute;
      top: 100%;
      left: 0;
      padding: 20px;
      width: 100%;
      z-index: 9;
      background-color: #13202E;
      border-radius: 20px;
      .mobile-nav-list {
        list-style: none;
        display: flex;
        flex-wrap: wrap;
        gap: 0;
        .mobile-nav-list-item {
          flex: 0 0 33%;
          border-bottom: 1px solid #2F3752;
          border-right: 1px solid #2F3752;
          &:nth-child(3n) {
            border-right: none;
          }
          &:nth-last-child(-n+3) {
            border-bottom: none;
          }
          .mobile-nav-list-item-holder {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 12px 20px;
            text-decoration: none;
            .nav-name {
              font-style: normal;
              font-weight: 700;
              font-size: 16px;
              line-height: 24px;
              color: #FFFFFF;
              span {
                transition: .3s ease;
                margin-top: 4px;
                display: block;
                font-style: normal;
                font-weight: 500;
                font-size: 14px;
                line-height: 24px;
                color: #B9C1C9;
              }
            }
            svg {
              transition: .3s ease;
            }

            &:hover {
              .nav-name {
                span {
                  color: #2FB6EF;
                }
              }
              svg {
                transform: translateX(4px);
                path {
                  stroke: #2FB6EF;
                }
              }
            }
          }
        }
      }
      .mobile-img-holder {
        margin-top: 20px;
        background-image: url(../assets/images/home/mobile-navigation.webp);
        background-size: cover;
        position: relative;
        display: flex;
        justify-content: center;
        border-radius: 8px;

        .book-now-cta {
          padding: 57px 20px;
          position: relative;
          z-index: 10;
          font-style: normal;
          font-weight: 700;
          font-size: 20px;
          line-height: 24px;
          text-transform: uppercase;
          color: #FFFFFF;
          text-decoration: none;
          svg {
            margin-left: 16px;
            vertical-align: middle;
            transition: .3s ease;
          }
          &:hover {
            svg {
              transform: translate(4px, 4px);
            }
          }
        }
      }
    }

    @media (max-width: 550px) {
      .phone-icon {
        position: fixed;
        bottom: 20px;
        right: 20px;
        z-index: 10;
        img {
          border: 3px solid #13202E !important;     
          border-radius: 50%;
          background-color: #FFFFFF;
        }
        &:hover {
          transform: scale(1.05);
          cursor: pointer;
          border: 1px solid transparent !important;
          img {
            border: 3px solid #2FB6EF !important;
          }
        }
      }
    }
  }


  .hamburger-menu-btn-active {
    .hamburger-menu {
      background-color: #2FB6EF;
    }
  }
</style>