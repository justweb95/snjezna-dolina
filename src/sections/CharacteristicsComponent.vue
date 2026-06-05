<script setup>
  import CouchIcon from '../assets/images/icons/couch.svg';
  import OvenIcon from '../assets/images/icons/oven.svg';
  import Bathtub from '../assets/images/icons/bathtub.svg';
  import WifiHighIcon from '../assets/images/icons/wifi_high.svg';
  import TelevisionIcon from '../assets/images/icons/television.svg';
  import CoatHangerIcon from '../assets/images/icons/coat_hanger.svg';
  import CarIcon from '../assets/images/icons/car.svg';
  import WavesIcon from '../assets/images/icons/waves.svg';
  import SecurityCameraIcon from '../assets/images/icons/security_camera.svg';

  const mainCharacteristics = [
    {
      title: 'Prostrani dnevni boravak',
      icon: CouchIcon,
      alt: 'Couch Icon'
    },
    {
      title: 'Opremljena kuhinja',
      icon: OvenIcon,
      alt: 'Oven Icon'
    },
    {
      title: 'Komforno kupatilo',
      icon: Bathtub,
      alt: 'Bathtub Icon'
    }
  ];

  const leftAmenities = [
    {
      title: 'Brzi Wi-Fi',
      icon: WifiHighIcon,
      alt: 'WiFi Icon'
    },
    {
      title: 'Smart TV',
      icon: TelevisionIcon,
      alt: 'Television Icon'
    },
    {
      title: 'Veš mašina',
      icon: Bathtub,
      alt: 'Amenity Icon'
    }
  ];

  const rightAmenities = [
    {
      title: 'Parking',
      icon: CarIcon,
      alt: 'Car Icon'
    },
    {
      title: 'Podno grejanje',
      icon: WavesIcon,
      alt: 'Waves Icon'
    },
    {
      title: 'Sigurnosna oprema',
      icon: SecurityCameraIcon,
      alt: 'Security Camera Icon'
    }
  ];
</script>

<template>
  <section class="characteristics-section">
    <div class="doli-container">
      <div class="characteristics-wrapper">
        <div class="characteristics-heading">
          <h2 class="characteristics-section-title">Karakteristike</h2>
          <h3 id="characteristics" class="characteristics-section-subtitle">Opremljenost apartmana</h3>
        </div>

        <div class="characteristics-content">
          <ul class="main-characteristics">
            <li
              v-for="item in mainCharacteristics"
              :key="item.title"
              class="main-characteristics-item"
            >
              <span class="main-char-item-icon-holder">
                <img :src="item.icon" :alt="item.alt" class="main-char-item-icon"/>
              </span>
              <p class="main-char-item-text">{{ item.title }}</p>
            </li>
          </ul>

          <div class="additional-characteristics-layout">
            <ul class="additional-characteristics additional-characteristics--side">
              <li
                v-for="item in leftAmenities"
                :key="item.title"
                class="additional-characteristics-item"
              >
                <p class="additional-char-item-text">{{ item.title }}</p>
                <img :src="item.icon" :alt="item.alt" class="additional-char-item-icon"/>
              </li>
            </ul>

            <div class="featured-characteristic">
              <img :src="CoatHangerIcon" alt="Coat Hanger Icon" class="featured-characteristic-icon"/>
              <p class="featured-characteristic-text">Komplet osnovnih potrebština</p>
            </div>

            <ul class="additional-characteristics additional-characteristics--side">
              <li
                v-for="item in rightAmenities"
                :key="item.title"
                class="additional-characteristics-item"
              >
                <p class="additional-char-item-text">{{ item.title }}</p>
                <img :src="item.icon" :alt="item.alt" class="additional-char-item-icon"/>
              </li>
            </ul>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<style scoped>
  .characteristics-section {
    padding: 100px 0px;
    background: #FFFFFF;

    .characteristics-wrapper {
      display: flex;
      flex-direction: column;
      gap: 60px;
    }

    .characteristics-heading {
      display: flex;
      flex-direction: column;
      align-items: center;
      gap: 16px;
    }

    .characteristics-section-title {
      position: relative;
      width: fit-content;
      margin: 0 auto;
      font-style: normal;
      font-weight: 400;
      font-size: 20px;
      line-height: 140%;
      text-align: center;
      color: #081B35;

      &::before {
        position: absolute;
        left: -20px;
        top: 50%;
        transform: translateY(-50%);
        content: '';
        border-radius: 50%;
        display: block;
        width: 8px;
        height: 8px;
        background-color: #13202E;
      }

      &::after {
        position: absolute;
        left: -20px;
        top: 50%;
        transform: translateY(-50%);
        transform-origin: center;
        animation: titleDotPopGlobal 1.6s cubic-bezier(0.16, 1, 0.3, 1) infinite;
        content: '';
        border-radius: 50%;
        display: block;
        width: 8px;
        height: 8px;
        background-color: #13202E;
      }
    }

    .characteristics-section-subtitle {
      width: 100%;
      font-style: normal;
      font-weight: 600;
      font-size: 48px;
      line-height: 60px;
      text-align: center;
      color: #081B35;
    }

    .characteristics-content {
      display: flex;
      flex-direction: column;
      gap: 40px;
    }

    .main-characteristics {
      display: grid;
      grid-template-columns: repeat(3, minmax(0, 1fr));
      gap: 16px;
    }

    .main-characteristics-item {
      display: flex;
      align-items: center;
      gap: 24px;
      min-height: 104px;
      padding: 24px 24px 24px 32px;
      background: #FFFFFF;
      border: 1px solid #E4E9ED;
      border-radius: 20px;
    }

    .main-char-item-icon-holder {
      display: inline-flex;
      align-items: center;
      justify-content: center;
      width: 56px;
      height: 56px;
      flex-shrink: 0;
      border-radius: 80px;
      background: rgba(19, 32, 46, 0.06);
    }

    .main-char-item-icon {
      width: 32px;
      height: 32px;
    }

    .main-char-item-text {
      flex: 1;
      font-style: normal;
      font-weight: 700;
      font-size: 24px;
      line-height: 140%;
      color: #081B35;
    }

    .additional-characteristics-layout {
      display: grid;
      grid-template-columns: repeat(3, minmax(0, 1fr));
      gap: 16px;
      align-items: stretch;
    }

    @media (prefers-reduced-motion: reduce) {
      .characteristics-section-title::after {
        animation: none;
      }
    }

    .additional-characteristics {
      display: flex;
      flex-direction: column;
      gap: 16px;
      min-width: 0;
    }

    .additional-characteristics-item {
      display: flex;
      align-items: center;
      gap: 32px;
      min-height: 80px;
      padding: 24px 24px 24px 32px;
      background: #FFFFFF;
      border: 1px solid #E4E9ED;
      border-radius: 20px;
    }

    .additional-char-item-text {
      flex: 1;
      font-style: normal;
      font-weight: 600;
      font-size: 20px;
      line-height: 25px;
      color: #081B35;
    }

    .additional-char-item-icon {
      width: 32px;
      height: 32px;
      flex-shrink: 0;
    }

    .featured-characteristic {
      display: flex;
      flex-direction: column;
      justify-content: center;
      align-items: center;
      gap: 12px;
      min-height: 272px;
      padding: 24px 32px;
      background: #FFFFFF;
      border: 1px solid #E4E9ED;
      border-radius: 20px;
      text-align: center;
    }

    .featured-characteristic-icon {
      width: 32px;
      height: 32px;
    }

    .featured-characteristic-text {
      max-width: 240px;
      font-style: normal;
      font-weight: 600;
      font-size: 20px;
      line-height: 140%;
      color: #081B35;
    }
    @media (max-width: 1200px) {
      .main-characteristics {
        grid-template-columns: 1fr;
      }

      .additional-characteristics-layout {
        grid-template-columns: 1fr;
      }
    }

    @media (max-width: 768px) {
      padding: 80px 0px;

      .characteristics-wrapper {
        gap: 40px;
      }

      .characteristics-section-title {
        font-size: 18px;
      }

      .characteristics-section-subtitle {
        font-size: 34px;
        line-height: 44px;
      }

      .main-characteristics-item,
      .additional-characteristics-item,
      .featured-characteristic {
        padding: 20px;
      }

      .main-characteristics-item {
        gap: 16px;
      }

      .main-char-item-text {
        font-size: 20px;
      }

      .additional-char-item-text,
      .featured-characteristic-text {
        font-size: 18px;
        line-height: 24px;
      }
    }
  }

  @keyframes titleDotPopGlobal {
    0% {
      transform: translateY(-50%) scale(1);
      opacity: 0.7;
    }

    70%,
    100% {
      transform: translateY(-50%) scale(2.6);
      opacity: 0;
    }
  }
</style>