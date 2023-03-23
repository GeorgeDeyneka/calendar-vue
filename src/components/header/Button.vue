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
  <button class="button">
    <component :is="innerComponent" />
  </button>
</template>

<style lang="scss" scoped>
@import "@/assets/mixins.scss";

.button {
  @include flex-center;
  cursor: pointer;
  background-color: transparent;
  border: none;
  min-width: 20px;
  min-height: 30px;
  border-radius: 4px;
  transition: background-color 100ms ease-in-out;

  &:hover {
    background-color: #444444;
  }
}
</style>
