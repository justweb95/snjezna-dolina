<script setup>
  import { ref } from 'vue';

  // Image imports
  import UsersFour from '../assets/images/icons/users_four_small.svg';
  import BedDouble from '../assets/images/icons/bed-double.svg';
  import Bathtub from '../assets/images/icons/bathtub.svg';
  import ArrowsOut from '../assets/images/icons/arrows_out.svg';
  import PlusIcon from '../assets/images/icons/plus-icon.svg';
  import MoneyWavy from '../assets/images/icons/money_wavy_small.svg';
  import CalendarIcon from '../assets/images/icons/calendar_check.svg';

  // Component imports
  import ButtonAction from '../components/ButtonAction.vue';
  import AvailabilityModal from '../components/AvailabilityModal.vue';
  import PricingModal from '../components/PricingModal.vue';

  // Props 
  const props = defineProps({
    aptData: {
      type: Object,
      required: true
    }
  });

  const isAvailabilityModalOpen = ref(false);
  const isPricingModalOpen = ref(false);

  const openAvailabilityModal = () => {
    isAvailabilityModalOpen.value = true;
  };

  const closeAvailabilityModal = () => {
    isAvailabilityModalOpen.value = false;
  };

  const openPricingModal = () => {
    isPricingModalOpen.value = true;
  };

  const closePricingModal = () => {
    isPricingModalOpen.value = false;
  };
</script>

<template>
  <article class="apts-content">
    <div class="apt-content-header">
      <span class="apt-title-holder">
        <h2 class="apt-title">{{ aptData.title }}</h2>
        <p class="apt-price">{{ aptData.price }}€/ noć</p>
      </span>
      <div class="apt-rev">
        <p class="apt-rating">{{ aptData.rating }}</p>
        <span class="apt-star-rating">
          <svg class="star" v-for="n in 5" :key="n" width="14" height="14" viewBox="0 0 14 14" fill="none" xmlns="http://www.w3.org/2000/svg">
            <path d="M13.4062 5.77127C13.865 5.42417 13.6196 4.69274 13.0442 4.69274H9.16789C8.90478 4.69274 8.67237 4.52133 8.59466 4.26996L7.40526 0.422765C7.23099 -0.140942 6.43308 -0.140944 6.2588 0.422764L5.0694 4.26996C4.99169 4.52133 4.75928 4.69274 4.49617 4.69274H0.601862C0.0283515 4.69274 -0.218289 5.42027 0.236982 5.76904L3.43452 8.2186C3.63344 8.37099 3.71671 8.63095 3.64335 8.87056L2.44711 12.7775C2.2762 13.3357 2.92227 13.7845 3.3857 13.4294L6.46715 11.0688C6.68245 10.9039 6.98162 10.9039 7.19691 11.0688L10.2714 13.4241C10.7355 13.7796 11.3822 13.3291 11.2095 12.7706L9.9963 8.84641C9.92171 8.60515 10.0062 8.34301 10.2076 8.19066L13.4062 5.77127Z" fill="#FFAD33"/>
          </svg>
        </span>
        <a class="apt-reviews">({{ aptData.reviews }} Reviews)</a>
      </div>
      <p class="apt-subtitle">{{ aptData.description }}</p>
    </div>
    <div class="apt-unit-info">
      <div class="apt-unit-info-item">
        <img :src="UsersFour" alt="Apt Capacity Icon" class="apt-unit-icon"/>
        <h3 class="apt-unit-title">Maksimalno gostiju</h3>
        <p class="apt-unit-value">{{ aptData.capacity }}</p>
      </div>
      <div class="apt-unit-info-item">
        <img :src="BedDouble" alt="Apt Capacity Icon" class="apt-unit-icon"/>
        <h3 class="apt-unit-title">Spavaće sobe</h3>
        <p class="apt-unit-value">{{ aptData.rooms }}</p>
      </div>
      <div class="apt-unit-info-item">
        <img :src="Bathtub" alt="Apt Capacity Icon" class="apt-unit-icon"/>
        <h3 class="apt-unit-title">Broj kupatila</h3>
        <p class="apt-unit-value">{{ aptData.bathrooms }}</p>
      </div>
      <div class="apt-unit-info-item">
        <img :src="ArrowsOut" alt="Apt Capacity Icon" class="apt-unit-icon"/>
        <h3 class="apt-unit-title">Površina</h3>
        <p class="apt-unit-value">{{ aptData.area }} m²</p>
      </div>
    </div>
    <div class="apt-unit-availability">
      <div class="apt-unit-availability-item" role="button" tabindex="0" @click="openAvailabilityModal" @keydown.enter="openAvailabilityModal" @keydown.space.prevent="openAvailabilityModal">
        <img :src="CalendarIcon" alt="Apt Capacity Icon" class="apt-unit-icon"/>
        <h3 class="apt-unit-title">Proveri dostupnost</h3>
        <button class="apt-availability-btn" type="button" @click.stop="openAvailabilityModal">
          <img :src="PlusIcon" alt="Check Availability Icon" class="apt-availability-icon"/>
        </button>
      </div>
      <div class="apt-unit-availability-item" role="button" tabindex="0" @click="openPricingModal" @keydown.enter="openPricingModal" @keydown.space.prevent="openPricingModal">
        <img :src="MoneyWavy" alt="Apt Capacity Icon" class="apt-unit-icon"/>
        <h3 class="apt-unit-title">Detaljni cenovnik</h3>
        <button class="apt-availability-btn" type="button" @click.stop="openPricingModal">
          <img :src="PlusIcon" alt="Check Availability Icon" class="apt-availability-icon"/>
        </button>
      </div>
    </div>
    <div class="apt-cta">
      <ButtonAction 
        type="primary"
        text="Rezerviši"
        action="href='tel:+38162204003'"
      />
      <ButtonAction 
        type="button-phone"
        text="Pozovi nas"
        action="href='tel:+38162204003'"
      />
    </div>
  </article>

  <AvailabilityModal :isOpen="isAvailabilityModalOpen" @close="closeAvailabilityModal" />
  <PricingModal :isOpen="isPricingModalOpen" @close="closePricingModal" />
</template>

<style scoped>
  .apts-content {
    flex: 1 0 45%;
    
    display: flex;
    flex-direction: column;
    gap: 32px;

    padding: 40px;
    background: #FFFFFF;
    border: 1px solid #E4E9ED;
    border-radius: 20px;


    max-width: 768px;
    .apt-content-header {
      display: flex;
      flex-direction: column;
      gap: 12px;
      .apt-title-holder {
        display: flex;
        gap: 12px;
        align-items: center;
        justify-content: space-between;
        .apt-title {
          font-style: normal;
          font-weight: 700;
          font-size: 24px;
          line-height: 130%;
          color: #081B35;}
        .apt-price {
          font-style: normal;
          font-weight: 700;
          font-size: 24px;
          line-height: 130%;
          color: #081B35;
        }
      }
      .apt-rev {
        display: flex;
        gap: 6px;
        .apt-rating {
          font-style: normal;
          font-weight: 600;
          font-size: 16px;
          line-height: 145%;
          color: #081B35;
        }
        .apt-star-rating {
          .star {
            vertical-align: middle;
          }
        }
        .apt-reviews {
          font-style: normal;
          font-weight: 400;
          font-size: 12px;
          line-height: 21px;
          color: #62686F;
        }
      }
      .apt-subtitle {
        width: 100%;
        font-style: normal;
        font-weight: 400;
        font-size: 16px;
        line-height: 150%;
        color: #081B35;
      }
    }
    .apt-unit-info {
      display: flex;
      flex-wrap: wrap;
      gap: 0px;
      .apt-unit-info-item {
        flex: 1 0 50%;
        padding: 16px 20px 16px 16px;
        border: 1px solid #E4E9ED;

        display: flex;
        justify-content: flex-start;
        align-items: center;
        gap: 12px;

        .apt-unit-title {
          font-style: normal;
          font-weight: 400;
          font-size: 18px;
          line-height: 24px;
          color: #081B35;
        }
        .apt-unit-value {
          margin-left: auto;
          font-style: normal;
          font-weight: 700;
          font-size: 18px;
          line-height: 24px;
          color: #081B35;
        }
        &:nth-of-type(1) {
          border-radius: 12px 0 0 0;
        }
        &:nth-of-type(2) {
          border-radius: 0 12px 0 0;
        }
        &:nth-of-type(3) {
          border-radius: 0 0 0 12px;
        }
        &:nth-of-type(4) {
          border-radius: 0 0 12px 0;
        }
      }
    }
    .apt-unit-availability {
      display: flex;
      flex-direction: column;
      gap: 8px;
      .apt-unit-availability-item {
        padding: 16px;
        background: #FAFAFA;

        display: flex;
        align-items: center;
        gap: 12px;
        border-radius: 12px;
        .apt-unit-title {
          transition: 0.3s ease;
          font-style: normal;
          font-weight: 400;
          font-size: 18px;
          line-height: 24px;
          color: #081B35;
        }
        .apt-availability-btn {
          border: none;
          background: transparent;
          margin-left: auto;
          transition: transform 0.3s ease;
          img {
            vertical-align: middle;
            cursor: pointer;
          }
        }
        &:hover {
          cursor: pointer;
          .apt-availability-btn {
            transform: rotate(90deg);
          }
        }
      }
    }
    .apt-cta {
      margin-top: 8px;
      display: flex;
      gap: 16px;
      .btn {
        margin: 0px;
      }
    }
  }

  @media (max-width: 1024px) {
    .apts-content {
      max-width: 100%;
      flex: 1 0 100%;
    }
  }

  @media (max-width: 550px) {
    .apts-content {
      padding: 32px 20px;
      .apt-content-header{
        .apt-title-holder {
          .apt-title, .apt-price {
            font-size: 20px;
          }
        }
      }
      .apt-unit-info {
        justify-content: space-between;
        .apt-unit-info-item {
          border: none;
          flex: 1 0 22%;
          padding: 0;
          gap: 0px;
          .apt-unit-title {
            display: none;
          }
          .apt-unit-value{
            margin-left: 12px;
          }
          &:last-of-type {
            flex: 1 0 25%;
          }
        }
      }
    }
    .apt-cta {
      justify-content: space-between;
    }
  }
</style>