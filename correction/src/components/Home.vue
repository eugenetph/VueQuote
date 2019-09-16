<template>
  <div class="container">
    <div class="title">
      <h1>Best quotes of the world</h1>
      <input v-model="searchedAuthor" placeholder="Author...">
    </div>
    <div class="authors-container">
      <h3>Favorite Authors</h3>
      <ul>
      <li 
        v-for="(author, index) in (listOfFavoriteAuthors)"
        :key="`author${index}`"
        >{{author}}</li></ul>
    </div>
    <div class="quotes-container">
      <quote
        v-for="item in (searchedListOfQuotes.slice(this.pageNumber, this.pageNumber+6))"
        :key="item.quote"
        :quote="item.quote"
        :author="item.author"
        :isFavorite="insideFavorite(item.author)"
        @likeEvent="updateLikedAuthors"
      />
    </div>
    <navigation @pageNumberEvent="updatepageNumber"/>
  </div>
</template>

<script>
import Navigation from "./Navigation.vue";
import Quote from "./Quote.vue";
export default {
  components: {
    Quote,
    Navigation
  },
  data: function() {
    return {
      pageNumber: 0,
      searchedAuthor: "",
      listOfQuotes: [], 
      listOfFavoriteAuthors: []
    };
  },
  created() {
    fetch("http://localhost:3001/")
      .then(data => data.json())
      .then(arr => {
        this.listOfQuotes = arr;
      });
  },
  methods: {
    updatepageNumber(value) {
      this.pageNumber = value;
    },
    updateLikedAuthors(value) {
      if(this.listOfFavoriteAuthors.includes(value)) {
        this.listOfFavoriteAuthors = this.listOfFavoriteAuthors.filter(item => item !== value)
      } else {  
        this.listOfFavoriteAuthors.push(value);
      }
    }, 
    insideFavorite(value) {
      return this.listOfFavoriteAuthors.includes(value)
    }
  },
  computed: {
    searchedListOfQuotes() {
      if (this.searchedAuthor !== "") {
        return this.listOfQuotes.filter(item =>
          item.author.toLowerCase().includes(this.searchedAuthor.toLowerCase())
        );
      }
      return this.listOfQuotes;
    }
  }
};
</script>

<style lang="scss" scoped>
.title {
  display: flex;
  align-items: center;
  h1 {
    margin-left: auto;
  }
}

input {
  height: 20px;
  width: 150px;
  margin-left: auto;
}

.container {
  display: flex;
  flex-direction: column;
  justify-content: space-between;
}

.quotes-container {
  margin-top: 30px;
  display: grid;
  grid-template-columns: auto auto auto;
  grid-template-rows: auto auto;
  grid-gap: 5px;
  margin-bottom: 50px;
  min-height: 400px;
  @media screen and (max-width: 600px) {
    display: block;
  }
}
.authors-container {
  text-align: left;
}
</style>
