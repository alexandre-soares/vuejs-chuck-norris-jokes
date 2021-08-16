<template>
  <div v-if="counter > 0" class="counter">{{ this.counter }}</div>
</template>

<script>
export default {
  name: "Counter",
  data() {
    return {
      counter: 25,
    };
  },
  mounted() {
    this.counterFrom25To0();
  },
  methods: {
    counterFrom25To0() {
      setInterval(() => {
        this.counter--;
      }, 1000);
    },
  },
};
</script>

<style></style>
