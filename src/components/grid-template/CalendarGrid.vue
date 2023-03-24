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
import ItemDetails from "./ItemDetails.vue";

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
        {
          start: new Date("2023-09-03T00:00:00+01:00"),
          end: new Date("2023-09-03T23:59:59+01:00"),
          title: "Turn the calendar",
        },
      ],
      showDetails: false,
      selectedDay: null,
    };
  },

  components: {
    CalendarItem,
    ItemDetails,
  },

  methods: {
    isPreviousMonth(date) {
      return isBefore(date, this.startOfMonth);
    },

    getEvents(date) {
      return this.events.filter((event) => isSameDay(event.start, date));
    },

    isSelected(day, selectedDay) {
      return isSameDay(day, selectedDay);
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
      @click.native="(showDetails = true), (selectedDay = day)"
      :key="day"
      :dayData="day"
      :isPreviousMonth="isPreviousMonth(day)"
      :events="getEvents(day)"
      :isSelectedDay="isSelected(day, selectedDay)"
    />
  </div>
  <ItemDetails
    v-if="showDetails"
    :dayInfo="selectedDay"
    :events="getEvents(selectedDay)"
    @close-details="(showDetails = false), (selectedDay = null)"
  />
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
