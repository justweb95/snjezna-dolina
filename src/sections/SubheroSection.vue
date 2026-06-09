<script setup>
  import PersonSimpleSky from '../assets/images/icons/person_simple_sky.svg';
  import BuildingOffice from '../assets/images/icons/building_office.svg';
  import UsersFour from '../assets/images/icons/users_four.svg';
  import MoneyWavy from '../assets/images/icons/money_wavy.svg';
</script>

<template>
  <section class="subhero-section">
    <div class="subhero-holder doli-container">
      <div class="subhero-content">
        <div class="subhero-sticky">
          <h2 class="subhero-title">Zašto naši apartmani na Jahorini?</h2>
          <h3 class="subhero-subtitle">Doživite vrhunac zimske magije u Snježnoj Dolini</h3>
        </div>
      </div>
      <div class="subhero-legend">
        <div class="legend-item">
          <h3 class="legend-title">30m</h3>
          <p class="legend-text">Direktan pristup stazi sa praga apartmana</p>
          <img :src="PersonSimpleSky" alt="Legend icon 1" class="legend-icon"/>
        </div>
        <div class="legend-item">
          <h3 class="legend-title">x 2</h3>
          <p class="legend-text">Komforni apartmani sa modernim enterijerom</p>
          <img :src="BuildingOffice" alt="Legend icon 2" class="legend-icon"/>
        </div>
        <div class="legend-item">
          <h3 class="legend-title">2 x 4</h3>
          <p class="legend-text">Pogodno za porodice, parove i grupne posete</p>
          <img :src="UsersFour" alt="Legend icon 3" class="legend-icon"/>
        </div>
        <div class="legend-item">
          <h3 class="legend-title">60 €</h3>
          <p class="legend-text">Najpovoljnije cene Smeštaja na jahorini</p>
          <img :src="MoneyWavy" alt="Legend icon 4" class="legend-icon"/>
        </div>
      </div>
    </div>
  </section>
</template>

<style scoped>
  .subhero-section {
    overflow: clip;
    padding: 100px 0px;
    background-size: 150%;
    background-position: center;
    background-repeat: no-repeat;
    background-image: url('../assets/images/home/subhero-bg-image.webp');
    animation: subhero-zoom linear both;
    animation-timeline: view();
    animation-range: entry 0% cover 55%;
    .subhero-holder {
      display: flex;
      justify-content: space-between;
      min-height: 700px;
      gap: 24px;
      .subhero-content {
        flex: 1 0 45%;
        position: relative;
        .subhero-sticky {
          position: sticky;
          top: 40px;
        }
        .subhero-title {
          font-style: normal;
          font-weight: 400;
          font-size: 20px;
          line-height: 140%;
          color: #FFFFFF;
          margin-left: 20px;
          &::before {
            position: absolute;
            left: 0px;
            top: 10px;
            content: '';
            border-radius: 50%;
            display: block;
            width: 8px;
            height: 8px;
            background-color: #FFFFFF;
          }

          &::after {
            position: absolute;
            left: 0px;
            top: 15px;
            transform: translateY(-50%);
            transform-origin: center;
            animation: titleDotPop 1.6s cubic-bezier(0.16, 1, 0.3, 1) infinite;
            content: '';
            border-radius: 50%;
            display: block;
            width: 8px;
            height: 8px;
            background-color: #FFFFFF;
          }
        }
        .subhero-subtitle {
          margin-top: 16px;
          max-width: 690px;
          font-style: normal;
          font-weight: 600;
          font-size: 48px;
          line-height: 140%;
          color: #FFFFFF;
        }
      }
      .subhero-legend {
        flex: 1 0 45%;
        max-width: 768px;
        margin-top: auto;
        display: flex;
        flex-direction: column;
        align-items: flex-start;
        background: #FFFFFF;
        border-radius: 20px;
        .legend-item {
          padding: 24px 36px;
          width: 100%;
          display: flex;
          justify-content: space-between;
          border-bottom: 1px solid #E4E9ED;

          .legend-title {
            width: 110px;
            font-style: normal;
            font-weight: 700;
            font-size: 48px;
            line-height: 60px;
            color: #101C2A;
          }
          .legend-text {
            max-width: 240px;
            font-weight: 700;
            font-size: 20px;
            line-height: 140%;
          }
          .legend-icon {
            max-width: 64px;
            max-height: 64px;
          }
        }
      }
    }
  }

  @keyframes subhero-zoom {
    from { background-size: 250%; }
    to { background-size: 150%; }
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
    .subhero-title::after {
      animation: none;
    }
  }

  @media (max-width: 1024px) {
    .subhero-section {
      .subhero-holder {
        flex-direction: column;
        min-height: auto;

        .subhero-content,
        .subhero-legend {
          flex: 1 1 auto;
          max-width: 100%;
        }
      }
    }
  }

  @media (max-width: 768px) {
    .subhero-section {
      padding: 56px 0 60px;
      background-size: cover !important;

      .subhero-holder {
        gap: 48px;

        .subhero-content {
          display: flex;
          flex-direction: column;
          align-items: center;
          gap: 16px;

          .subhero-title {
            margin: 0;
            font-size: 18px;
            line-height: 140%;
            text-align: center;
          }

          .subhero-subtitle {
            margin-top: 16px !important;
            margin: 0;
            max-width: 358px;
            font-size: 36px;
            line-height: 140%;
            text-align: center;
          }
        }

        .subhero-legend {
          border-radius: 20px;
          overflow: hidden;

          .legend-item {
            flex-wrap: wrap;
            flex-direction: column;
            justify-content: center;
            align-content: space-between;
            height: 145px;
            padding: 20px 24px;
            gap: 6px;
            border-bottom: 1px solid #E4E9ED;

            &:last-child {
              border-bottom: 0;
            }

            .legend-title {
              width: 96px;
              font-size: 32px;
              line-height: 40px;
            }

            .legend-text {
              max-width: 240px;
              font-size: 18px;
              line-height: 140%;
            }

            .legend-icon {
              width: 56px;
              height: 56px;
              max-width: 56px;
              max-height: 56px;
            }
          }
        }
      }
    }
  }
</style>





