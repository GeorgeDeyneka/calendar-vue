<script>
import { format } from "date-fns";
import { utcToZonedTime } from "date-fns-tz";

export default {
  props: {
    dayInfo: {
      type: Date,
      required: true,
    },
    events: {
      type: Array,
    },
  },

  methods: {
    formatDate(date, formatStr) {
      return format(date, formatStr);
    },

    formatByTimeZone(date, formatStr) {
      const timeZone = "Europe/London";
      const dateInUTC = utcToZonedTime(date, timeZone);

      return format(dateInUTC, formatStr, { timeZone });
    },
  },
};
</script>

<template>
  <div class="details">
    <div class="details__info">
      <h3 class="details__date">{{ formatDate(dayInfo, "PPPP") }}</h3>

      <ul class="details__events" v-if="events.length" v-for="event in events">
        <li class="details__event">
          {{ event.title }}
          from {{ formatByTimeZone(event.start, "HH:mm") }} to
          {{ formatByTimeZone(event.end, "HH:mm") }}
        </li>
      </ul>

      <div class="details__events" v-else>There is no events for this day.</div>
    </div>

    <button class="details__close-btn" @click="$emit('close-details', false)">
      Close
    </button>
  </div>
</template>

<style lang="scss" scoped>
.details {
  display: flex;
  align-items: center;
  background-color: #2d2e34;
  padding: 10px;

  &__info {
    flex-grow: 1;
    color: #d1d1d1;
  }

  &__close-btn {
    padding: 5px 20px;
    border-radius: 4px;
    border: none;
    background-color: #303d4f;
    color: #d1d1d1;
    cursor: pointer;
    box-shadow: 0px 0px 5px 0px #0d0c0c;
    transition: background-color 100ms ease-in;

    &:hover {
      background-color: #435267;
    }
  }
}
</style>
