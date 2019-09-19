<template>
  <div class="nav-button">
    <button @click="back()" :class="{disabled: isStartPage()}" :disabled="isStartPage()">&lt;- Prev</button>
    <span>{{pageNumber}}</span>
    <button @click="next()" :class="{disabled: isEndPage()}" :disabled="isEndPage()">Next -&gt;</button>
  </div>
</template>

<script>
export default {
  name: "Navigation",
  data: function() {
    return {
      pageNumber: 0
    };
  },
  props: {
    maxPageNumber: Number
  },
  methods: {
    isStartPage() {
      return this.pageNumber === 0;
    },
    isEndPage() {
      return this.pageNumber === this.maxPageNumber;
    },
    back() {
      this.pageNumber =
        this.pageNumber > 0 ? this.pageNumber - 1 : this.pageNumber;
      this.$emit("pageNumberEvent", this.pageNumber);
    },
    next() {
      this.pageNumber =
        this.pageNumber < this.maxPageNumber ? this.pageNumber + 1 : this.pageNumber;
      this.$emit("pageNumberEvent", this.pageNumber);
    }
  }
};
</script>

<style scoped>
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
