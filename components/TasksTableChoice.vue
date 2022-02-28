<template>

  <div class="wrapper">
    <div class="table-settings">
      <div class="display-type">
        <NuxtLink to="/dashboard">
          <button
          @click="showSortingBtns"
          :class="[showCalendarButtons ? 'display-mode-button-off' : 'display-mode-button-on']">
          Задачи
        </button>
        </NuxtLink>
        <NuxtLink to="/dashboard/month">
          <button
          @click="showCalendarBtns"
          :class="[showCalendarButtons ? 'display-mode-button-on' : 'display-mode-button-off']">
          Календарь
        </button>
        </NuxtLink>
        </div>
      <div :class="[showCalendarButtons ? 'unshown' : 'sorting-buttons']">
        <div class="select-wrapper">
          <select name="sort-by" id="sort-by" class="table-settings-select">
                <option value="date">Сортировка по дате &uarr;</option>
                <option value="date">Сортировка по дате &darr;</option>
                <option value="name">Сортировка по алфавиту &uarr;</option>
                <option value="name">Сортировка по алфавиту &darr;</option>
              </select>
        </div>

        <button type="button" class="filter-button">Фильтр</button>
      </div>
      <div :class="[showCalendarButtons ? 'display-type-calendar-buttons' : 'unshown']">
        <NuxtLink to="/dashboard/week">
          <button :class="[showMonthMode === 'isWeek' ? 'calendar-button-on' : 'calendar-button-off']">Неделя</button>
        </NuxtLink>
        <NuxtLink to="/dashboard/month">
          <button :class="[showMonthMode === 'isMonth' ? 'calendar-button-on' : 'calendar-button-off']">Месяц</button>
        </NuxtLink>
        </div>
    </div>

  </div>

</template>

<script>

  export default {
    data() {
      return {
        showCalendarButtons: false,
        showMonthMode: '',
      }
    },
    props: {
      pageType: { type: String },
      buttonsSetup: { type: Boolean }
    },

    watch: {
      pageType: {
        immediate: true,
        deep: true,
        handler() {
          this.showMonthMode = this.pageType
        }
      },
      buttonsSetup: {
        immediate: true,
        deep: true,
        handler() {
          this.showCalendarButtons = this.buttonsSetup
        }
      }
    },

    methods: {
      showSortingBtns() {
        this.showCalendarButtons = false;
        this.$emit('showSortBtns', 'isDashboard');
      },
      showCalendarBtns() {
        this.showCalendarButtons = true;
      },
      showWeekTable() {
        this.showMonthMode = false;
      },
      showMonthTable() {
        this.showMonthMode = true;
      }
    }
  }

</script>

<style scoped>

</style>
