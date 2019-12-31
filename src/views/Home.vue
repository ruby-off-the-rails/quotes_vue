<template>
  <div class="home">
    <button v-on:click="filterTheme('games')">Filter quotes by games</button>
    <button v-on:click="filterTheme('movies')">Filter quotes by movies</button>
    <div v-for="quote in shownQuotes">
      <p>{{ quote.source }}</p>
      <p>{{ quote.quote }}</p>
      <p>{{ quote.theme }}</p>
      <hr>
    </div>
    <button v-on:click="showPage(1)">1</button>
    <button v-on:click="showPage(2)">2</button>
    <button v-on:click="showPage(3)">3</button>
  </div>
</template>

<style>
</style>

<script>
import axios from "axios";
export default {
  data: function() {
    return {
      message: "Welcome to Vue.js!",
      quotes: [],
      shownQuotes: []
    };
  },
  created: function() {
    // get the data from gist.github.com...
    axios.get("https://gist.githubusercontent.com/benchprep/dffc3bffa9704626aa8832a3b4de5b27/raw/quotes.json").then(response => {
      console.log(response.data)
      this.quotes = response.data;
      this.shownQuotes = this.quotes;
      // page 1
      // this.quotes = this.quotes.slice(0,15)
      // page 2
      // this.quotes = this.quotes.slice(16,31)
      // page 3
      // this.quotes = this.quotes.slice(32,48)
    })
  },
  methods: {
    showPage: function(pageNumber) {
      console.log(pageNumber);
      var startingNumber = (pageNumber - 1) * 16;
      var endingNumber = startingNumber + 15;
      console.log('showing the page...');
      this.shownQuotes = this.quotes.slice(startingNumber, endingNumber);
    },
    filterTheme: function(themeName) {
      console.log(themeName);
      var newArray = [];
      this.quotes.forEach(function(quote) {
        if (quote.theme === themeName) {
          newArray.push(quote);
        }
      })
      this.shownQuotes = newArray;
    }
  }
};
</script>
