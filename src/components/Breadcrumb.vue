<template>
  <div class="breadcrumb">
    <span class="all" @click="goToHome">All categories</span>
    <i class="fa fa-chevron-right fa-fw icon" aria-label="Read"></i>
    <span class="category-title">{{ title }}</span>
  </div>
</template>

<script>
export default {
  props: {
    title: {
      type: String,
      default: "",
    },
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
.breadcrumb {
  padding: 21px 0;
  font-family: $font-family;
  display: flex;
  align-items: center;
  flex-direction: row;
  margin-left: 2.5rem;
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
</style>
