<template>

  <div>
    <Header :isPage="isTeam" />
    <div class="wrapper">
      <h2>Team</h2>
    </div>
    <TeamMember />
  </div>

</template>

<script>

  export default {
    name: 'Team',
    data() {
      return {
        isTeam: 'isTeamPage',
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
