<template>
  <div class="quote">
    <p>{{quote}}</p>
    <span>{{author}}</span>
    <button @click="likeEvent" :class="isFavorite ? 'active' : ''">
      Like
    </button>
  </div>
</template>

<script>

export default {
  props: {
    author: String,
    quote: String,
    isFavorite: Boolean
  },
  methods: {
    likeEvent() {
      this.$emit('likeEvent', this.author);
    }
  }
};
</script>

<style lang="scss" scoped>
.quote {
  border: 1px solid #333;
  padding: 10px;
  min-height: 200px;
}
button {
  margin-left: 20px;
  padding: 10px;
  border: 1px block grey; 
  background: none;
}

button.active {
  background-color: #fab1a0;
}
</style>
