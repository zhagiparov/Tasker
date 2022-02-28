<template>

  <div>
    <Header :isPage="isProjects" />
    <div class="wrapper">
      <h2>Projects</h2>
    </div>
    <ProjectGroups />
  </div>

</template>

<script>

  export default {
    name: 'Projects',
    data() {
      return {
        isProjects: 'isProjectsPage'
      }
    }
  }

</script>

<style scoped>

  h2 {
    margin: 1em 0;
    padding: 0;
  }

</style>
