<template>
  <div class="modal" v-if="modalOpen">
    <div class="modal__box">
      <h1>Did you like it?</h1>
      <span class="modal__close" @click="closeModal">x</span>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      modalOpen: false,
    };
  },
  mounted() {
    setTimeout(() => {
      this.openModal();
    }, 25000);
  },
  methods: {
    openModal() {
      this.modalOpen = true;
    },
    closeModal() {
      this.modalOpen = !this.modalOpen;
    },
  },
};
</script>

<style lang="scss" scoped>
.modal {
  position: absolute;
  top: 0;
  left: 0;
  height: 100vh;
  width: 100vw;
  z-index: 9999;
  background-color: rgba(0, 0, 0, 0.479);
  display: flex;
  justify-content: center;
  align-items: center;

  &__box {
    position: relative;
    background-color: white;
    height: 40%;
    width: 70%;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
  }

  &__close {
    position: absolute;
    font-size: 3rem;
    top: 1rem;
    right: 2rem;
    cursor: pointer;
  }
}
</style>
