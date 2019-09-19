<template>
  <div id="app">
    <div class="container">
      <div class="title">
        <h1>Best quotes of the world</h1>
        <input placeholder="Author..." v-model="searchedByAuthor" />
        <!-- <input placeholder="Author..." :value="searchedByAuthor" @input="searchedByAuthor = $event.target.value" /> -->
      </div>
      <Navigation @pageNumberEvent="updatepageNumber" :maxPageNumber="Math.floor(searchQuoteList.length/9)"/>
      <Authors :favoriteAuthorList="favoriteAuthorList" />
      <QuoteContainer
        :quoteList="searchQuoteList.slice(9 * pageNumber,9 * (pageNumber+1))"
        :favoriteAuthorList="favoriteAuthorList"
        @updateFavoriteAuthorList="updateFavoriteAuthorList"
      />
    </div>
  </div>
</template>

<script>
// import HelloWorld from "./components/HelloWorld.vue";
import QuoteContainer from "./components/QuoteContainer.vue";
import Authors from "./components/Authors.vue";
import Navigation from "./components/Navigation.vue"
import axios from "axios";

export default {
  name: "app",
  components: {
    QuoteContainer,
    Authors,
    Navigation
  },
  data() {
    return {
      dataSource: [],
      searchedByAuthor: "",
      favoriteAuthorList: [],
      pageNumber: 0
    };
  },
  mounted() {
    axios.get("http://localhost:3001").then(response => {
      this.dataSource = response.data;
    });
  },
  computed: {
    searchQuoteList() {
      if (this.searchedByAuthor) {
        return this.dataSource.filter(quote =>
          quote.author
            .toLowerCase()
            .includes(this.searchedByAuthor.toLowerCase())
        );
      }
      return this.dataSource;
    }
  },
  methods: {
    updateFavoriteAuthorList(authorName) {
      let isExisted = this.favoriteAuthorList
        ? this.favoriteAuthorList.includes(authorName)
        : false;
      if (isExisted) {
        this.favoriteAuthorList = this.favoriteAuthorList.filter(
          author => author !== authorName
        );
      } else {
        this.favoriteAuthorList = [...this.favoriteAuthorList, authorName];
      }
    },
    updatepageNumber(page) {
      this.pageNumber = page
    }
  }
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
body {
  padding: 20px;
}
input {
  height: 20px;
  width: 150px;
  margin-left: auto;
}
.title {
  display: flex;
  align-items: center;
}
.container {
  display: flex;
  flex-direction: column;
  justify-content: space-between;
}
.title h1 {
  margin-left: auto;
}
</style>
