<script>
import {
  startOfMonth,
  endOfMonth,
  subWeeks,
  eachDayOfInterval,
  format,
} from "date-fns";
import CalendarHeader from "./header/CalendarHeader.vue";
import CalendarSubheader from "./header/CalendarSubheader.vue";

export default {
  components: { CalendarHeader, CalendarSubheader },
  data() {
    return {
      currentMonth: new Date(),
    };
  },

  computed: {
    startOfMonth() {
      return startOfMonth(this.currentMonth);
    },

    endOfMonth() {
      return endOfMonth(this.currentMonth);
    },

    monthPrevWeek() {
      return subWeeks(this.startOfMonth, 1);
    },

    countDaysInMonth() {
      return eachDayOfInterval({
        start: this.startOfMonth,
        end: this.endOfMonth,
      });
    },
  },

  methods: {
    formatDate(date, formatStr) {
      return format(date, formatStr);
    },
  },
};
</script>

<template>
  <main class="container">
    <div class="calendar">
      <CalendarHeader
        :currentMonth="currentMonth"
        @update:currentMonth="currentMonth = $event"
      />

      <CalendarSubheader />

      <div class="calendar-grid">
        <div
          v-for="day in countDaysInMonth"
          :key="day"
          class="calendar-grid__day"
        >
          {{ formatDate(day, "d") }}
        </div>
      </div>
    </div>
  </main>
</template>

<style lang="scss" scoped>
@import "@/assets/mixins.scss";
.container {
  margin: 0 auto;
  padding: 50px 0;
  min-height: 100vh;
  max-width: 1024px;
  font-family: Arial, sans-serif;
}

.calendar {
  margin: 0 auto;
  width: 600px;
  border: 1px solid #303030;
  border-radius: 5px;
  overflow: hidden;

  &-grid {
    display: grid;
    grid-template-columns: repeat(7, 1fr);
    grid-template-rows: repeat(5, 1fr);
    gap: 1px;
    background-color: #1a1b22;
    padding: 1px;

    &__day {
      @include flex-center;
      font-size: 16px;
      cursor: pointer;
      height: 60px;
      background-color: #2d2e34;
      border-radius: 4px;
      color: #d1d1d1;

      &:hover {
        background-color: #494d52;
      }
    }
  }
}
</style>
