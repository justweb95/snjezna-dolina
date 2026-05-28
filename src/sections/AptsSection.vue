<script setup>
  import AptsGallery from "../components/AptsGallery.vue";
  import AptsContent from "../components/AptsContent.vue";

  import { apartments } from "../data/aptData";

</script>

<template>
  <section class="apts-section">
    <div class="doli-container">
      <h2 class="apts-section-title">Karakteristike</h2>
      <h3 class="apts-section-subtitle">Apartmani u ponudi</h3>
      
      <div class="apts-list">

        <!-- First Apartment -->
        <div class="single-apt">
          <AptsGallery :aptGallery="apartments[0].gallery" />
          <AptsContent :aptData="apartments[0]" />
        </div>
      
        <!-- Second Apartment -->
        <div class="single-apt">
          <AptsContent :aptData="apartments[1]" />
          <AptsGallery :aptGallery="apartments[1].gallery" />
        </div>
      </div>

    </div>
  </section>
</template>

<style scoped>
  .apts-section {
    padding: 100px 0 24px;
    .doli-container {
      .apts-section-title {
        position: relative;
        width: fit-content;
        margin: 0 auto ;
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
          background-color: #081B35;
        }
      }
      .apts-section-subtitle {
        font-style: normal;
        font-weight: 600;
        font-size: 48px;
        line-height: 60px;
        text-align: center;
        color: #081B35;
      }
      .apts-list {
        margin-top: 60px;
        display: flex;
        flex-direction: column;
        gap: 60px;
        .single-apt {
          display: flex;
          gap: 24px;
        }
      }
    }
  }
</style>