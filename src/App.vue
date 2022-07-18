<template>

  
  <router-view />
</template>

<script>
import HomeViewVue from "./views/HomeView.vue";
export default {
  components: {
    "app-Home": HomeViewVue,
  },
};
</script>

<style scoped>

html,
body {
  font-family: "IBM Plex Sans", sans-serif;
  max-width: 100%;
  overflow-x: hidden;
}


nav {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 19px 118px 94px 120px;
}

nav a {
  margin-right: 72px;
  font-style: normal;
  font-weight: 700;
  font-size: 18px;
  line-height: 130%;
  /* or 23px */
  letter-spacing: -0.04em;
  color: #000000;
  text-decoration: none;
}
</style>
