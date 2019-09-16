<template>
  <div class="authors-container">
    <h3>Favorite Authors</h3>
    <!-- <ul>
      <li>something</li>
    </ul> -->
    <ul :key="index" v-for="(author, index) in favoriteAuthorList">
      <li>{{ author }}</li>
    </ul>
  </div>
</template>

<script>
export default {
  name: "Authors",
  props: {
    favoriteAuthorList: Array
  }
};
</script>

<style scoped>
.authors-container {
    text-align: left;
}
</style>