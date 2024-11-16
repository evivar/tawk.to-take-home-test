<template>
  <div class="article-card">
    <div class="article-card--info">
      <i :class="getIconClass(article.icon)" class="fa-fw icon" aria-hidden="true"></i>
      <div class="article-card--info__details">
        <span class="title">{{ article.title }}</span>
        <span class="updated">Updated {{ getLastUpdated(article.updatedOn) }}</span>
      </div>
    </div>
    <div class="article-card--action">
      <i class="fa fa-chevron-right icon" aria-label="Read"></i>
    </div>
  </div>
</template>

<script>
import moment from "moment";

export default {
  props: {
    article: {
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
  },
};
</script>

<style lang="scss" scoped>
@import "../scss/variables";

.article-card {
  display: flex;
  width: 640px;
  flex-direction: row;
  justify-content: space-between;
  align-items: center;
  padding-left: 40px;
  padding-right: 40px;
  padding-top: 35px;
  padding-bottom: 35px;
  background: white;
  border: 1px solid $border-color;
  border-radius: 4px;
  &--info {
    display: flex;
    flex-direction: row;
    align-items: center;
    &__details {
      margin-left: 16px;
      display: flex;
      margin-left: 16px;
      flex-direction: column;
      & > .title {
        font-size: 20px;
        font-weight: 400;
      }
      & > .updated {
        font-size: 11px;
        font-weight: 400;
        color: $text-gray;
      }
    }
  }
}
.icon {
  color: $green;
}
</style>
