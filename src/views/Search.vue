<template>
  <div class="search">
    <input
      type="text"
      @keyup.enter="searchJoke"
      v-model="input"
      placeholder="Search for a joke..."
    />
    <p class="info-message" >Search must be between 3 and 120 characters</p>

    <div class="info" v-if="errors">
      Sorry but there are no jokes matching with your search!
    </div>

    <div class="jokes">
      <div class="joke" v-for="(joke, index) in jokes" :key="index">
        <p>{{ joke.value }}</p>
      </div>
    </div>

    <div class="loading" v-if="isLoading">
      <span></span>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "Search",
  data() {
    return {
      input: "",
      isLoading: false,
      jokes: [],
      errors: false,
    };
  },
  methods: {
    async searchJoke() {
      // Only search if input is between 3 and 120 characters
      if (this.input.length > 3 || this.input.length < 120) {
        // Start the loading screen
        this.isLoading = true;

        // Reset error message
        this.errors = null;

        // Api Call
        try {
          const response = await axios.get(
            `https://api.chucknorris.io/jokes/search?query=${this.input}`
          );
          this.jokes = response.data.result;

          // Start the loading screen
          this.isLoading = false;
        } catch (error) {
          this.jokes = [];
          this.errors = true;
          // Start the loading screen
          this.isLoading = false;
        }
      }
    },
  },
};
</script>

<style lang="scss">
.search {
  height: auto;
  width: auto;
  & input {
    display: block;
    margin: 4rem auto 1rem;
    font-size: 1.4rem;
    padding: 2rem 4rem;
    border-radius: 1.5rem;
    border: none;
    width: 50%;

    &:focus {
      outline: 3px solid orange;
      border-radius: 1.5rem;
      color: black;
    }
  }

  & .info-message {
    text-align: center;
    margin: 0 auto 2rem;
    width: 40%;
    border-radius: 1rem;
    display: block;
    font-size: 1.6rem;
    padding: 1rem 2rem;
  }

   & .info {
    text-align: center;
    background-color: #fff3cd;
    color: #735b14;
    margin: 0 auto 1rem;
    width: 40%;
    border-radius: 1rem;
    display: block;
    font-size: 1.6rem;
    padding: 1rem 2rem;
  }
}

.jokes {
  width: 70%;
  margin: 0 auto;
  display: flex;
  flex-direction: column;

  & .joke {
    margin: 2rem 0;
    border-radius: 1.5rem;
    background-color: white;
    padding: 1rem 2rem;

    & p {
      font-size: 1.4rem;
      text-transform: capitalize;
    }
  }
}

.loading {
  top: 0;
  left: 0;
  z-index: 101;
  height: 100%;
  width: 100%;
  position: absolute;
  display: flex;
  justify-content: center;
  align-items: center;
  @keyframes spin {
    to {
      transform: rotateZ(360deg);
    }
  }
  span {
    display: block;
    width: 60px;
    height: 60px;
    margin: 0 auto;
    border: 3px solid transparent;
    border-top-color: #fff;
    border-bottom-color: #fff;
    border-radius: 50%;
    animation: spin ease 1000ms infinite;
  }
}
</style>
