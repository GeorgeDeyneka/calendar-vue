<script>
import {
  startOfMonth,
  endOfMonth,
  subWeeks,
  subMonths,
  addMonths,
  eachDayOfInterval,
  format,
} from "date-fns";
import IconArrowLeft from "./icons/IconArrowLeft.vue";
import IconArrowRight from "./icons/IconArrowRight.vue";

export default {
  components: { IconArrowLeft, IconArrowRight },
  data() {
    return {
      monday: new Date(1970, 0, 5),
      sunday: new Date(1970, 0, 11),
      currentMonth: new Date(),
    };
  },

  computed: {
    daysOfWeek() {
      return eachDayOfInterval({
        start: this.monday,
        end: this.sunday,
      });
    },

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
        <div class="calendar-header__months">
          {{ formatDate(currentMonth, "MMMM yyyy") }}
        </div>

        <div class="calendar-header__buttons">
          <div class="calendar-header__button" @click="prevMonth">
            <icon-arrow-left />
          </div>
          <div class="calendar-header__button" @click="nextMonth">
            <icon-arrow-right />
          </div>
        </div>
      </div>
      <div class="calendar-subheader__week">
        <div
          v-for="day in daysOfWeek"
          :key="day"
          class="calendar-subheader__week-day"
        >
          <strong>
            {{ formatDate(day, "E") }}
          </strong>
        </div>
      </div>

      <div class="calendar-grid">
        <div
          v-for="day in countDaysInMonth"
          :key="day"
          class="calendar-grid__day"
        >
          {{ formatDate(day, 'd') }}
        </div>
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
  border: 1px solid #303030;
  border-radius: 5px;
  overflow: hidden;

  &-header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 10px 20px;
    background-color: #2d2e34;
    color: #b6b6b6;
    font-weight: bold;

    &__buttons {
      display: flex;
      gap: 20px;
    }

    &__button {
      display: flex;
      align-items: center;
      justify-content: center;
      cursor: pointer;
    }

    &__months {
      text-align: center;
      font-size: 18px;
    }
  }

  &-subheader {
    &__week {
      display: grid;
      gap: 1px;
      padding: 0 5px;
      grid-template-columns: repeat(7, 1fr);
      background-image: linear-gradient(to right, #5979b3, #c2cbde);
    }

    &__week-day {
      display: flex;
      justify-content: center;
      align-items: center;
      color: #101010;
    }
  }

  &-grid {
    display: grid;
    grid-template-columns: repeat(7, 1fr);
    grid-template-rows: repeat(5, 1fr);
    gap: 1px;
    background-color: #1a1b22;
    padding: 1px;

    &__day {
      display: flex;
      justify-content: center;
      align-items: center;
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
