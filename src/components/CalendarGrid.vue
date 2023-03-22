<script setup></script>

<template>
  <main class="container">
    <div class="calendar">
      <div class="calendar-header">
        <div class="calendar-header__button">&lt;</div>
        <div class="calendar-header__title">March 2023</div>
        <div class="calendar-header__button">&gt;</div>
      </div>
      <div class="calendar-grid">
        <div class="calendar-day">1</div>
        <div class="calendar-day">2</div>
        <div class="calendar-day">3</div>
        <div class="calendar-day">4</div>
        <div class="calendar-day">5</div>
        <div class="calendar-day">6</div>
        <div class="calendar-day">7</div>
        <div class="calendar-day">8</div>
        <div class="calendar-day">9</div>
        <div class="calendar-day">10</div>
        <div class="calendar-day">11</div>
        <div class="calendar-day">12</div>
        <div class="calendar-day">13</div>
        <div class="calendar-day">14</div>
        <div class="calendar-day">15</div>
        <div class="calendar-day">16</div>
        <div class="calendar-day">17</div>
        <div class="calendar-day">18</div>
        <div class="calendar-day">19</div>
        <div class="calendar-day">20</div>
        <div class="calendar-day">21</div>
        <div class="calendar-day">22</div>
        <div class="calendar-day">23</div>
        <div class="calendar-day">24</div>
        <div class="calendar-day">25</div>
        <div class="calendar-day">26</div>
        <div class="calendar-day">27</div>
        <div class="calendar-day">28</div>
        <div class="calendar-day">29</div>
        <div class="calendar-day">30</div>
        <div class="calendar-day">31</div>
      </div>
    </div>
  </main>
</template>

<style lang="scss" scoped>
.container {
  margin: 0 auto;
  padding: 50px 0;
  min-height: 100vh;
  max-width: 1024px;
  font-family: Arial, sans-serif;
}
.calendar {
  margin: 0 auto;
  width: 600px;
  border: 1px solid #ccc;
  border-radius: 5px;
  overflow: hidden;

  .calendar-header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    background-color: #f0f0f0;
    padding: 10px;
    font-weight: bold;

    .calendar-header__button {
      cursor: pointer;
      font-size: 20px;
    }

    .calendar-header__title {
      text-align: center;
      font-size: 18px;
    }
  }

  .calendar-grid {
    display: grid;
    grid-template-columns: repeat(7, 1fr);
    grid-template-rows: repeat(5, 1fr);
    gap: 1px;
    background-color: #fff;

    .calendar-day {
      display: flex;
      justify-content: center;
      align-items: center;
      font-size: 16px;
      cursor: pointer;
      height: 60px;

      &:hover {
        background-color: #f0f0f0;
      }
    }
  }
}
</style>
