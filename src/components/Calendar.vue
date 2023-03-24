<script>
import CalendarHeader from "./header/CalendarHeader.vue";
import CalendarSubheader from "./header/CalendarSubheader.vue";
import CalendarGrid from "./grid-template/CalendarGrid.vue";

export default {
  components: { CalendarHeader, CalendarSubheader, CalendarGrid },
  data() {
    return {
      currentMonth: new Date(),
    };
  },
};
</script>

<template>
  <main class="container">
    <div class="calendar">
      <CalendarHeader
        :currentMonth="currentMonth"
        @update:currentMonth="currentMonth = $event"
      />

      <CalendarSubheader />

      <CalendarGrid :currentMonth="currentMonth" />
    </div>
  </main>
</template>

<style lang="scss" scoped>
.container {
  margin: 0 auto;
  padding: 20px 3px;
  min-height: 100vh;
  max-width: 1024px;
  font-family: Arial, sans-serif;
}

.calendar {
  margin: 0 auto;
  max-width: 600px;
  border: 1px solid #303030;
  border-radius: 5px;
  overflow: hidden;
}

@media (min-width: 768px) {
  .container {
    padding: 50px 0;
  }
}
</style>
