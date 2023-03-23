<template>
  <svg class="arrow">
    <use href="../../assets/sprite.svg#icon-arrow-left"></use>
  </svg>
</template>

<style lang="scss" scoped>
@import "../../assets/mixins.scss";
.arrow {
  @include flex-center;
  width: 20px;
  height: 20px;
  stroke: #b6b6b6;
}
</style>
