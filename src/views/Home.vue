<template>
  <Modal />
  <Jokes />
  <Counter />
</template>

<script>
// @ is an alias to /src
import Jokes from "@/components/Jokes.vue";
import Modal from "@/components/Modal.vue";
import Counter from "@/components/Counter.vue";

export default {
  name: "Home",
  components: {
    Jokes,
    Modal,
    Counter,
  },
};
</script>
