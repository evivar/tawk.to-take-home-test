<template>
  <div class="category-card" @click="onCategoryCardClick">
    <i
      :class="getIconClass(category.icon)"
      class="fa-fw fa-3x icon"
      :aria-label="`Icon for ${category.title}`"
    ></i>
    <div class="category-card--info">
      <span class="name">{{ category.title }}</span>
      <span class="articles">{{ category.totalArticle }} articles</span>
      <span class="updated">Last updated {{ getLastUpdated(category.updatedOn) }}</span>
    </div>
  </div>
</template>
<script>
import moment from "moment";

export default {
  props: {
    category: {
      type: Object,
      default: () => {},
    },
  },
  methods: {
    /**
     * The `getIconClass` function generates a CSS class string for a Font Awesome icon
     *
     * @function getIconClass
     * @param {string} iconName - The name of the icon
     * @returns {string} - A CSS class string in the format `fas fa-{iconName}`
     */
    getIconClass(iconName) {
      return `fas fa-${iconName}`;
    },
    /**
     * The `getLastUpdated` function formats a given date as a relative time string using moment.js library
     *
     * @function getLastUpdated
     * @param {string|Date} updatedOn - The date or timestamp to be formatted
     * @returns {string} - A string representing the relative time since the given date
     */
    getLastUpdated(updatedOn) {
      return moment(updatedOn).fromNow();
    },
    /**
     * The `onCategoryCardClick` function navigates the user to a specific category page using the Vue Router
     *
     * @function onCategoryCardClick
     * @returns {void}
     */
    onCategoryCardClick() {
      this.$router.push({ name: "Category", params: { id: this.category.id } });
    },
  },
};
</script>
<style lang="scss" scoped>
@import "../scss/_variables.scss";

.category-card {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: space-evenly;
  border: 1px solid #eeeeee;
  border-radius: 5px;
  width: 315px;
  height: 220px;
  background: #ffffff;
  cursor: pointer;
  & > .icon {
    color: $green;
  }
  &--info {
    display: flex;
    flex-direction: column;
    align-items: center;
    & > .name {
      color: #373737;
      font-size: 20px;
      margin-bottom: 21px;
    }
    & > .articles {
      color: $green;
      font-size: 13px;
    }
    & > .updated {
      color: #9c9aa6;
      font-size: 11px;
    }
  }
}
</style>
