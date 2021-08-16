<template>
  <div class="jokes">
    <h1>{{ this.joke }}</h1>
    <button class="btn" @click="getRandomJoke">Get Random Joke</button>
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "Jokes",
  data() {
    return {
      joke: "",
    };
  },
  mounted() {
    this.getRandomJoke();
  },
  methods: {
    async getRandomJoke() {
      try {
        const response = await axios.get(
          "https://api.chucknorris.io/jokes/random"
        );
        this.joke = response.data.value;
        console.log(response);
      } catch (error) {
        console.error(error);
      }
    },
  },
};
</script>

<style lang="scss" scoped>
.jokes {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  width: 80%;
  margin: 0 auto;

  & h1 {
      text-align: center;
  }
}

</style>
