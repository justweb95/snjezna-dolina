<script setup>
  import MoneyWavyBlue from '../assets/images/icons/money_wavy_blue.svg';

  const props = defineProps({
    isOpen: {
      type: Boolean,
      default: false
    }
  });

  const emit = defineEmits(['close']);

  const closeModal = () => {
    emit('close');
  };
</script>

<template>
  <Teleport to="body">
    <div v-if="props.isOpen" class="pricing-modal-overlay" @click.self="closeModal">
      <div class="pricing-modal" role="dialog" aria-modal="true" aria-labelledby="pricing-modal-title">
        <div class="pricing-modal-header">
          <div class="pricing-modal-header-main">
            <img :src="MoneyWavyBlue" alt="Money icon" class="pricing-modal-icon" />
            <h3 id="pricing-modal-title" class="pricing-modal-title">Cenovnik</h3>
          </div>
          <button type="button" class="pricing-modal-close" @click="closeModal" aria-label="Zatvori popup">
            <svg width="24" height="24" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
              <path d="M5 19L18.9987 5.00102" stroke="#13202E" stroke-width="1.5"/>
              <path d="M5 19L18.9987 5.00102" stroke="black" stroke-opacity="0.2" stroke-width="1.5"/>
              <path d="M5 19L18.9987 5.00102" stroke="black" stroke-opacity="0.2" stroke-width="1.5"/>
              <path d="M5 19L18.9987 5.00102" stroke="black" stroke-opacity="0.2" stroke-width="1.5"/>
              <path d="M5 19L18.9987 5.00102" stroke="black" stroke-opacity="0.2" stroke-width="1.5"/>
              <path d="M5 5L18.9987 18.999" stroke="#13202E" stroke-width="1.5"/>
              <path d="M5 5L18.9987 18.999" stroke="black" stroke-opacity="0.2" stroke-width="1.5"/>
              <path d="M5 5L18.9987 18.999" stroke="black" stroke-opacity="0.2" stroke-width="1.5"/>
              <path d="M5 5L18.9987 18.999" stroke="black" stroke-opacity="0.2" stroke-width="1.5"/>
              <path d="M5 5L18.9987 18.999" stroke="black" stroke-opacity="0.2" stroke-width="1.5"/>
            </svg>
          </button>
        </div>

        <div class="pricing-modal-content">
          <p class="pricing-modal-subtitle">Cene od 1. decembra do 28. februara:</p>
          <div class="pricing-table" role="table" aria-label="Detaljni cenovnik">
            <div class="pricing-row pricing-row--head" role="row">
              <p role="columnheader">Trajanje</p>
              <p role="columnheader">Cena po nocenju</p>
              <p role="columnheader">Ukupno</p>
            </div>
            <div class="pricing-row" role="row">
              <p>1 nocenje</p>
              <p class="is-blue">120 EUR</p>
              <p>120 EUR</p>
            </div>
            <div class="pricing-row" role="row">
              <p>2 nocenja</p>
              <p class="is-blue">90 EUR</p>
              <p>180 EUR</p>
            </div>
            <div class="pricing-row" role="row">
              <p>3 nocenja</p>
              <p class="is-blue">80 EUR</p>
              <p>240 EUR</p>
            </div>
            <div class="pricing-row" role="row">
              <p>4 - 5 nocenja</p>
              <p class="is-blue">75 EUR</p>
              <p>-</p>
            </div>
            <div class="pricing-row" role="row">
              <p>5 - 9 nocenja</p>
              <p class="is-blue">70 EUR</p>
              <p>-</p>
            </div>
            <div class="pricing-row" role="row">
              <p>Preko 9 nocenja</p>
              <p class="is-blue">60 EUR</p>
              <p>-</p>
            </div>
          </div>
        </div>

        <div class="pricing-modal-actions">
          <button type="button" class="pricing-modal-action pricing-modal-action--close" @click="closeModal">Zatvori</button>
          <button type="button" class="pricing-modal-action pricing-modal-action--call">Pozovi nas</button>
        </div>
      </div>
    </div>
  </Teleport>
</template>

<style scoped>
  .pricing-modal-overlay {
    position: fixed;
    inset: 0;
    z-index: 99;
    display: flex;
    align-items: center;
    justify-content: center;
    padding: 20px;
    background: rgba(19, 32, 46, 0.2);
    backdrop-filter: blur(6px);
  }

  .pricing-modal {
    width: min(544px, 100%);
    max-height: min(92vh, 820px);
    padding: 32px;
    border-radius: 20px;
    background: #FFFFFF;
    display: flex;
    flex-direction: column;
    gap: 32px;
    overflow-y: auto;
  }

  .pricing-modal-header {
    display: flex;
    align-items: center;
    justify-content: space-between;
    gap: 12px;
    padding-bottom: 32px;
    border-bottom: 1px solid #E4E9ED;
  }

  .pricing-modal-header-main {
    display: flex;
    align-items: center;
    gap: 12px;
  }

  .pricing-modal-icon {
    width: 32px;
    height: 32px;
  }

  .pricing-modal-title {
    font-style: normal;
    font-weight: 600;
    font-size: 20px;
    line-height: 24px;
    color: #081B35;
  }

  .pricing-modal-close {
    width: 24px;
    height: 24px;
    border: none;
    border-radius: 40px;
    background: transparent;
    color: #081B35;
    font-size: 14px;
    font-weight: 700;
    display: inline-flex;
    align-items: center;
    justify-content: center;
    cursor: pointer;
  }

  .pricing-modal-content {
    display: flex;
    flex-direction: column;
    gap: 20px;
  }

  .pricing-modal-subtitle {
    font-style: normal;
    font-weight: 700;
    font-size: 20px;
    line-height: 24px;
    color: #081B35;
    text-align: center;
  }

  .pricing-table {
    border: 1px solid #E4E9ED;
    border-radius: 16px;
    overflow: hidden;
    background: #E4E9ED;
    display: flex;
    flex-direction: column;
    gap: 1px;
  }

  .pricing-row {
    display: grid;
    grid-template-columns: 1.3fr 1fr 0.8fr;
    gap: 12px;
    background: #FFFFFF;
    padding: 16px;
  }

  .pricing-row p {
    font-style: normal;
    font-weight: 500;
    font-size: 16px;
    line-height: 24px;
    color: #081B35;
  }

  .pricing-row p:nth-child(2),
  .pricing-row p:nth-child(3) {
    text-align: right;
  }

  .pricing-row--head {
    background: #FAFAFA;
  }

  .pricing-row--head p {
    font-size: 14px;
  }

  .pricing-row .is-blue {
    font-weight: 700;
    color: #2FB6EF;
  }

  .pricing-modal-actions {
    display: flex;
    gap: 16px;
  }

  .pricing-modal-action {
    flex: 1;
    height: 56px;
    border: none;
    border-radius: 100px;
    font-style: normal;
    font-weight: 700;
    font-size: 18px;
    line-height: 24px;
    color: #FFFFFF;
    cursor: pointer;
    transition: all 0.3s ease;  
  }

  .pricing-modal-action--close {
    background: #13202E;
    border: 2px solid #13202E;
    &:hover {
      color: #13202E;
      background: #FFFFFF;
    }
  }

  .pricing-modal-action--call {
    background: #2FB6EF;
    border: 2px solid #2FB6EF;
    &:hover {
      color: #2FB6EF;
      background: #FFFFFF;
    }
  }

  @media (max-width: 768px) {
    .pricing-modal {
      padding: 24px;
      gap: 24px;
    }

    .pricing-modal-header {
      padding-bottom: 20px;
    }

    .pricing-modal-subtitle {
      font-size: 18px;
      line-height: 22px;
    }

    .pricing-modal-actions {
      flex-direction: column;
    }

    .pricing-row {
      grid-template-columns: 1fr;
      gap: 6px;
    }

    .pricing-row p:nth-child(2),
    .pricing-row p:nth-child(3) {
      text-align: left;
    }
  }
</style>
