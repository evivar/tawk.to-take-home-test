<template>
  <div class="category">
    <div class="category--breadcrumb">
      <span class="all" @click="goToHome">All categories</span>
      <i class="fa fa-chevron-right fa-fw icon" aria-label="Read"></i>
      <span class="category-title">{{ category.title }}</span>
    </div>
    <div class="category--container">
      <category-info :category="category" />
      <div class="category-container--article-list">
        <article-card v-for="(article, idx) in articles" :key="idx" :article="article" />
      </div>
    </div>
  </div>
</template>

<script>
import ArticleCard from "../components/ArticleCard.vue";
import axios from "axios";
import _ from "underscore";
import CategoryInfo from "../components/CategoryInfo.vue";

export default {
  components: { ArticleCard, CategoryInfo },
  data() {
    return {
      category: {},
      categories: [],
      articles: [],
    };
  },
  /**
   * The `mounted` function is automatically called when the Vue component is mounted
   * It performs the following tasks:
   * 1. Fetches category data from a REST API and selects a specific category based on the route parameter
   * 2. Fetches articles for the selected category and filters only the published ones
   * 3. Handles any potential errors during the HTTP requests and logs them to the console
   *
   * @async
   * @function mounted
   * @returns {void}
   */
  async mounted() {
    try {
      const responseCategories = await axios.get(`http://localhost:9000/api/categories`);
      this.category = _.findWhere(responseCategories.data, { id: this.$route.params.id });
      const responseArticles = await axios.get(
        `http://localhost:9000/api/category/${this.$route.params.id}`
      );
      responseArticles.data.forEach((article) => {
        if (article.status === "published") {
          this.articles.push(article);
        }
      });
    } catch (error) {
      console.log("error :>> ", error);
    }
  },
  methods: {
    /**
     * The `goToHome` function navigates the user to the "Home" route of the application.
     
     * @function goToHome
     * @returns {void}
     */
    goToHome() {
      this.$router.push({ name: "Home" });
    },
  },
};
</script>

<style lang="scss" scoped>
@import "../scss/_variables.scss";

.category {
  display: flex;
  flex-direction: column;
  justify-content: center;
  padding-left: 120px;
  padding-right: 180px;
  padding-bottom: 100px;
  background: #fafafa;
  &--breadcrumb {
    padding: 21px 0;
    font-family: $font-family;
    display: flex;
    align-items: center;
    flex-direction: row;
    gap: 13px;
    & > .all {
      font-size: 13px;
      color: $green;
      cursor: pointer;
    }
    & > .icon {
      width: 8px;
      color: #d3d3d3;
    }
    & > .category-title {
      font-size: 13px;
      color: $text-gray;
    }
  }
  &--container {
    font-family: $font-family;
    padding-top: 22px;
    height: 100%;
    // display: grid;
    // grid-template-columns: repeat(2, auto);
    display: flex;
    align-items: start;
    justify-content: center;
    gap: 20px;
    padding-left: 120px;
    padding-right: 180px;
    padding-bottom: 100px;
    &--article-list {
      display: flex;
      flex-direction: column;
      gap: 14px;
    }
  }
}
</style>
