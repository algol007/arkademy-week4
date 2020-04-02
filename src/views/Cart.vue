<template>
  <div class="cart">
    <h1>Cart Page</h1>
    <button class="button is-primary trigger" v-on:click="showModal">Primary</button>
    <Modal />
  </div>
</template>

<script>
import Modal from '../components/Modal.vue';

export default {
  name: 'Cart',
  components: {
    Modal,
  },
  methods: {
    showModal() {
      const modal = document.querySelector('.modal');
      modal.classList.toggle('is-active');
    },
  },
};
</script>

<style></style>
