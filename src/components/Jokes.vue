<template>
  <Loading v-if="isLoading" />
  <div class="jokes">
    <h1>Chuck Norris Jokes App</h1>
    <h2>{{ this.joke }}</h2>
    <button class="btn" @click="getRandomJoke">Get Random Joke</button>
  </div>
</template>

<script>
import Loading from "../components/Loading.vue";
import axios from "axios";
export default {
  name: "Jokes",
  components: {
    Loading,
  },
  data() {
    return {
      joke: "",
      isLoading: false,
    };
  },
  mounted() {
    this.getRandomJoke();
  },
  methods: {
    async getRandomJoke() {
      this.isLoading = true;
      try {
        const response = await axios.get(
          "https://api.chucknorris.io/jokes/random"
        );
        this.joke = response.data.value;
        this.isLoading = false;
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
  justify-content: space-around;
  width: 80%;
  height: 60vh;
  margin: 0 auto;

  & h1 {
    text-align: center;
  }

  & h2 {
    text-align: center;
  }
}
</style>
