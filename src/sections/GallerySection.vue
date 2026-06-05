<script setup>
  // Image imports
  import GalleryImage_1 from '../assets/images/gallery/Gallery_1.webp';
  import GalleryImage_2 from '../assets/images/gallery/Gallery_2.webp';
  import GalleryImage_3 from '../assets/images/gallery/Gallery_3.webp';
  import GalleryImage_4 from '../assets/images/gallery/Gallery_4.webp';
  import GalleryImage_5 from '../assets/images/gallery/Gallery_5.webp';
  import GalleryImage_6 from '../assets/images/gallery/Gallery_6.webp';
  import GalleryImage_7 from '../assets/images/gallery/Gallery_7.webp';
  import GalleryImage_8 from '../assets/images/gallery/Gallery_8.webp';
  import GalleryImage_9 from '../assets/images/gallery/Gallery_9.webp';
  import GalleryImage_10 from '../assets/images/gallery/Gallery_10.webp';
  import GalleryImage_11 from '../assets/images/gallery/Gallery_11.webp';
  import GalleryImage_12 from '../assets/images/gallery/Gallery_12.webp';
  // Import components
  import ButtonAction from '../components/ButtonAction.vue';

  const galleryImages = [
    GalleryImage_1,
    GalleryImage_2,
    GalleryImage_3,
    GalleryImage_4,
    GalleryImage_5,
    GalleryImage_6,
    GalleryImage_7,
    GalleryImage_8,
    GalleryImage_9,
    GalleryImage_10,
    GalleryImage_11,
    GalleryImage_12,
  ];

  // Duplicate one full sequence for seamless infinite scrolling.
  const galleryTrackImages = [...galleryImages, ...galleryImages];
</script>

<template>
  <section class="gallery-section">
    <div class="gallery-container doli-container">
      <div class="gallery-heading-wrap">
        <div class="gallery-kicker-wrap">
          <h2 class="gallery-section-title">Galerija</h2>
        </div>

        <p class="gallery-section-subtitle">Uživajte u zimskom raju</p>

        <p class="gallery-desct">
          Jahorina je poznata po vrhunskim ski stazama, čistom planinskom vazduhu i nezaboravnim panoramama.
          Posle dana provedenog na snegu, opustite se u toplini apartmana i uživajte u pogledu.
        </p>

        <ButtonAction
          type="secondary"
          text="Rezerviši odmah"
          action="#apts"
        />
      </div>

      <div class="gallery-wrapper">
        <div class="gallery-track">
          <img
            v-for="(image, index) in galleryTrackImages"
            :key="`${index}-${image}`"
            :src="image"
            alt="Galerija slika apartmana"
            class="gallery-image"
            loading="lazy"
            decoding="async"
            fetchpriority="low"
          />
        </div>
      </div>
    </div>
  </section>
</template>

<style scoped>
  .gallery-section {
    overflow: hidden;
    display: flex;
    flex-direction: column;
    align-items: center;
    padding: 100px 0 24px;
    gap: 120px;
    background: #13202E;

    .gallery-container {
      display: flex;
      flex-direction: column;
      align-items: center;
      gap: 100px;
      width: 100%;
      max-width: none;

      .gallery-heading-wrap {
        display: flex;
        flex-direction: column;
        align-items: center;
        gap: 40px;
        width: 100%;

        .gallery-kicker-wrap {
          display: flex;
          align-items: center;
          justify-content: center;
          gap: 0;

          .gallery-section-title {
            position: relative;
            margin: 0;
            margin-left: 20px;
            font-family: 'Plus Jakarta Sans';
            font-style: normal;
            font-weight: 400;
            font-size: 20px;
            line-height: 140%;
            color: #B9C1CA;

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
              background-color: #B9C1CA;
            }

            &::after {
              position: absolute;
              left: -20px;
              top: 50%;
              transform: translateY(-50%);
              transform-origin: center;
              animation: titleDotPop 1.6s cubic-bezier(0.16, 1, 0.3, 1) infinite;
              content: '';
              border-radius: 50%;
              display: block;
              width: 8px;
              height: 8px;
              background-color: #B9C1CA;
            }
          }
        }

        .gallery-section-subtitle {
          margin: 0;
          max-width: 100%;
          font-family: 'Plus Jakarta Sans';
          font-style: normal;
          font-weight: 600;
          font-size: 48px;
          line-height: 60px;
          text-align: center;
          color: #FFFFFF;
        }

        .gallery-desct {
          max-width: 968px;
          margin: 0;
          font-family: 'Plus Jakarta Sans';
          font-style: normal;
          font-weight: 400;
          font-size: 20px;
          line-height: 140%;
          text-align: center;
          color: #B9C1CA;
        }
      }

      .gallery-wrapper {
        width: 100%;
        overflow: hidden;
        mask-image: linear-gradient(to right, transparent 0, #000 6%, #000 94%, transparent 100%);

        .gallery-track {
          display: flex;
          align-items: flex-start;
          gap: 16px;
          width: max-content;
          animation: galleryLoop 70s linear infinite;
          will-change: transform;
        }

        .gallery-image {
          width: 280px;
          border-radius: 20px;
          object-fit: cover;
          flex: 0 0 auto;
          content-visibility: auto;
          contain-intrinsic-size: 280px 400px;
          background: rgba(255, 255, 255, 0.06);
        }

        .gallery-image:nth-child(3n + 1) {
          height: 280px;
        }

        .gallery-image:nth-child(3n + 2) {
          height: 360px;
        }

        .gallery-image:nth-child(3n + 3) {
          height: 400px;
        }
      }
    }
  }

  @keyframes galleryLoop {
    from {
      transform: translateX(0);
    }

    to {
      transform: translateX(calc(-50% - 8px));
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
    .gallery-section-title::after {
      animation: none;
    }
  }

  @media (max-width: 1200px) {
    .gallery-section {
      gap: 80px;
      padding: 80px 0 20px;

      .gallery-container {
        gap: 72px;

        .gallery-heading-wrap {
          .gallery-section-subtitle {
            font-size: 40px;
            line-height: 1.2;
          }

          .gallery-desct {
            font-size: 18px;
          }
        }

        .gallery-wrapper .gallery-track {
          animation-duration: 60s;
        }
      }
    }
  }

  @media (max-width: 768px) {
    .gallery-section {
      gap: 56px;
      padding: 64px 0 16px;

      .gallery-container {
        gap: 48px;

        .gallery-heading-wrap {
          gap: 28px;

          .gallery-section-title {
            font-size: 18px;
          }

          .gallery-section-subtitle {
            font-size: 30px;
            line-height: 1.25;
          }

          .gallery-desct {
            font-size: 16px;
          }

          :deep(.btn.primary) {
            width: 100%;
            max-width: 280px;
            justify-content: flex-start;
          }
        }

        .gallery-wrapper {
          .gallery-image {
            width: 220px;
          }

          .gallery-image:nth-child(3n + 1) {
            height: 220px;
          }

          .gallery-image:nth-child(3n + 2) {
            height: 280px;
          }

          .gallery-image:nth-child(3n + 3) {
            height: 320px;
          }

          .gallery-track {
            animation-duration: 52s;
          }
        }
      }
    }
  }

</style>