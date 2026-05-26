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
        <h2 class="subhero-title">Zašto naši apartmani na Jahorini?</h2>
        <h3 class="subhero-subtitle">Doživite vrhunac zimske magije u Snježnoj Dolini</h3>
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
    padding: 100px 0px;

    background-size: cover;
    background-position: center;
    background-repeat: no-repeat;
    background-image: url('../assets/images/home/subhero-bg-image.webp');
    .subhero-holder {
      display: flex;
      justify-content: space-between;
      min-height: 700px;
      gap: 24px;
      .subhero-content {
        flex: 1 0 45%;
        .subhero-title {
          position: relative;
          font-style: normal;
          font-weight: 400;
          font-size: 20px;
          line-height: 140%;
          color: #FFFFFF;
          margin-left: 20px;
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
        }
        .subhero-subtitle {
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

          .legend-title {
            width: 110px;
            font-style: normal;
            font-weight: 700;
            font-size: 48px;
            line-height: 60px;
            color: #13202E;
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
</style>





