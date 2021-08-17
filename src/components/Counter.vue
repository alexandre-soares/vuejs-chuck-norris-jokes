<template>
  <div v-if="counter > 0" class="counter">
    <p>A modal box is going to appear in {{ this.counter }} seconds</p>
  </div>
</template>

<script>
export default {
  name: "CounterComponent",
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
      // Decrease counter by 1 every second
      setInterval(() => {
        this.counter--;
      }, 1000);
    },
  },
};
</script>

<style></style>
