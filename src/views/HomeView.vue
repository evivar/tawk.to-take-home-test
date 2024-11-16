<template>
  <div class="home">
    <category-card
      v-for="category in categories"
      :key="category.id"
      :category="category"
    />
  </div>
</template>

<script>
import axios from "axios";
import _ from "underscore";
import CategoryCard from "../components/CategoryCard.vue";

export default {
  components: { CategoryCard },
  data() {
    return {
      categories: [],
      categoriesError: null,
    };
  },
  /**
   * The `mounted` function is automatically called when the Vue component is mounted
   * It performs the following tasks:
   * 1. Attempts to fetch categories from a REST API
   * 2. Filters enabled categories and sorts them by the `order` property
   * 3. Handles any potential errors during the HTTP request and stores them in a reactive property
   *
   * @async
   * @function mounted
   * @returns {void}
   */
  async mounted() {
    try {
      this.categoriesError = null;
      const response = await axios.get("http://localhost:9000/api/categories");
      response.data.forEach((category) => {
        if (category.enabled) {
          this.categories.push(category);
        }
      });
      this.categories = _.sortBy(this.categories, "order");
    } catch (error) {
      console.log("error :>> ", error);
      this.categoriesError = error;
    }
  },
};
</script>

<style lang="scss" scoped>
@import "../scss/_variables.scss";

.home {
  font-family: $font-family;
  padding-top: 60px;
  background: #fafafa;
  height: 100%;
  display: grid;
  grid-template-columns: repeat(3, auto);
  align-items: center;
  justify-content: center;
  gap: 20px;
  padding-left: 148px;
  padding-right: 148px;
  padding-bottom: 100px;
}
</style>
