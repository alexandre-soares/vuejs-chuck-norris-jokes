<template>
  <div class="home">
    <Jokes />
  </div>
</template>

<script>
// @ is an alias to /src
import Jokes from "@/components/Jokes.vue";

export default {
  name: "Home",
  components: {
    Jokes,
  },
};
</script>

<style lang="scss" scoped>
h1 {
  text-align: center;
  font-size: 4.8rem;
  display: flex;
  justify-content: center;

  @media only screen and (max-width: $bp-medium) {
    flex-direction: column;
  }

  & img {
    margin-left: 2rem;

    @media only screen and (max-width: $bp-medium) {
      height: 7rem;
      width: 7rem;
      text-align: center;
      margin: 1rem auto;
    }
  }
}
</style>
