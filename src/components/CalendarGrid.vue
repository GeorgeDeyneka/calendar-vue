<script>
import { subMonths, addMonths, eachDayOfInterval, format } from "date-fns";

export default {
  data() {
    return {
      startOfWeek: new Date(1970, 0, 5),
      endOfWeek: new Date(1970, 0, 11),

      currentMonth: new Date(),

      days: [
        1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20,
        21, 22, 23, 24, 25, 26, 27, 28, 29, 30, 31,
      ],
    };
  },

  computed: {
    daysOfWeek() {
      return eachDayOfInterval({
        start: this.startOfWeek,
        end: this.endOfWeek,
      });
    },
  },

  methods: {
    prevMonth() {
      this.currentMonth = subMonths(this.currentMonth, 1);
    },

    nextMonth() {
      this.currentMonth = addMonths(this.currentMonth, 1);
    },

    formatDate(date, formatStr) {
      return format(date, formatStr);
    },
  },
};
</script>

<template>
  <main class="container">
    <div class="calendar">
      <div class="calendar-header">
        <div class="calendar-header__button" @click="prevMonth">&lt;</div>
        <div class="calendar-header__title">
          {{ formatDate(currentMonth, "MMMM yyyy") }}
        </div>
        <div class="calendar-header__button" @click="nextMonth">&gt;</div>
      </div>
      <div class="calendar-week-wrapper">
        <div v-for="day in daysOfWeek" :key="day" class="calendar-week">
          {{ formatDate(day, "E") }}
        </div>
      </div>
      <div class="calendar-grid">
        <div v-for="day in days" :key="day" class="calendar-day">{{ day }}</div>
      </div>
    </div>
  </main>
</template>

<style lang="scss" scoped>
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
  border: 1px solid #ccc;
  border-radius: 5px;
  overflow: hidden;

  &-week-wrapper {
    display: grid;
    gap: 1px;
    grid-template-columns: repeat(7, 1fr);
  }

  &-week {
    display: flex;
    justify-content: center;
    align-items: center;
  }

  .calendar-header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    background-color: #f0f0f0;
    padding: 10px;
    font-weight: bold;

    .calendar-header__button {
      cursor: pointer;
      font-size: 20px;
    }

    .calendar-header__title {
      text-align: center;
      font-size: 18px;
    }
  }

  .calendar-grid {
    display: grid;
    grid-template-columns: repeat(7, 1fr);
    grid-template-rows: repeat(5, 1fr);
    gap: 1px;
    background-color: #fff;

    .calendar-day {
      display: flex;
      justify-content: center;
      align-items: center;
      font-size: 16px;
      cursor: pointer;
      height: 60px;

      &:hover {
        background-color: #f0f0f0;
      }
    }
  }
}
</style>
