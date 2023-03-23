<script>
import {
  startOfMonth,
  endOfMonth,
  subWeeks,
  eachDayOfInterval,
} from "date-fns";
import CalendarItem from "./CalendarItem.vue";

export default {
  props: ["currentMonth"],

  components: {
    CalendarItem,
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
};
</script>

<template>
  <div class="grid-template">
    <CalendarItem v-for="day in countDaysInMonth" :key="day" :dayData="day" />
  </div>
</template>

<style lang="scss" scoped>
.grid-template {
  display: grid;
  grid-template-columns: repeat(7, 1fr);
  grid-template-rows: repeat(5, 1fr);
  gap: 1px;
  background-color: #1a1b22;
  padding: 1px;
}
</style>
