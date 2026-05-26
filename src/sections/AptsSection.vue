<script setup>

</script>

<template>
  <section class="apts-section">
    <div class="doli-container">
      <h2 class="apts-section-title">Zašto naši apartmani na Jahorini?</h2>
      <h3 class="apts-section-subtitle">Doživite vrhunac zimske magije u Snježnoj Dolini</h3>
      
      <div class="apts-list">

        <!-- First Apartment -->
        <div class="single-apt">
          <AptsGalery :aptGallery="galleryData" />
          <AptsContent :aptData="aptData" />
        </div>
      
        <!-- Second Apartment -->
        <div class="single-apt">
          <AptsGalery :aptGallery="galleryData" />
          <AptsContent :aptData="aptData" />
        </div>
      </div>

    </div>
  </section>
</template>

<style scoped>

</style>