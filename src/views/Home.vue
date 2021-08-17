<template>
  <div class="home">
    <h1>
      Chuck Norris Jokes App
      <img
        src="https://assets.chucknorris.host/img/avatar/chuck-norris.png"
        alt="logo"
      />
    </h1>

    <Modal />
    <Jokes />
  </div>
</template>

<script>
// @ is an alias to /src
import Jokes from "@/components/Jokes.vue";
import Modal from "@/components/Modal.vue";

export default {
  name: "Home",
  components: {
    Jokes,
    Modal,
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
