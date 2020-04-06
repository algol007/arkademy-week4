<template>
  <div class="cart">
    <HomeNav />
    <h1>Cart Page</h1>
    <button class="button is-primary trigger" v-on:click="showModal">Primary</button>
    <Modal />
    <h4>List Book</h4>
    <ul v-for="book in books" :key="book.id">
      <li>{{ book.title }}</li>
    </ul>
    <input type="text" v-model="email">
    <FormLogin @change="mInput" />
  </div>
</template>

<script>
import axios from 'axios';
import Modal from '../components/Modal.vue';
import HomeNav from '../components/HomeNav.vue';
import FormLogin from '../components/FormLogin.vue';

export default {
  name: 'Cart',
  components: {
    Modal,
    HomeNav,
    FormLogin,
  },
  data() {
    return {
      email: null,
      books: [],
    };
  },
  methods: {
    mInput() {
      // console.log(this.email);
    },
    showModal() {
      const modal = document.querySelector('.modal');
      modal.classList.toggle('is-active');
    },
    getAllBooks() {
      axios.get('http://localhost:5000/api/library/book')
        .then((res) => {
          this.books = res.data.books.rows;
          // console.log(res.data.books.rows);
        })
        .catch(() => {
          // console.log('Error when load data!');
        });
    },
  },
  mounted() {
    this.getAllBooks();
  },
};
</script>

<style></style>
