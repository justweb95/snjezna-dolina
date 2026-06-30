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
  <section id="hero" class="hero-section">
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
        <h1 class="hero-title">Apartmani na Jahorini <br class="desktop-br"> Uz samu <br class="mobile-br"> ski stazu</h1>
        <p class="sub-content">Boravak već od 60 € po noćenju</p>
        <ButtonAction 
          type="primary"
          text="Pogledajte apatmane"
          action="#apts"
        />

        <p class="hero-text">Doživite pravu zimsku čaroliju! Naši moderni apartmani nalaze se <br class="desktop-br"> tik uz ski lift – izađite iz smeštaja i odmah ste na stazi.</p>
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
        <a href="#location">
          <img 
            :src="mapIcon" 
            alt="Map icon"
            class="map-icon"/>
        </a>
      </div>
    </div>
  </section>
</template>

<style scoped>
  .mobile-br {
    display: none;
  }
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

        > *:not(.header-main) {
            opacity: 0;
            transform: translateY(10px);
            animation: textReveal 0.8s cubic-bezier(0.22, 1, 0.36, 1) forwards;
          }

        .badge {
          animation-delay: 0.1s;
        }

        .hero-title {
          animation-delay: 0.2s;
        }

        .sub-content {
          animation-delay: 0.3s;
        }

        .hero-text {
          animation-delay: 0.4s;
        }

        .hero-score {
          animation-delay: 0.5s;
        }

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
          padding: 8px 24px;
          background: #FAFAFA;
          border-radius: 6px;
          display: block;
          width: fit-content;
          margin: 0 auto;
          font-weight: 700;
          font-size: 18px;
          line-height: 23px;
          text-align: center;
        }

        .hero-text {
          font-size: 20px;
          display: block;
          max-width: 595px;
          text-align: center;
          margin: auto auto 32px;
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

          hr {
            width: 1px;
            height: 40px;
            background: #E4E9ED;
            border: none;
          }
          
          .guest-return {
            text-align: center;
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

        perspective: 1200px;

        .hero-img {
          width: 100%;
          height: auto;
          display: block;

          opacity: 0;
          filter: grayscale(100%);
          transform:
            rotateZ(-10deg)
            scale(1.1);

          transform-origin: center center;

          animation: imageEntry 1.3s cubic-bezier(0.22, 1, 0.36, 1) forwards;
          animation-delay: 0.2s;

          will-change: transform, filter, opacity;
        }

        .map-icon {
          position: absolute;
          bottom: 32px;
          right: 32px;
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
    }
  }

  @media (max-width: 1024px) {
    .hero-section {
      .header-main {
        margin-bottom: 48px;
      }
      .doli-container {
        flex-direction: column;

        .hero-content,
        .hero-image-holder {
          flex: 1 1 auto;
          max-width: 100%;

          .hero-text {
            max-width: 100%;
            font-size: 16px;
            line-height: 140%;
            margin: 48px auto 32px;
          }
        }
      }
    }
  }

  @media (max-width: 768px) {
    .desktop-br {
      display: none;
    }
    .mobile-br {
      display: inline;
    }
    .hero-section {
      padding: 16px 0;

      .doli-container {
        gap: 24px;

        .hero-content {
          .badge {
            padding: 8px 24px;
            font-size: 18px;
            line-height: 23px;
          }

          .hero-title {
            margin: 20px 0;
            font-size: 36px;
            line-height: 140%;
          }

          .sub-content {
            width: min(100%, 327px);
            margin: 0 auto;
            padding: 7px 24px;
            font-size: 16px;
            line-height: 22px;
            background: #FAFAFA;
            border-radius: 6px;
          }

          :deep(.btn.primary) {
            width: min(100%, 284px);
            margin: 12px auto 0;
            padding: 4px 24px 4px 4px;

            .button-icon {
              width: 40px;
              height: 40px;
              padding: 10px 13px;
            }

            .btn-text {
              font-size: 18px;
              line-height: 24px;
              padding-left: 52px;
            }
          }

          .hero-text {
            max-width: 100%;
            font-size: 16px;
            line-height: 140%;
            margin: 48px auto 0px;
          }

          .hero-score {
            display: none;
          }
        }

        .hero-image-holder {
          min-height: 400px;

          .hero-img {
            height: 400px;
            object-fit: cover;
          }

          .map-icon {
            width: 48px;
            height: 48px;
            right: 20px;
            bottom: 20px;
          }
        }
      }
    }
  }
</style>