<script setup>
  // Image Imports
  import Header from '../layout/Header.vue';
  import locationBadge from '../assets/images/home/location-badge.svg';
  import mapIcon from '../assets/images/home/map-icon.svg';
  import heroImage from '../assets/images/home/hero-image.webp';
  import guestFavorite from '../assets/images/home/guest-favorite.svg';

  // Button imports
  import ButtonAction from '../components/ButtonAction.vue';
  

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
        <ButtonAction 
          type="primary"
          text="Pogledajte apatmane"
          action="#apartmans"
        />

        <p class="hero-text">Doživite pravu zimsku čaroliju! Naši moderni apartmani nalaze se tik uz ski lift – izađite iz smeštaja i odmah ste na stazi.</p>
        <div class="hero-score">
          <img class="guest-favorite"
            :src="guestFavorite" 
            alt="Guest favorite icon"
          />
          <span class="guest-return">
            <h3>80%</h3>
            <p>Povratak</p>
          </span>
          <hr>
          <span class="guest-return">
            <h3>4.9</h3>
            <p>Ocena</p>
          </span>
          <hr>
          <span class="guest-return">
            <h3>24/7</h3>
            <p>Podrška</p>
          </span>
        </div>
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
          margin: auto auto 0;
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
        .hero-text {
          text-align: center;
          margin-top: auto;
        }
        .hero-score {
          display: flex;
          justify-content: flex-end;
          align-items: center;
          gap: 32px;
          padding: 24px 32px;
          border: 1px solid #E4E9ED;
          border-radius: 20px;
          .guest-favorite {
            margin-right: auto;
          }
          .guest-return {
            h3 {
              font-size: 18px;
              line-height: 32px;
              font-weight: 700;
            }
            p {
              font-size: 12px;
              line-height: auto;
              font-weight: 400;
            }
          }
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