<template>
  <div class="quote">
    <p>{{ quote.quote }}</p>
    <span>{{ quote.author }}</span>
    <button @click='likeEventListener' :class="isLiked ? 'quote-like active' : 'quote-like ínactive'">Like</button>
  </div>
</template>

<script>
export default {
  name: "Quote",
  props: {
    quote: Object,
    isLiked: Boolean
  },
  methods: {
    likeEventListener () {
      this.$emit('likeEventListener', this.quote.author);
    }
  }
};
</script>

<style scoped>
.quote {
    border: 1px solid #333;
    padding: 10px;
    min-height: 200px;
}
.quote-like {
    margin-left: 20px;
    padding: 10px;
    border: 1px block grey; 
    background: none;
    color: black;
    font-size: 12px;
}

.quote-like.active {
    background-color: #ece0dd;
}

.quote-like.inactive {
    background-color: #fab1a0;
}
</style>