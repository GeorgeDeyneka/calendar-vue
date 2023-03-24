<script>
import {
  startOfMonth,
  endOfMonth,
  startOfWeek,
  isBefore,
  eachDayOfInterval,
  isSameDay,
} from "date-fns";
import CalendarItem from "./CalendarItem.vue";

export default {
  props: {
    currentMonth: {
      type: Date,
      required: true,
    },
  },

  data() {
    return {
      events: [
        {
          start: new Date("2023-03-26T14:00:00+02:00"),
          end: new Date("2023-03-26T15:00:00+02:00"),
          title: "Meeting",
        },
      ],
    };
  },

  components: {
    CalendarItem,
  },

  methods: {
    isPreviousMonth(date) {
      return isBefore(date, this.startOfMonth);
    },

    getEvents(date) {
      return this.events.filter((event) => isSameDay(event.start, date));
    },
  },

  computed: {
    startOfMonth() {
      return startOfMonth(this.currentMonth);
    },

    endOfMonth() {
      return endOfMonth(this.currentMonth);
    },

    countDaysInMonth() {
      return eachDayOfInterval({
        start: startOfWeek(this.startOfMonth, { weekStartsOn: 1 }),
        end: this.endOfMonth,
      });
    },
  },
};
</script>

<template>
  <div class="grid-template">
    <CalendarItem
      v-for="day in countDaysInMonth"
      :key="day"
      :dayData="day"
      :isPreviousMonth="isPreviousMonth(day)"
      :events="getEvents(day)"
    />
  </div>
</template>

<style lang="scss" scoped>
.grid-template {
  display: grid;
  grid-template-columns: repeat(7, 1fr);
  grid-template-rows: repeat(6, 1fr);
  gap: 1px;
  background-color: #1a1b22;
  padding: 1px;
}
</style>
