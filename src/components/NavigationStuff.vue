<template>
<div>
    <nav>
      <figure>
        <img src="../assets/heroLogo.svg" alt="foodl Logo">
      </figure>
      <div>
        <router-link to="/">Home</router-link>
        <router-link to="/about">Search</router-link>
      </div>
    </nav>
</div>
  
</template>

<script>
export default {

}
</script>

<style scoped>
nav{
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 19px 118px 94px 0px;
}

nav a{
  margin-right: 72px;
  text-decoration: none;
  font-family: 'IBM Plex Sans';
  font-style: normal;
  font-weight: 400;
  font-size: 18px;
  line-height: 130%;
  /* or 23px */
  color: #000000;
}

nav a:hover{
  font-weight: 700;
}

</style>