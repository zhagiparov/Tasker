<template>
  <div>
      <TasksTableWeek />
    </div>
  </div>
</template>

<script>
  export default {
    name: 'Week',
    mounted: function() {
    this.$emit('showWeekView', 'isWeek');
    this.$emit('showClndBttnsEmmit', true);
    }
  }
</script>

<style scoped>

</style>
