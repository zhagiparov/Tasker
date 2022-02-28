<template>
  <div>
      <TasksTableMonth />
    </div>
  </div>
</template>

<script>
  export default {
    name: 'Month',
    mounted: function() {
    this.$emit('showMonthView', 'isMonth');
    this.$emit('showClndBttnsEmmit', true);
    }
  }
</script>

<style scoped>

</style>
