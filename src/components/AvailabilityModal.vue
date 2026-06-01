<script setup>
  import CalendarIconBlue from '../assets/images/icons/calendar_check_blue.svg';

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
    <div v-if="props.isOpen" class="availability-modal-overlay" @click.self="closeModal">
      <div class="availability-modal" role="dialog" aria-modal="true" aria-labelledby="availability-modal-title">
        <div class="availability-modal-header">
          <div class="availability-modal-header-main">
            <img :src="CalendarIconBlue" alt="Calendar icon" class="availability-modal-icon" />
            <h3 id="availability-modal-title" class="availability-modal-title">Dostupnost</h3>
          </div>
          <button type="button" class="availability-modal-close" @click="closeModal" aria-label="Zatvori popup">
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

        <div class="availability-modal-content">
          <div class="availability-calendar-placeholder" aria-label="Kalendar uskoro">
            <div class="availability-calendar-top">
              <button type="button" class="availability-calendar-nav" aria-label="Prethodni mesec">
                <svg width="24" height="24" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
                  <path d="M16 20L8 12L16 4" stroke="#0D1F4C" stroke-width="2"/>
                </svg>
              </button>
              <p class="availability-calendar-month">Septembar 2026</p>
              <button type="button" class="availability-calendar-nav" aria-label="Sledeci mesec">
                <svg width="24" height="24" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
                  <path d="M8 20L16 12L8 4" stroke="#0D1F4C" stroke-width="2"/>
                </svg>
              </button>
            </div>
            <div class="availability-calendar-grid availability-calendar-grid--days">
              <span>PON</span>
              <span>UTO</span>
              <span>SRE</span>
              <span>CET</span>
              <span>PET</span>
              <span>SUB</span>
              <span>NED</span>
            </div>
            <div class="availability-calendar-grid availability-calendar-grid--dates">
              <span class="is-muted">1</span>
              <span class="is-muted">2</span>
              <span class="is-booked">3</span>
              <span class="is-booked">4</span>
              <span class="is-booked">5</span>
              <span class="is-available">6</span>
              <span class="is-available">7</span>
              <span class="is-available">8</span>
              <span class="is-available">9</span>
              <span class="is-available">10</span>
              <span class="is-available">11</span>
              <span class="is-available">12</span>
              <span class="is-available">13</span>
              <span class="is-available">14</span>
              <span class="is-available">15</span>
              <span class="is-available">16</span>
              <span class="is-available">17</span>
              <span class="is-available">18</span>
              <span class="is-available">19</span>
              <span class="is-available">20</span>
              <span class="is-available">21</span>
              <span class="is-available">22</span>
              <span class="is-available">23</span>
              <span class="is-available">24</span>
              <span class="is-available">25</span>
              <span class="is-available">26</span>
              <span class="is-available">27</span>
              <span class="is-available">28</span>
              <span class="is-available">29</span>
              <span class="is-available">30</span>
            </div>
          </div>
        </div>

        <div class="availability-modal-actions">
          <button type="button" class="availability-modal-action availability-modal-action--close" @click="closeModal">Zatvori</button>
          <button type="button" class="availability-modal-action availability-modal-action--call">Pozovi nas</button>
        </div>
      </div>
    </div>
  </Teleport>
</template>

<style scoped>
  .availability-modal-overlay {
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

  .availability-modal {
    width: min(532px, 100%);
    max-height: min(92vh, 820px);
    padding: 32px;
    border-radius: 20px;
    background: #FFFFFF;
    display: flex;
    flex-direction: column;
    gap: 40px;
    overflow-y: auto;
  }

  .availability-modal-header {
    display: flex;
    align-items: center;
    justify-content: space-between;
    gap: 12px;
    padding-bottom: 32px;
    border-bottom: 1px solid #E4E9ED;
  }

  .availability-modal-header-main {
    display: flex;
    align-items: center;
    gap: 12px;
  }

  .availability-modal-icon {
    width: 32px;
    height: 32px;
  }

  .availability-modal-title {
    font-style: normal;
    font-weight: 600;
    font-size: 20px;
    line-height: 24px;
    color: #081B35;
  }

  .availability-modal-close {
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

  .availability-modal-content {
    display: flex;
    flex-direction: column;
    gap: 20px;
  }

  .availability-calendar-placeholder {
    border-radius: 16px;
    padding: 20px;
    display: flex;
    flex-direction: column;
    gap: 16px;
  }

  .availability-calendar-top {
    display: flex;
    gap: 20px;
    align-items: center;
    justify-content: center;
  }

  .availability-calendar-nav {
    width: 24px;
    height: 24px;
    border: none;
    background: transparent;
    color: #0D1F4C;
    font-size: 16px;
    cursor: pointer;
  }

  .availability-calendar-month {
    font-style: normal;
    font-weight: 700;
    font-size: 20px;
    line-height: 140%;
    color: #081B35;
  }

  .availability-calendar-grid {
    display: grid;
    grid-template-columns: repeat(7, minmax(0, 1fr));
    gap: 8px;
  }

  .availability-calendar-grid--days span {
    display: inline-flex;
    justify-content: center;
    align-items: center;
    height: 40px;
    font-style: normal;
    font-weight: 400;
    font-size: 16px;
    line-height: 20px;
    color: #081B35;
  }

  .availability-calendar-grid--dates span {
    display: inline-flex;
    justify-content: center;
    align-items: center;
    height: 52px;
    border-radius: 120px;
    font-style: normal;
    font-weight: 600;
    font-size: 18px;
    line-height: 23px;
    color: #62686F;
  }

  .availability-calendar-grid--dates .is-muted {
    opacity: 0.8;
  }

  .availability-calendar-grid--dates .is-booked {
    color: #FF264D;
    background: rgba(255, 38, 77, 0.08);
  }

  .availability-calendar-grid--dates .is-available {
    color: #34D572;
    background: rgba(52, 213, 114, 0.12);
  }

  .availability-modal-actions {
    display: flex;
    gap: 16px;
    padding-top: 32px;
    border-top: 1px solid #E4E9ED;
  }

  .availability-modal-action {
    flex: 1;
    height: 54px;
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

  .availability-modal-action--close {
    background: #13202E;
    border: 2px solid #13202E;
    &:hover {
      color: #13202E;
      background: #FFFFFF;
    }
  }

  .availability-modal-action--call {
    background: #2FB6EF;
    border: 2px solid #2FB6EF;
    &:hover {
      color: #2FB6EF;
      background: #FFFFFF;
    }
  }

  @media (max-width: 768px) {
    .availability-modal {
      padding: 24px;
      gap: 24px;
    }

    .availability-modal-header {
      padding-bottom: 20px;
    }

    .availability-modal-actions {
      flex-direction: column;
      padding-top: 20px;
    }
  }
</style>
