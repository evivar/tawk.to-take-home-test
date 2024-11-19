<template>
  <div class="search-input">
    <input
      class="input-outlined"
      type="text"
      placeholder="Search for answers"
      v-model="searchQuery"
    />
    <div class="icon-container">
      <i
        class="fa-fw fas fa-search icon icon-container--icon"
        :aria-label="`Search`"
        @click="onSearchClick"
      ></i>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      searchQuery: null,
    };
  },
  methods: {
    onSearchClick() {
      if (this.searchQuery) {
        this.$router.push({ name: "Search", params: { query: this.searchQuery.trim() } });
      }
    },
  },
};
</script>

<style lang="scss" scoped>
@import "../scss/_variables.scss";

.search-input {
  display: flex;
  flex-direction: row;
  align-items: center;
  width: 720px;
  & > .input-outlined {
    display: block;
    width: 100%;
    padding: 20px 30px;
    font-size: 14px;
    font-family: inherit;
    color: $text-black;
    background-color: transparent;
    border: 2px solid $border-color;
    border-top-left-radius: 5px;
    border-bottom-left-radius: 5px;
    outline: none;
    transition: border-color 0.3s ease, background-color 0.3s ease, color 0.3s ease;
  }

  .input-outlined:focus {
    border-color: $border-color;
    box-shadow: 0 0 4px 0 $border-color;
  }

  .input-outlined::placeholder {
    color: $text-gray;
    opacity: 0.6;
  }
  & > .icon-container {
    cursor: pointer;
    padding: 20px 30px;
    background: $green;
    border-top-right-radius: 5px;
    border-bottom-right-radius: 5px;
    border: 1px solid $green;
    &--icon {
      color: white;
    }
  }
}

.icon {
  color: white;
}
</style>
