<script setup>
  // Image imports
  import UsersFour from '../assets/images/icons/users_four.svg';
  import BedDouble from '../assets/images/icons/bed-double.svg';
  import Bathtub from '../assets/images/icons/bathtub.svg';
  import ArrowsOut from '../assets/images/icons/arrows_out.svg';
  import PlusIcon from '../assets/images/icons/plus-icon.svg';
  import MoneyWavy from '../assets/images/icons/money_wavy.svg';

  // Component imports
  import ButtonAction from '../components/ButtonAction.vue';

  // Props 
  const props = defineProps({
    aptData: {
      type: Object,
      required: true
    }
  })
</script>

<template>
  <article class="apts-content">
    <div class="apt-content-header">
      <div class="apt-cont-head-title">
        <h2 class="apt-title">{{ aptData.title }}</h2>
        <div class="apt-rev">
          <p class="apt-rating">{{ aptData.rating }}</p>
          <span class="apt-star-rating">
            <i class="star" v-for="n in 5" :key="n" :class="{ filled: n <= Math.round(aptData.rating) }">★</i>
          </span>
          <a class="apt-reviews">({{ aptData.reviews }} Reviews)</a>
        </div>
        <p class="apt-subtitle">{{ aptData.description }}</p>
      </div>
    </div>
    <div class="apt-unit-info">
      <div class="apt-unit-info-item">
        <img :src="PersonSimpleSky" alt="Apt Capacity Icon" class="apt-unit-icon"/>
        <h3 class="apt-unit-title">Maksimalno gostiju</h3>
        <p class="apt-unit-value">{{ aptData.capacity }} osobe</p>
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
      <div class="apt-unit-availability-item">
        <img :src="PersonSimpleSky" alt="Apt Capacity Icon" class="apt-unit-icon"/>
        <h3 class="apt-unit-title">Proveri dostupnost</h3>
        <button class="apt-availability-btn">
          <img :src="PlusIcon" alt="Check Availability Icon" class="apt-availability-icon"/>
        </button>
      </div>
      <div class="apt-unit-availability-item">
        <img :src="MoneyWavy" alt="Apt Capacity Icon" class="apt-unit-icon"/>
        <h3 class="apt-unit-title">Detaljni cenovnik</h3>
        <button class="apt-availability-btn">
          <img :src="PlusIcon" alt="Check Availability Icon" class="apt-availability-icon"/>
        </button>
      </div>
    </div>
    <div class="apt-cta">
      <ButtonAction 
        type="primary"
        text="Pogledajte apatmane"
        action="#apartmans"
      />
      <ButtonAction 
        type="primary"
        text="Pogledajte apatmane"
        action="#apartmans"
      />
    </div>
  </article>
</template>

<style scoped>

</style>