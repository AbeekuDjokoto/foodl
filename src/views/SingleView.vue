<template>
  <div class="container">
    <app-nav></app-nav>
    <div class="singleImageInfoFlex">
      <figure>
        <img class="singleImage" :src="singleArticle.strMealThumb" alt="" />
      </figure>
      <div>
        <h1 class="heroTitle">{{ singleArticle.strMeal }}</h1>
        <div class="cardContainer">
          <div :class="singleArticle.strCategory ? 'card' : 'emptyCard'">
            <figure class="cardFlex">
              <img class="cardImg" :src="cardImg.category" alt="" />
              <div>
                <p class="cardText">Categories</p>
              </div>
            </figure>
            <h1 class="cardInfo">{{ singleArticle.strCategory }}</h1>
          </div>
          <div :class="singleArticle.strArea ? 'card' : 'emptyCard'">
            <figure class="cardFlex">
              <img class="cardImg" :src="cardImg.location" alt="" />
              <div>
                <p class="cardText">Area</p>
              </div>
            </figure>
            <h1 class="cardInfo">{{ singleArticle.strArea }}</h1>
          </div>
          <div :class="singleArticle.strTags ? 'card' : 'emptyCard'">
            <figure class="cardFlex">
              <img class="cardImg" :src="cardImg.tag" alt="" />
              <div>
                <p class="cardText">Tags</p>
              </div>
            </figure>
            <h1 class="cardInfo">{{ singleArticle.strTags }}</h1>
          </div>
        </div>
      </div>
    </div>

    <div class="ingredientsCard">
      <h1 class="ingredientTitle">Ingredients</h1>
      <div class="buttonCardFlex">
        <div class="buttonCard" v-for="item in ingAndMeas" :key="item.ingredient">
          <p>
            {{ item.ingredient
            }}<span>{{ item.measure }}</span>
          </p>
        </div>
        <div class="buttonCard">
          <p>
            {{ singleArticle.strIngredient2
            }}<span>{{ singleArticle.strMeasure2 }}</span>
          </p>
        </div>
      </div>
    </div>

    <div class="heroInstructions">
      <h1 class="instructions">Instructions</h1>
      <div v-for="(value, index) in instructions" :key="index">
        <h2 class="instructionText">{{ value }}</h2>
      </div>
    </div>
  </div>
</template>

<script>
import NavigationStuffVue from "@/components/NavigationStuff.vue";
export default {
  components: {
    "app-nav": NavigationStuffVue,
  },
  data() {
    return {
      id: this.$route.params.id,
      singleArticle: {},
      instructions: [],
      result: [],
      ingredients: [],
      measurements: [],
      ingAndMeas: [],
      cardImg: {
        category: require("@/assets/categoryImg.svg"),
        location: require("@/assets/location.svg"),
        tag: require("@/assets/tag.svg"),
      },
    };
  },
  created() {
    fetch("https://www.themealdb.com/api/json/v1/1/lookup.php?i=" + this.id)
      .then((response) => response.json())
      .then((response) => {
        // console.log(response.meals[0]);
        this.singleArticle = response.meals[0];
        Object.entries(this.singleArticle).forEach(([key, value]) => {
          if (key.startsWith("strIngredient") && value.trim() !== "") {
            this.ingredients.push(value);
          }

          if (key.startsWith("strMeasure") && value.trim()) {
            this.measurements.push(value);
          }
        });

        this.ingredients.forEach((ing, index) => {
          this.ingAndMeas.push({
            ingredient: ing,
            measure: this.measurements[index],
          });
        });

        console.log(this.ingAndMeas);
        this.result = response.meals[0].strInstructions.split("\r\n");
        this.instructions = this.result.filter(Boolean);
        // console.log(this.instructions);
      });
  },
};
</script>

<style scoped>
.container {
  background-image: url("../assets/Group1.svg");
  background-repeat: no-repeat;
  background-size: contain;
  padding-left: 120px;
  padding-bottom: 84px;
}

.emptyCard{
  display: none;
}

.singleImageInfoFlex {
  display: flex;
  justify-content: flex-start;
}

.singleImage {
  background: url("../assets/bgSearch.svg"), #fbfbfb;
  box-shadow: 0px 32px 48px -16px rgba(0, 0, 0, 0.25);
  border-radius: 8px;
  width: 260px;
  margin: -50px 40px 92px 190.4px;
}

.heroTitle {
  font-family: "IBM Plex Sans";
  font-style: normal;
  font-weight: 700;
  font-size: 40px;
  line-height: 100%;
  /* identical to box height, or 40px */
  letter-spacing: -0.02em;
  color: #000000;
  margin: -30px 0px 24px 0px;
}

.cardContainer {
  display: flex;
  flex-wrap: wrap;
  gap: 16px;
}
.card {
  background: rgba(255, 255, 255, 0.3);
  box-shadow: 0px 8px 8px rgba(0, 0, 0, 0.05),
    inset 1px 1px 2px rgba(255, 255, 255, 0.37);
  backdrop-filter: blur(94px);
  /* Note: backdrop-filter has minimal browser support */
  border-radius: 4px;
  /* Inside auto layout */
  flex: none;
  order: 0;
  flex-grow: 0;
  align-items: center;
  padding: 15px 24px 12px 24px;
}

.cardFlex {
  display: flex;
  align-items: center;
}

.cardText {
  margin-left: 6px;
  font-family: "IBM Plex Sans";
  font-style: normal;
  font-weight: 400;
  font-size: 10px;
  line-height: 100%;
  /* identical to box height, or 10px */
  letter-spacing: 0.09em;
  text-transform: uppercase;
  color: #954f1d;
  /* Inside auto layout */
  flex: none;
  order: 1;
  flex-grow: 0;
}

.cardInfo {
  font-family: "IBM Plex Sans";
  font-style: normal;
  font-weight: 400;
  font-size: 20px;
  line-height: 100%;
  /* identical to box height, or 20px */
  letter-spacing: -0.02em;
  color: #000000;
  /* Inside auto layout */
  flex: none;
  order: 1;
  flex-grow: 0;
  margin-top: 10px;
}

.ingredientsCard {
  margin-left: auto;
  margin-right: auto;
  width: 590px;
  padding: 27px 0px 39px 33px;
  background: rgba(255, 255, 255, 0.6);
  box-shadow: 0px 24px 64px -16px rgba(0, 0, 0, 0.1),
    inset 0px 4px 2px rgba(255, 255, 255, 0.65);
  backdrop-filter: blur(24px);
  /* Note: backdrop-filter has minimal browser support */
  border-radius: 10px;
}

.ingredientTitle {
  margin-bottom: 35px;
  font-family: "IBM Plex Sans";
}

.buttonCardFlex {
  display: flex;
  flex-wrap: wrap;
  gap: 20px;
}

.buttonCard {
  padding: 11px 10px 11px 16px;
  background: #fff;
  border-radius: 30px;
  border: 1px solid  #919191;
}

.buttonCard:hover {
  background: #ff9f59;
  border: none;
}

.buttonCard p:hover {
  font-family: "IBM Plex Sans";
  color: #000000;
}

.buttonCard span {
  font-family: "IBM Plex Sans";
  padding: 2px 8px;
  background: #aaaaaa;
  border-radius: 30px;
  /* Inside auto layout */
  flex: none;
  order: 1;
  flex-grow: 0;
  margin-left: 10px;
}

.buttonCard span:hover {
  color: #ff9f59;
  background: #ffffff;
}

.heroInstructions {
  margin-top: 72px;
  margin-left: 275px;
}

.instructions {
  margin-bottom: 32px;
}

.instructionText {
  font-family: "IBM Plex Sans";
  width: 598px;
  font-style: normal;
  font-weight: 400;
  font-size: 16px;
  line-height: 165%;
  /* or 26px */
  text-transform: capitalize;
  color: #000000;
  margin-bottom: 10px;
}

@media only screen and (max-width: 375px) {
  .container {
    background-size: contain;
    padding-left: 20px;
  }

  .singleImageInfoFlex {
    flex-wrap: wrap;
  }

  .singleImage {
    margin: 10px 40px 52px 0px;
  }

  .ingredientsCard {
    width: max-content;
    padding: 27px 56px 46.5px 32px;
    border-radius: 10px;
    margin-top: 20px;
    margin-left: 0px;
  }

  .heroInstructions {
    margin-left: auto;
  }

  .instructionText {
    width: auto;
    margin-bottom: 10px;
    padding-right: 10px;
  }
}
</style>
