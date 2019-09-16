<template>
  <div class="nav-button">
    <button @click="back()" :class="{disabled: isStart()}" :disabled="isStart()">&lt;- Prev</button>
    <span>{{pageNumber}}</span>
    <button @click="next()" :class="{disabled: isEnd()}" :disabled="isEnd()">Next -&gt;</button>
  </div>
</template>

<script>
export default {
  data: function() {
    return {
      pageNumber: 0
    };
  },
  methods: {
    isStart() {
      return this.pageNumber === 0;
    },
    isEnd() {
      return this.pageNumber === 15;
    },
    back() {
      if (this.pageNumber > 0) {
        this.pageNumber--;
        this.$emit("pageNumberEvent", this.pageNumber);
      }
    },
    next() {
      if (this.pageNumber < 15) {
        this.pageNumber++;
        this.$emit("pageNumberEvent", this.pageNumber);
      }
    }
  }
};
</script>

<style lang="scss" scoped>
.nav-button {
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  align-items: center;
  font-size: 18px;
}
button {
  background-color: gray;
  color: #fff;
  padding: 20px;
  font-size: 15px;
  border-radius: 0;
}
.disabled {
  background: lightgray;
}
</style>
