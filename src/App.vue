<template>
  <router-view />
  <Counter />
</template>

<script>
import Counter from "./components/Counter.vue";
export default {
  name: "App",
  components: {
    Counter,
  },
};
</script>

<style lang="scss">
// Breakpoints

$bp-largest: 75em; // 1200px
$bp-large: 68.75em; // 1100px
$bp-medium: 56.25em; // 900px
$bp-small: 37.5em; // 600px
$bp-smallest: 31.25em; // 500px

* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
  font-family: "Poppins", sans-serif;
}

html {
  font-size: 62.5%; // 1rem = 10px
  overflow-x: hidden;

  @media only screen and (max-width: $bp-large) {
    font-size: 60%;
  }
}

body {
  background-color: #fbab7e;
  background-image: linear-gradient(62deg, #fbab7e 0%, #f7ce68 100%);
  width: 100vw;
  height: 100vh;
  display: flex;
  flex-direction: column;
  justify-content: space-around;
  align-items: center;
}

.btn {
  padding: 1rem 2rem;
  border-radius: 0.5rem;
  border: none;
  cursor: pointer;
  transition: all 0.3s ease-in-out;
  margin: 2rem;

  &:hover {
    color: white;
    background-color: darkgray;
  }

  &:active {
    transform: translateY(.5rem);
  }
}

p {
  font-size: 1.6rem;
  margin: 2rem;
  line-height: 1.6;
}
</style>
