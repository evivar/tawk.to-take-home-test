<template>
  <div class="category-info">
    <div id="icon--container">
      <i
        :class="getIconClass(category.icon)"
        class="fa-fw fa-3x icon"
        :aria-label="`Icon for ${category.title}`"
      ></i>
      <i
        :class="getIconClass(category.icon)"
        class="fa-fw fa-3x icon-shadow"
        :aria-label="`Icon for ${category.title}`"
      ></i>
    </div>
    <div class="category-info--info">
      <span class="name">{{ category.title }}</span>
      <span class="articles">{{ category.totalArticle }} articles</span>
      <span class="updated">Last updated {{ getLastUpdated(category.updatedOn) }}</span>
    </div>
    <hr class="separator" />
    <div class="category-info--desc">
      <i class="fa fa-info-circle icon" aria-label="Read"></i>
      <p class="description">{{ category.description }}</p>
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
  },
};
</script>
<style lang="scss" scoped>
@import "../scss/_variables.scss";

.category-info {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: space-evenly;
  border: 1px solid $border-color;
  border-radius: 5px;
  width: 280px;
  background: #ffffff;
  padding-top: 40px;
  padding-bottom: 50px;
  & > .icon {
    color: $green;
  }
  &--info {
    display: flex;
    flex-direction: column;
    align-items: center;
    & > .name {
      color: $text-black;
      font-size: 20px;
      margin-bottom: 21px;
      text-align: center;
    }
    & > .articles {
      color: $green;
      font-size: 13px;
    }
    & > .updated {
      color: $text-gray;
      font-size: 11px;
    }
  }
  &--desc {
    display: flex;
    flex-direction: column;
    align-items: center;

    padding-left: 30px;
    padding-right: 30px;
    & > .description {
      font-size: 13px;
      color: $text-gray;
      text-align: center;
    }
  }
}

.separator {
  height: 1px;
  background-color: $border-color;
  border: none;
  width: 100%;
  margin: 20px 0;
}

.icon {
  color: $green;
}

#icon--container {
  position: relative;
  & > .icon-shadow {
    color: $green;
    position: absolute;
    left: 7px;
    top: 7px;
    opacity: 0.25;
  }
}
</style>
