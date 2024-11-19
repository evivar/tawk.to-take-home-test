<template>
  <div class="search">
    <breadcrumb :title="`Seach: ${this.$route.params.query}`" />
    <div class="search--article-list" v-if="articles.length > 0">
      <article-card v-for="(article, idx) in articles" :key="idx" :article="article" />
    </div>
    <div class="search--no-results" v-else>
      <span>No results</span>
    </div>
  </div>
</template>
<script>
import axios from "axios";
import ArticleCard from "../components/ArticleCard.vue";
import Breadcrumb from "../components/Breadcrumb.vue";

export default {
  components: { ArticleCard, Breadcrumb },
  data() {
    return {
      articles: [],
    };
  },
  async mounted() {
    await this.getArticles();
  },
  watch: {
    "$route.params.query": {
      immediate: true,
      handler() {
        this.getArticles();
      },
    },
  },
  methods: {
    async getArticles() {
      const query = this.$route.params.query;
      console.log('query :>> ', query);
      this.articles = [];
      try {
        const response = await axios.get(`http://localhost:9000/api/search/${query}`);
        if (response.data) {
          const responseFiltered = response.data.filter((article) =>
            article.title.toLowerCase().includes(query.toLowerCase()) && article.status !== "archived"
          );
          this.articles = responseFiltered;
        }
      } catch (error) {
        console.log("error :>> ", error);
      }
    },
  },
};
</script>
<style lang="scss" scoped>
@import "../scss/_variables.scss";
.search {
  background: #fafafa;
  font-family: $font-family;
  &--article-list {
    padding-top: 2rem;
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 1rem;
  }
  &--no-results {
    display: flex;
    align-items: center;
    justify-content: center;
  }
}
</style>
