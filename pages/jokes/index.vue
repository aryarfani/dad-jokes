<template>
  <div>
    <SearchJokes v-on:search-text="searchText" />
    <div class="joke" v-for="joke in jokes" :key="joke.id">
      <Joke :joke="joke.joke" :id="joke.id" />
      <p></p>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import Joke from "@/components/Joke.vue";
import SearchJokes from "@/components/SearchJokes.vue";

export default {
  components: {
    Joke
  },
  data() {
    return {
      jokes: []
    };
  },
  head() {
    return {
      title: "Dad jokes",
      meta: [
        {
          hid: "description",
          name: "description",
          content: "Your place for corny dad jokes"
        }
      ]
    };
  },
  methods: {
    async searchText(text){
      const config = {
      headers: {
        Accept: "application/json"
      }
    };
    try {
      const res = await axios.get(`https://icanhazdadjoke.com/search?term=${text}`, config);
      this.jokes = res.data.results;
      console.log(this.jokes);
    } catch (error) {
      console.log(error);
    }
    }
  },
  async created() {
    const config = {
      headers: {
        Accept: "application/json"
      }
    };
    try {
      const res = await axios.get("https://icanhazdadjoke.com/search", config);
      this.jokes = res.data.results;
      console.log(this.jokes);
    } catch (error) {
      console.log(error);
    }
  }
};
</script>

<style>
</style>