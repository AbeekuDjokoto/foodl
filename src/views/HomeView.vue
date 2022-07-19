<template>
  <div class="container">

    <app-nav></app-nav>

    <div class="heroMain">
      <div>
        <h1>Find recipes for the ingredients you have on hand</h1>
        <router-link to="/about"><app-button :text="searchButtonText"></app-button></router-link>
      </div>
      <figure class="figure">
        <img class="bowlImage" src="../assets/bowlImage.svg" alt="bowlImage">
        <img class="blackRectangle" src="../assets/blackRectangle.svg" alt="bowlImage">
      </figure>
      </div>
  </div>
</template>

<script>
import ButtonsVue from "@/components/Buttons.vue";
import NavigationVue from "@/components/NavigationStuff.vue"
export default {
  components: {
    "app-button": ButtonsVue,
    "app-nav": NavigationVue,
  },
  data() {
    return {
      searchButtonText: "Search Now",
    };
  },
};
</script>

<style scoped>

.container {
  padding-left: 120px;
  max-width: 100%;
  overflow-x: hidden;
  background: #E98237;
}

h1 {
  font-family: "IBM Plex Sans";
  font-style: normal;
  font-weight: 700;
  font-size: 48px;
  line-height: 130%;
  /* or 62px */
  letter-spacing: -0.04em;
  color: #000000;
  margin-bottom: 32px;
  width: 442px;
  margin-top: 120px;
}

.heroMain{
  display: flex;
}

.figure{
  display: flex;
}

.blackRectangle{
  position: relative;
  right: 180px;
  z-index: 0; 
}

.bowlImage{
  width: 519px;
  z-index: 1;
}

@media only screen and (max-width: 375px) {
  .container {
  padding-left: 12px;
}

h1 {
  font-size: 48px;
  margin-bottom: 32px;
  width: auto;
  margin-top: 40px;
}

.heroMain{
  flex-wrap: wrap;
}
.figure{
  margin-top: 40px;
}
.blackRectangle{
  position: relative;
  right: 180px;
  z-index: 0; 
}

.bowlImage{
  width: 319px;
  z-index: 1;
}
}
</style>
