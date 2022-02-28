<template>
<div>
  <Header
    :isPage="isIndex"
  />
  <Greeting />
  <TasksTableChoice
    :pageType="pageType"
    :buttonsSetup="buttonsSetup"
    @showSortBtns="showTaskTable($event)"
  />
  <TasksTable
    :class="[taskTableShown ? '' : 'unshown']"
  />
  <NuxtChild
    :class="[taskTableShown ? 'unshown' : '']"
    @showWeekView="showWeekTable($event)"
    @showMonthView="showMonthTable($event)"
    @showClndBttnsEmmit="passButtonsSetup($event)"
  />
</div>

</template>

<script>

  export default {
    name: 'IndexPage',
    data() {
      return {
        taskTableShown: true,
        buttonsSetup: false,
        isIndex: 'isIndexPage',
        pageType: 'isDashboard',
      }
    },
    methods: {
      showTaskTable(page) {
        this.pageType = page;
        this.taskTableShown = true;
        this.buttonsSetup = false;
      },
      showWeekTable(page) {
        this.pageType = page;
        this.taskTableShown = false;
      },
      showMonthTable(page) {
        this.pageType = page;
        this.taskTableShown = false;
      },
      passButtonsSetup(bool) {
        this.buttonsSetup = bool;
      }
    }
  }

</script>

<style scoped>

</style>
