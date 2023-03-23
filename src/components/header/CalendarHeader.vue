<script>
import { subMonths, addMonths, format } from "date-fns";
import IconArrowLeft from "../icons/IconArrowLeft.vue";
import IconArrowRight from "../icons/IconArrowRight.vue";
import CalendarButton from "./CalendarButton.vue";

export default {
  components: { CalendarButton },

  props: ["currentMonth"],

  data() {
    return {
      IconArrowLeft,
      IconArrowRight,
    };
  },

  methods: {
    prevMonth() {
      const newMonth = subMonths(this.currentMonth, 1);
      this.$emit("update:currentMonth", newMonth);
    },

    nextMonth() {
      const newMonth = addMonths(this.currentMonth, 1);
      this.$emit("update:currentMonth", newMonth);
    },

    formatDate(date, formatStr) {
      return format(date, formatStr);
    },
  },
};
</script>

<template>
  <div class="header">
    <h3 class="header__title">
      {{ formatDate(currentMonth, "MMMM yyyy") }}
    </h3>

    <div class="header__buttons">
      <CalendarButton :innerComponent="IconArrowLeft" @click="prevMonth" />
      <CalendarButton :innerComponent="IconArrowRight" @click="nextMonth" />
    </div>
  </div>
</template>

<style lang="scss" scoped>
@import "@/assets/mixins.scss";

.header {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 10px 20px;
  background-color: #2d2e34;
  color: #b6b6b6;
  font-weight: bold;

  &__buttons {
    display: flex;
    gap: 20px;
  }

  &__button {
    @include flex-center;
    cursor: pointer;
    background-color: transparent;
    border: none;
  }
}
</style>
