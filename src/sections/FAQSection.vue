<script setup>
  import { ref } from 'vue';

  // Image imports
  import FAQ_1 from '../assets/images/faq/faq_1.webp';
  import FAQ_2 from '../assets/images/faq/faq_2.webp';
  import FAQ_3 from '../assets/images/faq/faq_3.webp';
  import FAQ_4 from '../assets/images/faq/faq_4.webp';
  import FAQ_5 from '../assets/images/faq/faq_5.webp';

  // Component imports
  import ButtonAction from '../components/ButtonAction.vue';

  const faqs = [
    {
      title: 'Kako doći do nas?',
      image: FAQ_1,
      content:
        'Snježna Dolina se nalazi u naselju Obućina bare na Jahorini. Put je potpuno asfaltiran i redovno se održava tokom zime, a tačnu lokaciju i uputstva za navigaciju šaljemo vam odmah nakon rezervacije.',
    },
    {
      title: 'Kako funkcionišu prijava i odjava?',
      image: FAQ_2,
      content:
        'Prijava je od 15:00, a odjava do 10:00. Ako vam treba raniji dolazak ili kasniji odlazak, javite nam unaprijed pa ćemo provjeriti dostupnost.',
    },
    {
      title: 'Da li je parking obezbjeđen?',
      image: FAQ_3,
      content:
        'Da, parking je obezbijeđen za goste apartmana. Dodatne informacije o pristupu i rasporedu parking mjesta dobijate prije dolaska.',
    },
    {
      title: 'Da li su dozvoljeni kućni ljubimci?',
      image: FAQ_4,
      content:
        'Iako volimo životinje, radi održavanja visokih higijenskih standarda i komfora svih naših gostiju, boravak kućnih ljubimaca u apartmanima trenutno nije dozvoljen.',
    },
    {
      title: 'Koliko je apartman udaljen od ski staze?',
      image: FAQ_5,
      content:
        'Apartmani su na kratkoj udaljenosti od ski staza, pa se do njih stiže za nekoliko minuta vožnje. Tačnu lokaciju i najbolju rutu dijelimo odmah nakon rezervacije.',
    },
  ];

  const activeFaqIndex = ref(0);

  const toggleFaq = (index) => {
    activeFaqIndex.value = activeFaqIndex.value === index ? -1 : index;
  };
</script>

<template>
  <section class="faq-section">
    <div class="doli-container faq-container">
      <div class="faq-section-heading">
        <div class="faq-kicker">
          <span class="faq-kicker-dot"></span>
          <span>FAQ</span>
        </div>
        <h2 class="faq-title">Sve što treba da znate o našim apartmanima</h2>
        <ButtonAction
          type="primary"
          text="Rezerviši odmah"
          action="#apartmans"
        />
      </div>

      <div class="faq-list-holder">
        <ul class="faq-list">
          <li
            v-for="(faq, index) in faqs"
            :key="faq.title"
            class="faq-item"
            :class="{ 'is-open': activeFaqIndex === index }"
          >
            <button
              class="faq-item-title"
              type="button"
              :aria-expanded="activeFaqIndex === index"
              :aria-controls="`faq-content-${index}`"
              @click="toggleFaq(index)"
            >
              <img class="faq-item-title-img" :src="faq.image" :alt="faq.title">
              <span class="faq-item-title-text">{{ faq.title }}</span>
              <svg class="faq-item-title-icon" viewBox="0 0 80 80" fill="none" xmlns="http://www.w3.org/2000/svg" aria-hidden="true">
                <path d="M39.2929 48.7071C39.6834 49.0976 40.3166 49.0976 40.7071 48.7071L47.0711 42.3431C47.4616 41.9526 47.4616 41.3195 47.0711 40.9289C46.6805 40.5384 46.0474 40.5384 45.6569 40.9289L40 46.5858L34.3431 40.9289C33.9526 40.5384 33.3195 40.5384 32.9289 40.9289C32.5384 41.3195 32.5384 41.9526 32.9289 42.3431L39.2929 48.7071ZM40 32L39 32L39 48L40 48L41 48L41 32L40 32Z" fill="currentColor"/>
              </svg>
            </button>

            <div
              :id="`faq-content-${index}`"
              class="faq-item-content"
            >
              <div class="faq-item-content-inner">
                <p>{{ faq.content }}</p>
              </div>
            </div>
          </li>
        </ul>
      </div>
    </div>
  </section>
</template>

<style scoped>
  .faq-section {
    padding: 100px 0;
    background: #FAFAFA;

    .faq-container {
      display: flex;
      justify-content: center;
      align-items: flex-start;
      gap: 56px;
      width: 95%;
      max-width: 1560px;
      margin: 0 auto;

      .faq-section-heading {
        width: min(100%, 752px);
        display: flex;
        flex-direction: column;
        align-items: flex-start;
        gap: 12px;

        .faq-kicker {
          display: flex;
          align-items: center;
          gap: 12px;
          font-family: 'Plus Jakarta Sans';
          font-size: 18px;
          font-weight: 400;
          line-height: 1.4;
          color: #13202E;
        }

        .faq-kicker-dot {
          width: 8px;
          height: 8px;
          border-radius: 50%;
          background: #13202E;
          flex: none;
        }

        .faq-title {
          max-width: 498px;
          margin: 0;
          font-family: 'Plus Jakarta Sans';
          font-style: normal;
          font-weight: 600;
          font-size: 56px;
          line-height: 130%;
          color: #13202E;
        }
        .btn {
          margin: 40px auto 0 0;
        }
      }

      .faq-list-holder {
        width: min(100%, 752px);

        .faq-list {
          display: flex;
          flex-direction: column;
          gap: 16px;
          list-style: none;

          .faq-item {
            overflow: hidden;
            background: #F3F3F3;
            border: 1px solid #E4E9ED;
            border-radius: 54px;
            transition:
              background-color .35s ease,
              border-color .35s ease,
              border-radius .35s ease,
              box-shadow .35s ease;

            &.is-open {
              background: #F3F3F3;
              border-color: transparent;
              border-radius: 54px;
            }

            .faq-item-title {
              appearance: none;
              border: 1px solid transparent;
              background: #FFFFFF;
              width: 100%;
              min-height: 104px;
              display: flex;
              align-items: center;
              gap: 32px;
              padding: 12px;
              border-radius: 54px;
              cursor: pointer;
              text-align: left;
            }

            &.is-open .faq-item-title {
              border-color: #E4E9ED;
            }

            .faq-item-title-img {
              width: 80px;
              height: 80px;
              border-radius: 50%;
              object-fit: cover;
              flex: none;
            }

            .faq-item-title-text {
              flex: 1;
              min-width: 0;
              font-family: 'Plus Jakarta Sans';
              font-style: normal;
              font-weight: 700;
              font-size: 24px;
              line-height: 32px;
              color: #13202E;
            }

            .faq-item-title-icon {
              width: 80px;
              height: 80px;
              flex: none;
              display: grid;
              place-items: center;
              background: #FFFFFF;
              color: #13202E;
              border-radius: 50%;
              transition:
                background-color .35s ease,
                transform .35s ease,
                color .35s ease,
                background-color .35s ease;

              path {
                fill: currentColor;
              }
            }

            &.is-open .faq-item-title-icon {
              color: #2FB6EF;
              transform: rotate(180deg);
            }

            .faq-item-content {
              display: grid;
              grid-template-rows: 0fr;
              opacity: 0;
              margin-top: 0;
              padding: 0 32px 0 40px;
              transition:
                grid-template-rows .38s ease,
                opacity .24s ease,
                margin-top .38s ease,
                padding-bottom .38s ease;
            }

            .faq-item-content-inner {
              overflow: hidden;
            }

            .faq-item-content p {
              margin: 0;
              padding: 32px 0 40px;
              font-family: 'Plus Jakarta Sans';
              font-size: 20px;
              line-height: 140%;
              color: #13202E;
            }

            &.is-open .faq-item-content {
              grid-template-rows: 1fr;
              opacity: 1;
              margin-top: 0;
              padding-bottom: 0;
            }
          }
        }
      }
    }
  }

  @media (max-width: 1200px) {
    .faq-section {
      padding: 72px 0;

      .faq-container {
        flex-direction: column;

        .faq-section-heading,
        .faq-list-holder {
          width: 100%;
          max-width: 752px;
        }

        .faq-section-heading .faq-title {
          font-size: 44px;
        }
      }
    }
  }

  @media (max-width: 768px) {
    .faq-section {
      padding: 56px 0;

      .faq-container {
        gap: 32px;

        .faq-section-heading {
          .faq-title {
            font-size: 34px;
          }
        }

        .faq-list-holder .faq-list .faq-item {
          .faq-item-title {
            min-height: 88px;
          }

          .faq-item-title-img,
          .faq-item-title-icon {
            width: 64px;
            height: 64px;
          }

          .faq-item-title-text {
            font-size: 18px;
            line-height: 1.25;
          }

          .faq-item-content {
            padding: 0 20px;
          }

          .faq-item-content p {
            padding-bottom: 24px;
            font-size: 16px;
          }
        }
      }
    }
  }
</style>