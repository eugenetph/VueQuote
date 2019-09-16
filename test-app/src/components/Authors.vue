<template>
  <div class="authors-container">
    <h3>Favorite Authors</h3>
    <ul>
      <li>something</li>
    </ul>
    <!-- <ul :for="name in names">
      <li>{{ name }}</li>
    </ul> -->
  </div>
</template>

<script>
export default {
  name: "Authors",
  props: {
    names: Array
  }
};
</script>

<style scoped>
.authors-container {
    text-align: left;
}
</style>