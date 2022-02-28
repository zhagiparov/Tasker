<template>

  <div class="wrapper">

    <div class="header-greeting">
      <div class="display-flex">
        <div>
          <h2 class="greeting">Добро пожаловать, User!</h2>
          <h3 class="current-date"> {{ currentMonthDay }} {{ currentMonth }} {{ currentYear }}, {{ currentWeekDay }} <span class="refresh-arrow">&#10227;</span></h3>
        </div>
        <img src="/astronaut.png" class="astronaut-image" />
      </div>

      <button type="button" name="new-task" class="create-task-button">&#8853; Создать задачу</button>
    </div>

  </div>

</template>

<script>

  export default {
    data() {
      return {
        currentDate: new Date(),
        monthNames: [
          'Января',
          'Февраля',
          'Марта',
          'Апреля',
          'Мая',
          'Июня',
          'Июля',
          'Августа',
          'Сентября',
          'Октября',
          'Ноября',
          'Декабря'
        ],
        weekDayNames: [
          'понедельник',
          'вторник',
          'среда',
          'четверг',
          'пятница',
          'суббота',
          'воскресенье',
        ]
      }
    },
    computed: {
      currentYear() {
        return this.currentDate.getFullYear();
      },
      currentMonth() {
        return this.monthNames[this.currentDate.getMonth()];
      },
      currentMonthDay() {
        return this.currentDate.getDate();
      },
      currentWeekDay() {
        return this.weekDayNames[this.currentDate.getDay()-1];
      }
    }
  }

</script>

<style scoped>

</style>
