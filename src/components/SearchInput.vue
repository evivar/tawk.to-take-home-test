<template>
  <div class="search-input">
    <input
      class="input-outlined"
      type="text"
      placeholder="Search for answers"
    />
    <div class="icon-container">
      <i class="fa-fw fas fa-search icon icon-container--icon" :aria-label="`Search`"></i>
    </div>
  </div>
</template>

<script>
export default {};
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
    color: black;
    background-color: transparent;
    border: 2px solid #eeeeee;
    border-top-left-radius: 5px;
    border-bottom-left-radius: 5px;
    outline: none;
    transition: border-color 0.3s ease, background-color 0.3s ease, color 0.3s ease;
  }

  .input-outlined:focus {
    border-color: #eeeeee;
    box-shadow: 0 0 4px 0 #eeeeee;
  }

  .input-outlined::placeholder {
    color: #9c9aa6;
    opacity: 0.6;
  }
  & > .icon-container {
    padding: 20px 30px;
    background: $green;
    border-top-right-radius: 5px;
    border-bottom-right-radius: 5px;
    &--icon {
      color: white;
    }
  }
}

.icon{
    color: white;
}
</style>
