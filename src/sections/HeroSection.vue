<script setup>
  // Image Imports
  import Header from '../layout/Header.vue';
  import locationBadge from '../assets/images/home/location-badge.svg';
  import mapIcon from '../assets/images/home/map-icon.svg';
  import heroImage from '../assets/images/home/hero-image.webp';
  

</script>

<template>
  <section class="hero-section">
    <div class="doli-container">
      <div class="hero-content">
        <Header />
        <span class="badge">
          <img 
            :src="locationBadge" 
            alt="Location badge"
            class="badge-icon"/>
          Jahorina, BIH
        </span>
        <h1 class="hero-title">Apartmani na Jahorini <br> Uz samu ski stazu</h1>
        <p class="sub-content">Boravak već od 60 € po noćenju</p>
        
      </div>
      
      <div class="hero-image-holder">
        <img 
          :src="heroImage" 
          alt="Hero image"
          class="hero-img"/>

          <img 
          :src="mapIcon" 
          alt="Map icon"
          class="map-icon"/>
      </div>
    </div>
  </section>
</template>

<style scoped>
  .hero-section {
    padding: 24px 0px;
    .doli-container {
      display: flex;
      gap: 24px;
      .hero-content {
        flex: 1 0 49%;
        max-width: 768px;
        display: flex;
        flex-direction: column;
        .badge {
          width: fit-content;
          margin: 0px auto;
          display: flex;
          justify-content: center;
          align-items: center;
          padding: 8px 24px;
          gap: 12px;
          border: 1px solid #E4E9ED;
          border-radius: 40px;
        }
        .hero-title {
          margin: 24px 0 28px;
          text-transform: uppercase;
          text-align: center;
        }
        .sub-content {
          font-weight: 700;
          font-size: 18px;
          line-height: 23px;
          text-align: center;
        }
      }
      .hero-image-holder {
        position: relative;
        flex: 1 0 49%;
        max-width: 768px;

        border-radius: 20px;
        overflow: hidden;
        .hero-img {
          width: 100%;
          height: auto;
          display: block;
        }
        .map-icon {
          position: absolute;
          bottom: 32px;
          right: 32px;
        }
      }
    }
  }
</style>