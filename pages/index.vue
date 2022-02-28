<template>
  <div>

  </div>
</template>

<script>
  export default {
    middleware: [
        function({ redirect }) {
            redirect('/dashboard');
        },
    ],
  }
</script>

<style scoped>

</style>
