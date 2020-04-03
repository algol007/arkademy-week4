<template>
  <div class="dashboard">
    <Navbar v-if="isLogin" />
    <HomeNav v-else/>
    <Slider/>
    <div class="book">
      <h1>List Book</h1>
      <div class="list-book">
        <div class="cards" v-for="book in books" :key="book.id">
          <router-link :to="'book/detail/' + book.id">
          <Card :bookTitle="book.title" :bookDesc="book.description" />
          </router-link>
        </div>
      </div>
    <Pagination class="pagination" />
    </div>
  </div>
</template>

<script>
import axios from 'axios';
import Navbar from '../components/Navbar.vue';
import Slider from '../components/Slider.vue';
import Card from '../components/Card.vue';
import Pagination from '../components/Pagination.vue';
import HomeNav from '../components/HomeNav.vue';

export default {
  name: 'Dashboard',
  components: {
    Navbar,
    Slider,
    Card,
    Pagination,
    HomeNav,
  },
  data() {
    return {
      isLogin: false,
      books: [],
    };
  },
  methods: {
    getAllBooks() {
      axios.get('http://localhost:5000/api/library/book?page=1')
        .then((res) => {
          this.books = res.data.books.rows;
          console.log(res.data.books.rows);
          console.log(this.isLogin);
        })
        .catch(() => {
          console.log('Error when load data!');
        });
    },
  },
  mounted() {
    this.getAllBooks();
  },
};
</script>

<style scoped>
  .book{
    padding: 50px 80px;
    font-size: 30px;
  }
  .list-book{
    display: flex;
    justify-content: center;
    margin-top: 30px;
    flex-wrap: wrap;
  }
  .list-book h1{
    display: block;
  }
  .pagination{
    margin-top: 50px;
  }
</style>
