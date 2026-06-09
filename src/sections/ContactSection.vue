<script setup>
  import { onMounted, onBeforeUnmount, ref } from 'vue'

  const mapRef = ref(null)
  let mapInstance = null

  onMounted(async () => {
    // Load CSS via link tag instead
    const link = document.createElement('link')
    link.rel = 'stylesheet'
    link.href = 'https://unpkg.com/leaflet@1.9.4/dist/leaflet.css'
    document.head.appendChild(link)

    const { default: L } = await import('https://esm.sh/leaflet@1.9.4')

    // Small wait for CSS to apply
    await new Promise(resolve => setTimeout(resolve, 100))

    mapInstance = L.map(mapRef.value, { zoomControl: false }).setView([43.741866, 18.636831], 11)

    L.tileLayer('https://{s}.basemaps.cartocdn.com/dark_all/{z}/{x}/{y}{r}.png', {
      attribution: '© OpenStreetMap © CARTO',
      maxZoom: 19,
    }).addTo(mapInstance)

    L.marker([43.741866, 18.636831]).addTo(mapInstance)
  })

  onBeforeUnmount(() => {
    mapInstance?.remove()
  })
</script>


<template>
  <section class="contact-section">
    <div class="contact-container doli-container">
      <h2 id="location" class="contact-title">Kontakt & Lokacija</h2>
      <p class="contact-description">Kontaktirajte nas</p>
      <ul class="list-of-contacts">
        <li class="list-item">
          <svg class="list-item-icon" width="48" height="48" viewBox="0 0 48 48" fill="none" xmlns="http://www.w3.org/2000/svg">
            <rect width="48" height="48" rx="24" fill="#1D3044"/>
            <path d="M27.75 25.4131C31.2731 25.9756 33.75 27.3153 33.75 28.8753C33.75 30.9462 29.385 32.6253 24 32.6253C18.615 32.6253 14.25 30.9462 14.25 28.8753C14.25 27.3153 16.7269 25.9775 20.25 25.4131" stroke="#2FB6EF" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>
            <path d="M24 21.375V28.875" stroke="#2FB6EF" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>
            <path d="M24 21.375C25.6569 21.375 27 20.0319 27 18.375C27 16.7181 25.6569 15.375 24 15.375C22.3431 15.375 21 16.7181 21 18.375C21 20.0319 22.3431 21.375 24 21.375Z" stroke="#2FB6EF" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>
          </svg>
          <h4 class="list-item-title">Lokacija</h4>
          <p class="list-item-description">Jahorina bb, 71423 Jahorina</p>
          <div class="list-item-geo-location">Jahorina • BiH</div>
        </li>
        <li class="list-item">
          <svg class="list-item-icon" width="48" height="48" viewBox="0 0 48 48" fill="none" xmlns="http://www.w3.org/2000/svg">
            <rect width="48" height="48" rx="24" fill="#1D3044"/>
            <path d="M14 18L20.913 21.917C23.4616 23.361 24.5384 23.361 27.087 21.917L34 18" stroke="#2FB6EF" stroke-width="2" stroke-linejoin="round"/>
            <path d="M14.0158 25.4756C14.0811 28.5412 14.1138 30.0739 15.245 31.2094C16.3761 32.3448 17.9503 32.3843 21.0988 32.4634C23.0393 32.5122 24.9607 32.5122 26.9012 32.4634C30.0497 32.3843 31.6239 32.3448 32.7551 31.2094C33.8862 30.0739 33.9189 28.5412 33.9842 25.4756C34.0053 24.4899 34.0053 23.5101 33.9842 22.5244C33.9189 19.4589 33.8862 17.9261 32.7551 16.7907C31.6239 15.6552 30.0497 15.6157 26.9012 15.5366C24.9607 15.4878 23.0393 15.4878 21.0988 15.5366C17.9503 15.6157 16.3761 15.6552 15.245 16.7906C14.1138 17.9261 14.0811 19.4588 14.0158 22.5244C13.9947 23.5101 13.9947 24.4899 14.0158 25.4756Z" stroke="#2FB6EF" stroke-width="2" stroke-linejoin="round"/>
          </svg>
          <h4 class="list-item-title">Email</h4>
          <p class="list-item-description">info@snjeznadolina.rs</p>
          <div class="list-item-geo-location">Odgovaramo brzo</div>
        </li>
        <li class="list-item">
          <svg class="list-item-icon" width="48" height="48" viewBox="0 0 48 48" fill="none" xmlns="http://www.w3.org/2000/svg">
            <rect width="48" height="48" rx="24" fill="#1D3044"/>
            <path d="M16.5999 23.9481C15.7466 22.4604 15.3347 21.2455 15.0863 20.0141C14.7189 18.1928 15.5596 16.4137 16.9524 15.2785C17.5411 14.7987 18.2159 14.9627 18.564 15.5872L19.3499 16.997C19.9728 18.1145 20.2842 18.6733 20.2224 19.2656C20.1607 19.858 19.7406 20.3405 18.9006 21.3054L16.5999 23.9481ZM16.5999 23.9481C18.3269 26.9594 21.0371 29.6711 24.0519 31.4001M24.0519 31.4001C25.5396 32.2534 26.7545 32.6653 27.9859 32.9137C29.8072 33.2811 31.5863 32.4404 32.7215 31.0476C33.2013 30.4589 33.0373 29.7841 32.4128 29.436L31.003 28.6501C29.8855 28.0272 29.3267 27.7158 28.7344 27.7776C28.142 27.8393 27.6595 28.2594 26.6946 29.0994L24.0519 31.4001Z" stroke="#2FB6EF" stroke-width="2" stroke-linejoin="round"/>
            <path d="M25.8008 19.3487C27.0817 19.8926 28.1082 20.9191 28.6522 22.2M26.3894 15C29.5729 15.9187 32.082 18.4277 33.0008 21.6111" stroke="#2FB6EF" stroke-width="2" stroke-linecap="round"/>
          </svg>
          <h4 class="list-item-title">Telefon</h4>
          <p class="list-item-description">+381 62 204 003</p>
          <div class="list-item-geo-location">Dostupni 24/7</div>
        </li>
      </ul>
      <div ref="mapRef" id="map" class="map-wrapper"></div>
    </div>


  </section>
</template>

<style scoped>

.contact-section {
  padding: 100px 0 24px;
  background-color: #101C2A;
  .contact-container {
    .contact-title {
      position: relative;
      width: fit-content;
      margin: 0 auto ;
      font-style: normal;
      font-weight: 400;
      font-size: 18px;
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
        animation: titleDotPopGlobal 1.6s cubic-bezier(0.16, 1, 0.3, 1) infinite;
        content: '';
        border-radius: 50%;
        display: block;
        width: 8px;
        height: 8px;
        background-color: #B9C1CA;
      }
    }
    .contact-description {
      font-style: normal;
      font-weight: 600;
      font-size: 48px;
      line-height: 60px;
      text-align: center;
      color: #FFFFFF;
      margin: 16px 0 80px;
    }
    .list-of-contacts {
      width: 100%;
      display: flex;
      gap: 0px;
      justify-content: center;
      margin-bottom: 100px;
      .list-item {
        flex: 1 0 33%;
        padding: 0 24px;
        display: flex;
        flex-direction: column;
        align-items: center;
        text-align: center;
        gap: 12px;
        border-left: 1px solid #1D3044;
        &:last-child {
          border-right: 1px solid #1D3044;
        }
        .list-item-icon {
          margin-bottom: 12px;
        }
        .list-item-title {
          font-style: normal;
          font-weight: 400;
          font-size: 18px;
          line-height: 140%;
          text-align: center;
          color: #B9C1CA;
        }
        .list-item-description {
          font-style: normal;
          font-weight: 600;
          font-size: 20px;
          line-height: 140%;
          text-align: center;
          color: #FFFFFF;
        }
        .list-item-geo-location {
          font-style: normal;
          font-weight: 300;
          font-size: 16px;
          line-height: 140%;
          text-align: center;
          color: #B9C1CA;
        }
      }
    }
  }
  .map-wrapper {
    border: none !important;
    /* border: 3px solid #1D3044; */
    width: 100%;
    height: 600px;
    border-radius: 20px;
    overflow: hidden;
    flex: none;
    order: 1;
    align-self: stretch;
    flex-grow: 0;
    .map {
      width: 100%;
      height: 100%;
    }
    .leaflet-right {
      display: none;
    }
  }

  @media (prefers-reduced-motion: reduce) {
    .contact-title::after {
      animation: none;
    }
  }

  @media (max-width: 768px) {
    padding: 56px 0 16px;
    .contact-container {
      .contact-description {
        font-size: 36px;
        margin: 16px 0 56px;
      }
      .list-of-contacts {
        flex-direction: column;
        margin-bottom: 56px;
        .list-item {
          flex: 1 0 33%;
          padding: 0 24px;
          display: flex;
          flex-direction: column;
          align-items: center;
          text-align: center;
          gap: 12px;
          border-left: none;
          border-bottom: 1px solid #1D3044;
          padding: 32px 0;
          &:last-child {
            border-left: none;
            border-right: none;
            border-bottom: 1px solid #1D3044;
          }
          &:first-child {
            padding-top: 0;
          }
        }
      }
    }
    .map-wrapper {
      height: 400px;
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