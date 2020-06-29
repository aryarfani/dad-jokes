<template>
  <div>
    <div>Joke for {{ $route.params.id }}</div>
    <Joke :joke="joke.joke" :id="joke.id" />
  </div>
</template>

<script>
import Joke from "@/components/Joke.vue";
import axios from "axios";

export default {
  components: {
    Joke
  },
  data() {
    return {
      joke: ""
    };
  },
  async created() {
    const config = {
      headers: {
        Accept: "application/json"
      }
    };
    try {
      const res = await axios.get(
        "https://icanhazdadjoke.com/j/" + this.$route.params.id,
        config
      );
      this.joke = res.data;
      console.log(this.joke);
    } catch (error) {
      console.log(error);
    }
  }
};
</script>

<style>
</style>