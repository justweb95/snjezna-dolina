<script setup>
import { computed, onBeforeUnmount, onMounted, ref } from 'vue'

const props = defineProps({
  aptGallery: {
    type: Array,
    required: true,
    default: () => []
  }
})

const activeIndex = ref(0)
const isLightboxOpen = ref(false)

let revealObserver = null

const activeImage = computed(() => props.aptGallery[activeIndex.value] ?? null)
const hasMultipleImages = computed(() => props.aptGallery.length > 1)

const goToSlide = (index) => {
  if (!props.aptGallery.length) {
    return
  }

  const total = props.aptGallery.length
  activeIndex.value = (index + total) % total
}

const showPrevious = () => {
  goToSlide(activeIndex.value - 1)
}

const showNext = () => {
  goToSlide(activeIndex.value + 1)
}

const openLightbox = () => {
  if (!activeImage.value) {
    return
  }

  isLightboxOpen.value = true
  document.body.style.overflow = 'hidden'
}

const closeLightbox = () => {
  isLightboxOpen.value = false
  document.body.style.overflow = ''
}

const handleKeydown = (event) => {
  if (!isLightboxOpen.value) {
    return
  }

  if (event.key === 'Escape') {
    closeLightbox()
  }

  if (event.key === 'ArrowLeft') {
    showPrevious()
  }

  if (event.key === 'ArrowRight') {
    showNext()
  }
}

onMounted(() => {
  window.addEventListener('keydown', handleKeydown)

  revealObserver = new IntersectionObserver((entries) => {
    entries.forEach((entry) => {
      if (entry.isIntersecting) {
        entry.target.classList.add('revealed')
        revealObserver.unobserve(entry.target)
      }
    })
  }, {
    threshold: 0.25
  })

  document
    .querySelectorAll('.apts-section .single-apt > :first-child')
    .forEach((el) => revealObserver.observe(el))
})

onBeforeUnmount(() => {
  window.removeEventListener('keydown', handleKeydown)

  if (revealObserver) {
    revealObserver.disconnect()
  }

  document.body.style.overflow = ''
})
</script>

<template>
  <section class="apts-gallery">
    <button
      v-if="hasMultipleImages"
      type="button"
      class="gallery-arrow gallery-arrow--previous"
      aria-label="Prethodna slika"
      @click.stop="showPrevious"
    >
      <svg viewBox="0 0 48 48" fill="none" xmlns="http://www.w3.org/2000/svg" aria-hidden="true">
        <rect width="48" height="48" rx="24" fill="currentColor" fill-opacity="0.18"/>
        <path d="M27.5359 31.071L20.4648 24L27.5359 16.9289" stroke="white" stroke-width="2.4"/>
      </svg>
    </button>

    <button
      v-if="activeImage"
      type="button"
      class="gallery-viewport"
      :aria-label="`Otvori galeriju za sliku ${activeIndex + 1}`"
      @click="openLightbox"
    >
      <span class="gallery-viewport__overlay">
      <span name="gallery-counter" :key="activeIndex" class="gallery-counter">{{ activeIndex + 1 }} / {{ aptGallery.length }}</span>
      </span>
        <img name="gallery-fade"
          :key="activeImage.src"
          :src="activeImage.src"
          :alt="activeImage.alt"
          class="gallery-image"
        />
    </button>

    <button
      v-if="hasMultipleImages"
      type="button"
      class="gallery-arrow gallery-arrow--next"
      aria-label="Sljedeća slika"
      @click.stop="showNext"
    >
      <svg viewBox="0 0 48 48" fill="none" xmlns="http://www.w3.org/2000/svg" aria-hidden="true">
        <rect width="48" height="48" rx="24" fill="currentColor" fill-opacity="0.18"/>
        <path d="M20.4641 31.071L27.5352 24L20.4641 16.9289" stroke="white" stroke-width="2.4"/>
      </svg>
    </button>

    <div v-if="hasMultipleImages" class="gallery-dots" aria-label="Navigacija galerije">
      <button
        v-for="(image, index) in aptGallery"
        :key="image.src"
        type="button"
        class="gallery-dot"
        :class="{ 'is-active': index === activeIndex }"
        :aria-label="`Prikaži sliku ${index + 1}`"
        @click="goToSlide(index)"
      />
    </div>
  </section>

  <Teleport to="body">
    <div
      v-if="isLightboxOpen && activeImage"
      class="gallery-lightbox"
      role="dialog"
      aria-modal="true"
      :aria-label="activeImage.alt"
      @click.self="closeLightbox"
    >
      <button
        type="button"
        class="gallery-lightbox__close"
        aria-label="Zatvori galeriju"
        @click="closeLightbox"
      >
        ×
      </button>

      <button
        v-if="hasMultipleImages"
        type="button"
        class="gallery-arrow gallery-arrow--lightbox gallery-arrow--previous"
        aria-label="Prethodna slika"
        @click.stop="showPrevious"
      >
        <svg viewBox="0 0 48 48" fill="none" xmlns="http://www.w3.org/2000/svg" aria-hidden="true">
          <rect width="48" height="48" rx="24" fill="currentColor" fill-opacity="0.18"/>
          <path d="M27.5359 31.071L20.4648 24L27.5359 16.9289" stroke="white" stroke-width="2.4"/>
        </svg>
      </button>

      <figure class="gallery-lightbox__content">
          <img name="gallery-fade"
            :key="activeImage.src"
            :src="activeImage.src"
            :alt="activeImage.alt"
            class="gallery-lightbox__image"
          />
      </figure>

      <button
        v-if="hasMultipleImages"
        type="button"
        class="gallery-arrow gallery-arrow--lightbox gallery-arrow--next"
        aria-label="Sljedeća slika"
        @click.stop="showNext"
      >
        <svg viewBox="0 0 48 48" fill="none" xmlns="http://www.w3.org/2000/svg" aria-hidden="true">
          <rect width="48" height="48" rx="24" fill="currentColor" fill-opacity="0.18"/>
          <path d="M20.4641 31.071L27.5352 24L20.4641 16.9289" stroke="white" stroke-width="2.4"/>
        </svg>
      </button>
    </div>
  </Teleport>
</template>

<style scoped>
  .apts-gallery {
    flex: 1 0 45%;
    position: relative;
    width: 100%;
    max-width: 768px;
    height: 600px;
    border-radius: 1.25rem;
    background: #d7e0ea;
    overflow: hidden;

    .gallery-viewport {
      border: none;
      width: 100%;
      height: 100%;
      padding: 0;

      .gallery-viewport__overlay {
        position: absolute;
        right: 32px;
        bottom: 32px;
        z-index: 2;
        display: inline-flex;
        align-items: center;
        padding: 4px 8px;
        border-radius: 999px;
        background: rgba(8, 27, 53, 0.55);
        backdrop-filter: blur(20px);

        .gallery-counter {
          color: #fff;
          font-size: 12px;
          font-weight: 400;
        }
      }

      .gallery-image {
        display: block;
        width: 100%;
        height: 100%;
        object-fit: cover;
      }
    }

    .gallery-arrow {
      position: absolute;
      top: 50%;
      z-index: 2;
      width: 48px;
      height: 48px;
      border: none;
      border-radius: 50%;
      transform: translateY(-50%);
      transition: background 0.2s ease;
      background: rgba(8, 27, 53, 0.6);

      &:hover {
        cursor: pointer;
        background: rgba(8, 27, 53, 0.8);
      }

      svg {
        width: 100%;
        height: 100%;
      }


      &.gallery-arrow--previous {
        left: 32px;
      }

      &.gallery-arrow--next {
        right: 32px;
      }
      
    }

    .gallery-dots {
      position: absolute;
      left: 50%;
      bottom: 1.5rem;
      z-index: 1;
      display: flex;
      gap: 0.625rem;
      transform: translateX(-50%);

      .gallery-dot {
        width: 0.75rem;
        height: 0.75rem;
        padding: 0;
        border: 0;
        border-radius: 50%;
        background: rgba(255, 255, 255, 0.45);
        cursor: pointer;
        transition: transform 0.2s ease, background-color 0.2s ease;

        &.is-active {
          background: #fff;
          transform: scale(1.15);
        }
      }
    }
  }

  .gallery-lightbox {
    position: fixed;
    inset: 0;
    z-index: 1000;
    display: flex;
    align-items: center;
    justify-content: center;
    padding: 2rem;
    background: rgba(4, 12, 24, 0.9);

    .gallery-lightbox__content {
      display: flex;
      align-items: center;
      justify-content: center;
      width: min(100%, 90rem);
      height: min(100%, 90vh);
      margin: 0;

      .gallery-lightbox__image {
        display: block;
        max-width: 100%;
        max-height: 90vh;
        border-radius: 1rem;
        object-fit: contain;
        box-shadow: 0 1.25rem 4rem rgba(0, 0, 0, 0.35);
        will-change: transform, opacity;
      }
    }

    .gallery-lightbox__close {
      position: absolute;
      top: 1.25rem;
      right: 1.25rem;
      z-index: 1001;
      width: 3rem;
      height: 3rem;
      border: 0;
      border-radius: 50%;
      background: rgba(255, 255, 255, 0.14);
      color: #fff;
      font-size: 2rem;
      line-height: 1;
      cursor: pointer;
    }

    .gallery-arrow {
      position: absolute;
      top: 50%;
      z-index: 1001;
      width: 48px;
      height: 48px;
      border: none;
      border-radius: 50%;
      transform: translateY(-50%);
      transition: background 0.2s ease;
      background: rgba(8, 27, 53, 0.6);

      &:hover {
        cursor: pointer;
        background: rgba(8, 27, 53, 0.8);
      }

      svg {
        width: 100%;
        height: 100%;
      }

      &.gallery-arrow--previous {
        left: 2rem;
      }

      &.gallery-arrow--next {
        right: 2rem;
      }
    }
  }

  .gallery-fade-enter-active,
  .gallery-fade-leave-active,
  .gallery-counter-enter-active,
  .gallery-counter-leave-active {
    transition: opacity 0.18s ease-out, transform 0.22s ease-out;
  }

  .gallery-fade-enter-from,
  .gallery-fade-leave-to {
    opacity: 0;
    transform: scale(1.03);
  }

  .gallery-fade-enter-to,
  .gallery-fade-leave-from {
    opacity: 1;
    transform: scale(1.015);
  }

  .gallery-counter-enter-from,
  .gallery-counter-leave-to {
    opacity: 0;
    transform: translateY(0.2rem);
  }

  .gallery-counter-enter-to,
  .gallery-counter-leave-from {
    opacity: 1;
    transform: translateY(0);
  }
  
  @media (max-width: 1024px) {
    .apts-gallery {
      order: -1;
      max-width: 100%;
      flex: 1 0 100%;
    }
  }

  @media (max-width: 960px) {
    .apts-gallery {
      height: 31.25rem;
      /* padding: 1.5rem; */
    }
  }

  @media (max-width: 550px) {
    .apts-gallery {
      max-width: 100%;
      height: 25rem;
      /* padding: 1rem; */
      gap: 0.75rem;

      .gallery-viewport {
        .gallery-viewport__overlay {
          right: 1rem;
          bottom: 3.25rem;
        }
      }

      .gallery-dots {
        bottom: 1rem;
      }

      .gallery-arrow {
        &.gallery-arrow--lightbox {
          &.gallery-arrow--previous {
            left: 0.75rem;
          }

          &.gallery-arrow--next {
            right: 0.75rem;
          }
        }
      }
    }

    .gallery-lightbox {
      padding: 1rem;

      .gallery-arrow {
        &.gallery-arrow--previous {
          left: 0.75rem;
        }

        &.gallery-arrow--next {
          right: 0.75rem;
        }
      }
    }
  }
</style>