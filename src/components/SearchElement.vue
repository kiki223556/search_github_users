<template>
  <div class="search-element">
    <SearchHead></SearchHead>
    <SearchList></SearchList>
  </div>
</template>

<script setup lang="ts">
import SearchHead from "./SearchHead.vue";
import SearchList from "./SearchList.vue";
</script>

<style scoped>
.search-element {
  margin: 50px;
}
</style>
