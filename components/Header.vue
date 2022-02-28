<template>
<div class="header-userbar-bg">
  <div class="wrapper">
    <div class="header-userbar">
      <input type="text" name="search-bar" class="search-bar" placeholder="Искать задачу..." value="">
      <div class="header-links">
        <NuxtLink to="/dashboard">Дашборд<span
          :class="[isPage === 'isIndexPage' ? 'link-highlighter' : 'opaque-lh']">&#8226;
        </span></NuxtLink>
        <NuxtLink to="/projects">Проекты<span
          :class="[isPage === 'isProjectsPage' ? 'link-highlighter' : 'opaque-lh']">&#8226;
        </span></NuxtLink>
        <NuxtLink to="/team">Команда<span
          :class="[isPage === 'isTeamPage' ? 'link-highlighter' : 'opaque-lh']">&#8226;
        </span></NuxtLink>
      </div>
      <img src="/alert-bell-placeholder-al.png" class="bell-icon">
      <!-- <div alt="alert bell icon" class="bell-icon"> </div> -->
      <div class="display-flex">
        <div>
          <div>
            <a @click.prevent href="#">Username</a>
          </div>
          <div>
            <a @click.prevent href="#">Specialty</a>
          </div>
        </div>
        <img src="/user-icon-placeholder.jpg" class="user-icon">
      </div>
    </div>
  </div>
</div>
</template>

<script>

  export default {
    props: { isPage: { type: String } }
  }

</script>

<style scoped>

  a {
    color: #fdfdfd;
    text-decoration: none;
    font-family: 'Montserrat', sans-serif;
  }

</style>
