<template>
  <div class="quotes-container">
    <Quote :key="index" v-for="(quote, index) in quoteData" :quote="quote" />
    <!-- <p>test</p> -->
  </div>
</template>

<script>
import Quote from "./Quote.vue";

export default {
  name: "QuoteContainer",
  components: {
    Quote
  },
  props: {
    quoteData: Array,
    toSearch: String
  }
};
</script>

<style scoped>
@media screen and (max-width: 550px) {
  .quotes-container {
    display: block;
  }
}

.quotes-container {
  margin-top: 30px;
  display: grid;
  grid-template-columns: auto auto auto;
  grid-template-rows: auto auto;
  grid-gap: 5px;
  margin-bottom: 50px;
  min-height: 400px;
}
</style>