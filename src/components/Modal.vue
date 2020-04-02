<template>
  <div class="modal">
    <div class="modal-background"></div>
    <div class="modal-card">
      <header class="modal-card-head">
        <p class="modal-card-title">{{ modalTitle }}</p>
        <button class="delete" aria-label="close" v-on:click="showModal"></button>
      </header>
      <section class="modal-card-body">
        <Input name="Url Image"/>
        <Input name="Title"/>
        <Textarea name="Description" />
      </section>
      <footer class="modal-card-foot">
        <button class="button is-warning">Save</button>
      </footer>
    </div>
  </div>
</template>

<script>
import Input from './Input.vue';
import Textarea from './Textarea.vue';

export default {
  name: 'Modal',
  props: [
    'modalTitle',
  ],
  components: {
    Input,
    Textarea,
  },
  methods: {
    showModal() {
      const modal = document.querySelector('.modal');
      modal.classList.toggle('is-active');
    },
  },
};
</script>

<style>
  .modal{
    padding: 0 20px;
  }
  .modal-card-foot{
    display: flex;
    flex-direction: row-reverse;
  }
</style>
