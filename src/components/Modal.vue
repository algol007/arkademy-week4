<template>
  <div class="modal">
    <div class="modal-background"></div>
    <div class="modal-card">
      <header class="modal-card-head">
        <p class="modal-card-title">{{ modalTitle }}</p>
        <button class="delete" aria-label="close" v-on:click="showModal"></button>
      </header>
      <section class="modal-card-body">
        <Input name="Title" :value="book.title"/>
        <Input name="Url Image" :value="book.image"/>
        <Input name="Author" :value="book.author"/>
        <Input name="ISBN" :value="book.isbn"/>
        <Input name="Total Page" :value="book.totalPage"/>
        <Input name="Category" :value="book.categoryId"/>
        <Input name="Price" :value="book.price"/>
        <Input name="Language" :value="book.language"/>
        <Input name="Penerbit" :value="book.publishedBy"/>
        <Input name="Tahun Terbit" :value="book.publishedAt"/>
        <Textarea name="Description" :value="book.description"/>
      </section>
      <footer class="modal-card-foot">
        <button class="button is-warning button-save" :v-on:click="addBook">Save</button>
      </footer>
    </div>
  </div>
</template>

<script>
import axios from 'axios';
import Input from './Input.vue';
import Textarea from './Textarea.vue';

export default {
  name: 'Modal',
  props: [
    'modalTitle',
    'save',
  ],
  components: {
    Input,
    Textarea,
  },
  data() {
    return {
      book: [],
      title: null,
    };
  },
  methods: {
    showModal() {
      const modal = document.querySelector('.modal');
      modal.classList.toggle('is-active');
    },
    getBookById() {
      axios.get(`http://localhost:5000/api/library/book/${this.$route.params.id}`)
        .then((res) => {
          this.book = res.data.book;
          // console.log(res.data.book);
          // console.log(${this.$route.params.id});
        })
        .catch(() => {
          // console.log('Error when load data!');
        });
    },
    addBook() {
      // console.log('Hello');
    },
  },
  mounted() {
    this.getBookById();
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
