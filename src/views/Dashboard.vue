<template>
  <div class="dashboard">
    <!-- <Navbar v-if="isLogin" />
    <HomeNav v-else/> -->
    <nav class="columns is-gapless custom-navbar">
      <Sidebar />
      <div class="toggle-menu" @click="sidebarShow">
        <img src="../assets/img/menu.png" alt="toggle-menu">
      </div>
      <div class="column sort-book">
        <div class="dropdown satu">
          <div class="dropdown-trigger">
            <a class="button" aria-haspopup="true" aria-controls="dropdown-menu"
            @click="active1">
              <span>Sort Book</span>
              <span class="icon is-small">
                <i class="fas fa-angle-down" aria-hidden="true"></i>
              </span>
            </a>
          </div>
          <div class="dropdown-menu" id="dropdown-menu" role="menu">
            <div class="dropdown-content">
              <div class="dropdown-item" @click="getBooksByTitle">
                By Title
              </div>
              <hr class="dropdown-divider">
              <div class="dropdown-item">
                By Author
              </div>
              <hr class="dropdown-divider">
              <div class="dropdown-item">
                By Years
              </div>
            </div>
          </div>
        </div>
      </div>
      <div class="column search">
        <div class="search-box">
          <i class="fas fa-search"></i>
          <input
            class="form-control mr-sm-2"
            type="search"
            placeholder="Search..."
            aria-label="Search"/>
        </div>
      </div>
      <div class="column navbar-brand">
        <router-link to="/">
        <img src="../assets/img/bookshelf.png" alt="logo" height="40px" width="40px">
        </router-link>
        <router-link to="/" class="back-home">Library</router-link>
      </div>
    </nav>
    <Slider class="slider" />
    <div class="book">
      <h1>List Book</h1>
      <div class="list-book">
        <div class="cards" v-for="book in books" :key="book.id">
          <router-link :to="'book/detail/' + book.id">
          <Card :bookTitle="book.title" :bookDesc="book.description" :image="book.image" />
          </router-link>
        </div>
      </div>
      <ul class="pagination is-centered" role="navigation" aria-label="pagination">
        <li><button class="pagination-previous" @click="prevPages">Previous</button></li>
          <li class="pagination-gap" v-for="pag in this.totalPage" :key="pag.id">
            <div class="pagination-link" :page="pag">{{ pag }}</div>
          </li>
        <li><button class="pagination-next" @click="nextPages">Next page</button></li>
        <!-- <ul class="pagination-list" v-for="page in this.totalPage" :key="page.id"> -->
        <!-- </ul> -->
      </ul>
    </div>
  </div>
</template>

<script>
import axios from 'axios';
// import Navbar from '../components/Navbar.vue';
import Slider from '../components/Slider.vue';
import Card from '../components/Card.vue';
import Sidebar from '../components/Sidebar.vue';
// import Pagination from '../components/Pagination.vue';
// import HomeNav from '../components/HomeNav.vue';

export default {
  name: 'Dashboard',
  components: {
    // Navbar,
    Slider,
    Card,
    Sidebar,
    // Pagination,
    // HomeNav,
  },
  data() {
    return {
      isLogin: true,
      books: [],
      page: 2,
      totalPage: 5,
    };
  },
  methods: {
    sidebarShow() {
      const sidebar = document.querySelector('.sidebar');
      sidebar.classList.toggle('show-sidebar');
      console.log('Navbar');
    },
    active1() {
      const dropdown1 = document.querySelector('.satu');
      dropdown1.classList.toggle('is-active');
    },
    getAllBooks() {
      // const limit = 8;
      console.log(localStorage.getItem('login'));
      axios
        .get(`http://localhost:5000/api/library/book?page=${this.page}`)
        // .get('http://localhost:5000/api/library/book?page=2')
        .then((res) => {
          // this.totalPage = Math.ceil(res.data.books.count / limit);
          this.books = res.data.books.rows;
          console.log(res.data.books.rows);
          console.log(this.isLogin);
          console.log(this.book.image);
        })
        .catch(() => {
          console.log('Error when load data!');
        });
    },
    getBooksByTitle() {
      axios
        .get('http://localhost:5000/api/library/book?page=1&title=ASC')
        // .get('http://localhost:5000/api/library/book?page=2')
        .then((res) => {
          // this.totalPage = Math.ceil(res.data.books.count / limit);
          this.books = res.data.books.rows;
          console.log(res.data.books.rows);
        })
        .catch(() => {
          console.log('Error when load data!');
        });
    },
    nextPages() {
      if (this.page === this.totalPage) {
        this.page = this.totalPage;
        console.log(this.page);
      } else {
        this.page += 1;
        console.log(this.page);
      }
    },
    prevPages() {
      if (this.page === 1) {
        this.page = 1;
        console.log(this.page);
      } else {
        this.page -= 1;
        console.log(this.page);
      }
    },
  },
  beforeMount() {
    this.getAllBooks();
  },
  // updated() {
  //   this.getBooksByTitle();
  // },
};
</script>

<style scoped>
  .book{
    transition: 0.5s;
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
    display: flex;
    justify-content: center;
  }
  .pagination-link, .pagination-next, .pagination-previous{
    cursor: pointer;
  }
  .pagination-next, .pagination-previous{
    margin: 0 20px;
  }
  .custom-navbar{
    background-color: #ffffff;
    z-index: 2;
    position: fixed;
    width: 100%;
    align-items: center;
    box-shadow: 3px 2px 20px rgba(0, 0, 0, 0.2);
    margin: 0;
    padding: 5px 0 !important;
    display: flex;
  }
  .column{
    padding: 0 !important;
  }
  .custom-navbar .toggle-menu{
    margin: 0 30px;
  }
  .toggle-menu{
    cursor: pointer;
    width: 40px;
  }
  .column{
    display: flex;
    flex-direction: row;
  }
  .sort-book{
    display: flex;
    justify-content: center;
  }
  .button span{
    font-size: 14px;
  }
  .button{
    border: none;
  }
  .search-box {
    width: 100%;
    display: flex;
    flex-direction: row;
    padding: 10px 20px;
    border-radius: 20px;
    border: 1px solid #ced4da;
    transition: 1s;
  }
  .search-box input{
    width: 100%;
    margin-left: 10px;
    border: none;
    outline: none;
  }
  .navbar-brand{
    display: flex;
    align-items: center;
    justify-content: center;
  }
  .navbar-brand img{
    margin-right: 10px;
  }
  .navbar-brand .back-home{
    color: #424242;
  }
  .dropdown-item{
    cursor: pointer;
  }
  @media (max-width: 768px) {
    .sort-book {
      display: none;
    }
    .book {
      padding: 50px 30px;
    }
  }
  @media (max-width: 450px) {
    .search-box {
      display: none;
    }
  }
</style>
