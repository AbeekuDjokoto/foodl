<template>
  <div class="container">
    <app-nav></app-nav>
    <div class="search">
      <h1>What ingredients do you have?</h1>
      <img src="../assets/searchIcon.svg" alt="" @click="searchResult()" class="searchImg">
      <input type="text" placeholder="Search for a meal" dir="ltr" v-model="result" @keyup.enter="searchResult()">
    </div>
      <div class="cardFlex">
        <div v-for="category in categories" :key="category.idMeal" class="card">
          <figure>
            <router-link :to="'/about/' + category.idMeal"><img :src="category.strMealThumb" alt="" class="foodImg"></router-link>
            <figcaption class="para">{{ category.strMeal }}</figcaption>
          </figure>
        </div>
      </div>
      
  </div>
</template>

<script>
import NavigationStuffVue from '@/components/NavigationStuff.vue'
import axios from 'axios'
export default {
  components: {
    "app-nav": NavigationStuffVue, 
  },
  data(){
      return{
        result: "",
        categories: [],
        tests: [],
        searchNotFound: ''
      }
    },
  created(){
          axios.get('https://www.themealdb.com/api/json/v1/1/random.php').then(response => {
          this.tests = response.data.meals
          console.log(response.data.meals)
      });
  },
  methods: {
    async searchResult(){
        await axios.get(`https://www.themealdb.com/api/json/v1/1/filter.php?i=${this.result}`).then(response =>{
        this.categories = response.data.meals
        console.log(this.categories)
        if(response.data.meals == null){
          console.log('Search result not found')
        }
      }).catch((err) => console.log(err))
      
      
    },
  }
}
</script>

<style scoped>
  .container{
    background-image: url('../assets/bgSearch.svg');
    background-repeat: no-repeat;
    padding-left: 120px;
    padding-bottom: 78px;
  }

.search{
  text-align: center;
  align-items: center;
}

h1{
  font-style: normal;
  font-weight: 700;
  font-size: 32px;
  line-height: 100%;
  /* identical to box height, or 32px */
  letter-spacing: -0.04em;
  color: #000000;
  margin-bottom: 24px;
}

.search input{
  padding: 14px 0px 24px 0px;
  width: 50%;
  background: #FFFFFF;
  box-shadow: 0px 14px 24px -8px rgba(182, 84, 14, 0.11);
  border-radius: 11px;
  border: none;
  font-family: 'IBM Plex Sans';
  font-style: normal;
  font-weight: 500;
  font-size: 24px;
  line-height: 100%;
  text-align: center;
}

.search input:focus{
  outline: none;
}

.searchImg{
  position: relative;
  left: 30px;
}

.cardFlex{
  display: flex;
  flex-wrap: wrap;
  justify-content: space-evenly;
  gap: 20px;
  margin-top: 104px;
}

.foodImg{
  width: 248px;
  box-shadow: 0px 32px 48px -16px rgba(0, 0, 0, 0.25);
  border-radius: 8px;
  position: relative;
  left: 20px;
}

.para{
  position: relative;
  z-index: -1;
  top: -220px;
  padding: 224px 0px 28px 22px;
  width: 285px;
  background: #FFFFFF;
  box-shadow: 0px 24px 64px -16px rgba(0, 0, 0, 0.1);
  border-radius: 16px;
  font-family: 'IBM Plex Sans';
  font-style: normal;
  font-weight: 400;
  font-size: 18px;
  line-height: 100%;
  color: black;
}


</style>
