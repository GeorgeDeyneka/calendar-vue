<script>
import { format } from "date-fns";

export default {
  props: ["dayData"],

  methods: {
    formatDate(date, formatStr) {
      return format(date, formatStr);
    },
  },
};
</script>

<template>
  <div class="item">
    {{ formatDate(dayData, "d") }}
  </div>
</template>

<style lang="scss" scoped>
@import "@/assets/mixins.scss";

.item {
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
</style>
