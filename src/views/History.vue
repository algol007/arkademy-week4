<template>
  <div>
    <Navbar />
    <div class="card">
  <header class="card-header">
    <p class="card-header-title">
      Borrow History
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
            <th>Title</th>
            <th>Date Borrow</th>
            <th>Action</th>
          </tr>
        </thead>
        <tbody v-for="cart in carts" :key="cart.id">
          <tr>
            <td>{{ cart.bookCart.title }}</td>
            <td>{{ cart.createdAt }}</td>
            <td>
              <button class="button is-info is-small" @click="seeDetail(cart.bookCart.id)">
                Detail</button>
              <button class="button is-danger is-small" @click="deleteCart(cart.id)"
              v-if="role=='admin'">Delete</button>
            </td>
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
      key: null,
      numbers: null,
      userId: null,
      role: null,
      name: null,
      // bookId: null,
    };
  },
  created() {
    this.items = JSON.parse(localStorage.getItem('items'));
    console.log(this.items);
    this.userId = this.items.id;
  },
  methods: {
    getUserById() {
      axios
        .get(`http://localhost:5000/api/library/user/${this.userId}`)
        .then((res) => {
          console.log(res);
          this.role = res.data.user.role;
          this.name = res.data.user.name;
          console.log(this.role);
        })
        .catch(() => {
          console.log('Error when load data!');
        });
    },
    getAllCart() {
      axios
        .get('http://localhost:5000/api/library/cart')
        .then((res) => {
          this.carts = res.data.carts.rows;
          this.numbers = res.data.carts.count;
          console.log(this.carts);
        })
        .catch(() => {
          console.log('Error when load data!');
        });
    },
    seeDetail(id) {
      console.log(id);
      this.$router.push(`/book/detail/${id}`);
    },
    deleteCart(id) {
      console.log(id);
      this.$swal.fire({
        html: 'Are you sure to delete cart?',
        icon: 'warning',
        showCancelButton: true,
        confirmButtonColor: '#3085d6',
        cancelButtonColor: '#d33',
        confirmButtonText: 'Yes',
      })
        .then((result) => {
          if (result.value) {
            axios
              .delete(`http://localhost:5000/api/library/cart/${id}`)
              .then((res) => {
                console.log(res);
                this.$swal.fire({
                  icon: 'success',
                  html: 'Cart has been deleted!',
                  showConfirmButton: false,
                  timer: 3000,
                });
                this.$router.go();
              });
          }
        });
    },
  },
  mounted() {
    this.getAllCart();
    this.getUserById();
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
