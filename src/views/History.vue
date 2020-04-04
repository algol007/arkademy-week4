<template>
  <div>
    <Navbar />
    <div class="card">
  <header class="card-header">
    <p class="card-header-title">
      History Transaction
    </p>
    <a href="#" class="card-header-icon" aria-label="more options">
      <span class="icon">
        <i class="fas fa-angle-down" aria-hidden="true"></i>
      </span>
    </a>
  </header>
  <div class="card-content">
    <div class="content">
      <table class="table is-hoverable">
        <thead>
          <tr>
            <th>ID Cart</th>
            <th>Title</th>
            <th>Date Borrow</th>
            <th>Action</th>
          </tr>
        </thead>
        <tbody v-for="cart in carts" :key="cart.id">
          <tr>
            <td>{{ cart.id }}</td>
            <td>{{ cart.bookCart.title }}</td>
            <td>{{ cart.createdAt }}</td>
            <td><button class="button is-info is-small" @click="seeDetail">Detail</button></td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</div>
  </div>
</template>

<script>
import axios from 'axios';
import Navbar from '../components/Navbar.vue';

export default {
  name: 'History',
  components: {
    Navbar,
  },
  data() {
    return {
      carts: [],
      // bookId: null,
    };
  },
  methods: {
    getAllCart() {
      axios
        .get('http://localhost:5000/api/library/cart')
        .then((res) => {
          this.carts = res.data.carts;
          console.log(this.carts);
        })
        .catch(() => {
          console.log('Error when load data!');
        });
    },
    seeDetail() {
      const book = this.carts;
      console.log(book.bookId);
      // axios
      //   .get(`http://localhost:5000/api/library/book/${book}`)
      //   .then((res) => {
      //     this.book = res.data.book;
      //     console.log(res);
      //   })
      //   .catch(() => {
      //     console.log('Error when load data!');
      //   });
    },
  },
  mounted() {
    this.getAllCart();
  },
  computed: {
    img() {
      return {
        // 'background-image': `url(${this.carts.bookCart.image})`,
      };
    },
  },
};
</script>
<style scoped>
  .book-image{
    width: 80px;
    height: 100px;
    background-color: teal;
  }
  .card{
    margin: 0 10px;
  }
  button{
    margin: 0 5px;
  }
  .lists{
    margin-top: 50px;
  }
</style>
