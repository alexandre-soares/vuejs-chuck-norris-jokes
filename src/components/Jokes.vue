<template>
  <Loading v-if="isLoading" />
  <div class="jokes">
    <h2>{{ this.joke.text }}</h2>
    <p>Rate this joke</p>
    <div class="buttons">
      <button @click="rateJoke('bad')">😩</button>
      <button @click="rateJoke('medium')">🤨</button>
      <button @click="rateJoke('good')">😂</button>
    </div>
    <button class="btn" @click="getRandomJoke">Get Another Joke</button>
    <div class="notifications">
      <p
        v-for="(notification, index) in notifications"
        :key="index"
        :class="notification.rating"
        @click="removeNotification(index)"
      >
        {{ notification.text }}
      </p>
    </div>
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
      joke: {
        id: null,
        text: null,
      },
      isLoading: false,
      notifications: [],
    };
  },
  mounted() {
    // Load the component with a joke when the page appears
    this.getRandomJoke();

    // Remove the first notification of the array (the oldest one) every 10 seconds
    setInterval(() => {
      this.autoRemoveNotification();
    }, 10000);
  },
  methods: {
    async getRandomJoke() {
      // Start the loading screen
      this.isLoading = true;

      // Api Call
      try {
        const response = await axios.get(
          "https://api.chucknorris.io/jokes/random"
        );

        // Show the joke
        this.joke.id = response.data.id;
        this.joke.text = response.data.value;

        // Stop the loading screen
        this.isLoading = false;
      } catch (error) {
        console.error(error);
      }
    },
    rateJoke(value) {
      // Push the notification object on the notifications array
      if (value === "bad") {
        this.notifications.push({
          id: this.joke.id,
          text: `You didn't like the joke: ${this.joke.text}!`,
          rating: "bad",
        });
      }

      if (value === "medium") {
        this.notifications.push({
          id: this.joke.id,
          text: `The joke "${this.joke.text}" didn't impress you!`,
          rating: "medium",
        });
      }

      if (value === "good") {
        this.notifications.push({
          id: this.joke.id,
          text: `You liked the joke: ${this.joke.text}`,
          rating: "good",
        });
      }

      // Api Call for another joke
      this.getRandomJoke();
    },
    autoRemoveNotification() {
      // Remove the oldest notification only if there is at least one
      if (this.notifications.length > 0) {
        this.notifications.shift();
      }
    },
    removeNotification(index) {
      this.notifications.splice(index, 1);
    },
  },
};
</script>

<style lang="scss" scoped>
.jokes {
  display: flex;
  flex-direction: column;
  align-items: center;
  width: 80%;
  margin: 0 auto 4rem;
  background-color: white;
  padding: 3rem 4rem;
  margin-top: 5rem;
  border-radius: 1.5rem;

  & h2 {
    font-size: 2rem;
    line-height: 1.6;
    text-align: center;
  }
}

.buttons {
  display: flex;
  align-items: center;
  justify-content: space-between;

  & button {
    font-size: 6rem;
    padding: 1.5rem;
    background-color: transparent;
    border: none;
    cursor: pointer;
    transition: all 0.5s ease-in-out;
    margin: 0.5rem;

    &:nth-child(2) {
      margin-top: 5rem;
    }

    @media only screen and (max-width: $bp-medium) {
      font-size: 4rem;
    }

    &:hover {
      background-color: rgba(141, 141, 141, 0.493);
    }
  }
}

.notifications {
  position: absolute;
  bottom: 1rem;
  right: 1rem;

  p {
    padding: 2rem 3rem;
    text-align: right;
    margin: 2rem;
    border-radius: 1.5rem;
    font-size: 1.4rem;
    cursor: pointer;
  }

  & .bad {
    background-color: #f8d7da;
    color: #842029;
  }

  & .medium {
    background-color: #fff3cd;
    color: #735b14;
  }

  & .good {
    color: #0f5132;
    background-color: #d1e7dd;
  }
}

.btn {
  height: 5rem;
}
</style>
