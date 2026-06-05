<script setup>
  import ButtonAction from '../components/ButtonAction.vue';
</script>

<template>
  <section class="special-section">
    <div class="special-container doli-container">
      <div class="special-wrapper">
        <h2 class="special-section-title">Specijalna ponuda</h2>
        <p class="special-section-subtitle">Rezervišite 30+ dana unapred i uštedite 15%</p>
        <ButtonAction 
          type="primary"
          text="Rezerviši odmah"
          action="#apts"
        />
      </div>
    </div>

  </section>
</template>

<style scoped>
  .special-section {
    padding: 24px 0px;
    .special-container {
      .special-wrapper {
        padding: 80px 20px;
        background-image: url('../assets/images/home/special_cover.webp');
        background-size: cover;
        background-position: center;
        background-repeat: no-repeat;
        border-radius: 24px;
        .special-section-title {
          width: fit-content;
          margin: 0 auto;
          position: relative;
          font-style: normal;
          font-weight: 400;
          font-size: 18px;
          line-height: 140%;
          color: #FFFFFF;
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
            background-color: #FFFFFF;
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
            background-color: #FFFFFF;
          }
        }
        .special-section-subtitle {
          max-width: 530px;
          margin: 20px auto 40px;
          font-style: normal;
          font-weight: 600;
          font-size: 48px;
          line-height: 130%;
          text-align: center;
          color: #FFFFFF;
        }
      }
    }
    @keyframes titleDotPop {
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

    @media (prefers-reduced-motion: reduce) {
      .special-section-title::after {
        animation: none;
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