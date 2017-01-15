<template>
  <div>
    <input type="text" class="search-user" placeholder="Enter a username..." v-model="searchedItem">
  </div>
</template>

<script>
  import { debounce } from 'lodash/fp';

  export default {
    name: 'search-bar',
    data() {
      return {
        searchedItem: '',
      }
    },
    watch: {
      searchedItem(newValue) {
        this.$emit('onSearch', newValue);
      }
    }
  }
</script>

<style scoped>
  .search-user {
    outline: none;
    border: none;
    width: 300px;
    padding: 10px;
    color: gray;
    margin: 20px auto;
    box-shadow: 0px 3px 6px 2px rgba(0,0,0,0.3);
  }
</style>