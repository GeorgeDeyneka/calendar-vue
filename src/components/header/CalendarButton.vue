<script>
export default {
  props: {
    text: String,
    innerComponent: {
      type: Object,
    },
  },
};
</script>

<template>
  <button class="header__button">
    <component :is="innerComponent" />
  </button>
</template>

<style lang="scss">
@import "@/assets/mixins.scss";

.header {
  &__button {
    @include flex-center;
    cursor: pointer;
    background-color: transparent;
    border: none;
    min-width: 20px;
    min-height: 20px;
  }
}
</style>
