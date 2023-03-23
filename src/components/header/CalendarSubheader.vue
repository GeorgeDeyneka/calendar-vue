<script>
import { format, eachDayOfInterval } from "date-fns";

export default {
  data() {
    return {
      monday: new Date(1970, 0, 5),
      sunday: new Date(1970, 0, 11),
    };
  },

  computed: {
    daysOfWeek() {
      return eachDayOfInterval({
        start: this.monday,
        end: this.sunday,
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
  <div class="subheader__week">
    <div v-for="day in daysOfWeek" :key="day" class="subheader__week-day">
      <strong>
        {{ formatDate(day, "E") }}
      </strong>
    </div>
  </div>
</template>

<style lang="scss">
@import "@/assets/mixins.scss";

.subheader {
  &__week {
    display: grid;
    gap: 1px;
    padding: 0 1px;
    grid-template-columns: repeat(7, 1fr);
    background-image: linear-gradient(to right, #5979b3, #c2cbde);
  }

  &__week-day {
    @include flex-center;
    color: #101010;
  }
}
</style>
