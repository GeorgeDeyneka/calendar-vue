<script>
import {
  startOfMonth,
  endOfMonth,
  subWeeks,
  eachDayOfInterval,
  format,
} from "date-fns";

export default {
  props: ["currentMonth"],

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
  <div class="grid-template">
    <div v-for="day in countDaysInMonth" :key="day" class="grid-template__day">
      {{ formatDate(day, "d") }}
    </div>
  </div>
</template>

<style lang="scss" scoped>
@import "@/assets/mixins.scss";

.grid-template {
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
</style>
