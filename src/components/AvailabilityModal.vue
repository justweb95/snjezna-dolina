<script setup>
import { ref, computed, onMounted } from 'vue';
import CalendarIconBlue from '../assets/images/icons/calendar_check_blue.svg';

const props = defineProps({
  isOpen: {
    type: Boolean,
    default: false
  },
  apartmentId: {
    type: Number,
    required: true
  }
});

const emit = defineEmits(['close']);

/* =========================
   ENV CONFIG
========================= */
const API_KEY = import.meta.env.VITE_GOOGLE_API_KEY;

/* =========================
   STATE
========================= */
const bookedRanges = ref([]);
const bookedDates = ref(new Set());
const loading = ref(false);
const currentDate = ref(new Date());

/* =========================
   DATE HELPERS (IMPORTANT FIX)
========================= */
const toDateString = (date) => {
  const year = date.getFullYear();
  const month = String(date.getMonth() + 1).padStart(2, '0');
  const day = String(date.getDate()).padStart(2, '0');

  return `${year}-${month}-${day}`;
};

/* =========================
   MONTH LABEL
========================= */
const MONTHS = [
  'Januar', 'Februar', 'Mart', 'April', 'Maj', 'Jun',
  'Jul', 'Avgust', 'Septembar', 'Oktobar', 'Novembar', 'Decembar'
];

const monthLabel = computed(() => {
  const d = currentDate.value;
  return `${MONTHS[d.getMonth()]} ${d.getFullYear()}`;
});

/* =========================
   NAVIGATION
========================= */
const prevMonth = () => {
  console.log("⬅️ Prev month");

  const d = new Date(currentDate.value);
  d.setMonth(d.getMonth() - 1);
  currentDate.value = d;

  console.log("📅 New month:", d);
};

const nextMonth = () => {
  console.log("➡️ Next month");

  const d = new Date(currentDate.value);
  d.setMonth(d.getMonth() + 1);
  currentDate.value = d;

  console.log("📅 New month:", d);
};

/* =========================
   FETCH GOOGLE CALENDAR
========================= */
const fetchCalendarEvents = async () => {
  try {
    loading.value = true;

    const timeMin = new Date();
    timeMin.setFullYear(timeMin.getFullYear() - 1);

    const timeMax = new Date();
    timeMax.setFullYear(timeMax.getFullYear() + 2);

    const params = new URLSearchParams({
      key: API_KEY,
      timeMin: timeMin.toISOString(),
      timeMax: timeMax.toISOString(),
      singleEvents: 'true',
      orderBy: 'startTime'
    });

    const url = `https://www.googleapis.com/calendar/v3/calendars/${encodeURIComponent(calendarId.value)}/events?${params}`;

    const res = await fetch(url);
    const data = await res.json();

    console.log("📥 API response:", data);
    console.log("📋 Items:", data.items);

bookedRanges.value = (data.items || [])
  .filter(ev => ev.start?.date && ev.summary === 'Rezervisano')
  .map(ev => ({
    start: ev.start.date,
    end: ev.end.date,
    title: ev.summary
  }));

    buildBookedDates();

  } catch (err) {
    console.error("❌ API error:", err);
  } finally {
    loading.value = false;
  }
};

const CALENDAR_IDS = {
  1: import.meta.env.VITE_CALENDAR_ID_1,
  2: import.meta.env.VITE_CALENDAR_ID_2,
};


const calendarId = computed(() => CALENDAR_IDS[props.apartmentId]);


/* =========================
   BUILD BOOKED DAYS
========================= */
const buildBookedDates = () => {
  const set = new Set();

  console.log("🔧 Building booked dates...");

  bookedRanges.value.forEach(r => {
    let start = new Date(r.start);
    let end = new Date(r.end);

    console.log("➡️ Range:", r.start, "→", r.end);

    while (start < end) {
      const dateStr = toDateString(start);
      set.add(dateStr);
      start.setDate(start.getDate() + 1);
    }
  });

  bookedDates.value = set;

  console.log("📆 Final booked dates Set:", bookedDates.value);
};

/* =========================
   PAST DATE CHECK (FIXED)
========================= */
const isPastDate = (dateStr) => {
  const today = new Date();
  today.setHours(0, 0, 0, 0);

  const [y, m, d] = dateStr.split('-');
  const date = new Date(y, m - 1, d);

  return date < today;
};

/* =========================
   CALENDAR GRID
========================= */
const calendarDays = computed(() => {
  const year = currentDate.value.getFullYear();
  const month = currentDate.value.getMonth();

  const lastDay = new Date(year, month + 1, 0);

  const days = [];

  console.log("📅 Building calendar for:", year, month + 1);

  for (let i = 1; i <= lastDay.getDate(); i++) {
    const date = new Date(year, month, i);

    const dateStr = toDateString(date);

    const isBooked = bookedDates.value.has(dateStr);

    days.push({
      day: i,
      date: dateStr,
      isBooked
    });
  }

  return days;
});

/* =========================
   LIFECYCLE
========================= */
onMounted(() => {
  fetchCalendarEvents();
});

/* =========================
   CLOSE MODAL
========================= */
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
              <button type="button" class="availability-calendar-nav" @click="prevMonth">
                <svg width="24" height="24" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
                  <path d="M16 20L8 12L16 4" stroke="#0D1F4C" stroke-width="2"/>
                </svg>
              </button>
              <p class="availability-calendar-month">{{ monthLabel }}</p>
              <button type="button" class="availability-calendar-nav" @click="nextMonth">
                <svg width="24" height="24" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
                  <path d="M8 20L16 12L8 4" stroke="#0D1F4C" stroke-width="2"/>
                </svg>
              </button>
            </div>
            <div v-if="loading" class="calendar-skeleton">
              <span v-for="n in 30" :key="n" class="skeleton-box"></span>
            </div>
            <div v-else class="availability-calendar-grid availability-calendar-grid--dates">
              <span
                v-for="day in calendarDays"
                :key="day.date"
                :class="{
                  'is-muted': isPastDate(day.date),
                  'is-booked': !isPastDate(day.date) && day.isBooked,
                  'is-available': !isPastDate(day.date) && !day.isBooked
                }"
              >
                {{ day.day }}
              </span>
            </div>
          </div>
        </div>

        <div class="availability-modal-actions">
          <button type="button" class="availability-modal-action availability-modal-action--close" @click="closeModal">Zatvori</button>
          <a type="button" class="availability-modal-action availability-modal-action--call">Pozovi nas</a>
        </div>
      </div>
    </div>
  </Teleport>
</template>

<style scoped>

.calendar-skeleton {
  display: grid;
  grid-template-columns: repeat(7, 1fr);
  gap: 8px;
}

.skeleton-box {
  height: 32px;
  background: #eee;
  border-radius: 6px;
  animation: pulse 1.2s infinite;
}

@keyframes pulse {
  0% { opacity: 0.4; }
  50% { opacity: 1; }
  100% { opacity: 0.4; }
}


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
    padding: 0 20px;
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
    background: #101C2A;
    border: 2px solid #101C2A;
    &:hover {
      color: #101C2A;
      background: #FFFFFF;
    }
  }

  .availability-modal-action--call {
    text-decoration: none;
    text-align: center;
    padding: 12px 0;
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
      .availability-modal-action {
        min-height: 54px;
      }
    }
  }
  @media (max-width: 550px) {
    .availability-calendar-placeholder {
      padding: 0;
    }
    .availability-modal {
      padding: 20px;
    }
    .availability-calendar-grid{
      gap: 4px;
    }
    .availability-calendar-grid--dates span {
      height: 41px;
      width: 41px;
      font-size: 14px;
    }
  }
  
  @media (max-width: 360px) {
    .availability-calendar-grid--dates span {
      height: 38px;
      width: 38px;
    }
  }

</style>
