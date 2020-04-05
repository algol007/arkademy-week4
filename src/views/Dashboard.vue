<template>
  <div class="dashboard">
    <!-- <Navbar v-if="isLogin" /> -->
    <HomeNav v-if="!isLogin"/>
    <nav class="columns is-gapless custom-navbar" v-else>
      <Sidebar :name="this.name" />
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
              <div class="dropdown-item" @click="getBooksByAuthor">
                By Author
              </div>
            </div>
          </div>
        </div>
        <div class="dropdown dua">
          <div class="dropdown-trigger">
            <a class="button" aria-haspopup="true" aria-controls="dropdown-menu"
            @click="active2">
              <span>All Time</span>
              <span class="icon is-small">
                <i class="fas fa-angle-down" aria-hidden="true"></i>
              </span>
            </a>
          </div>
          <div class="dropdown-menu" id="dropdown-menu" role="menu">
            <div class="dropdown-content">
              <div class="dropdown-item" @click="getBooksByYear2">
                Newest
              </div>
              <hr class="dropdown-divider">
              <div class="dropdown-item" @click="getBooksByYear">
                Latest
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
            aria-label="Search"
            v-model="search"
            @change="searchBooks"/>
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
          <Card :bookTitle="book.title" :bookAuthor="book.author" :image="book.image"
          :year="book.publishedAt" />
          </router-link>
        </div>
      </div>
      <ul class="pagination is-centered" role="navigation" aria-label="pagination">
        <li><button class="pagination-previous" @click="prevPages">Previous</button></li>
          <li class="pagination-gap" v-for="page in this.totalPage" :key="page.id"
          @click="pages(page)">
            <div class="pagination-link" v>{{ page }}</div>
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
import HomeNav from '../components/HomeNav.vue';

export default {
  name: 'Dashboard',
  components: {
    // Navbar,
    Slider,
    Card,
    Sidebar,
    // Pagination,
    HomeNav,
  },
  data() {
    return {
      items: [],
      isLogin: false,
      books: [],
      currentPage: 1,
      totalPage: [],
      offset: null,
      limit: 8,
      sort: null,
      search: null,
      name: null,
      // role: null,
      url: 'http://localhost:5000/api/library/book?page=',
    };
  },
  created() {
    this.items = JSON.parse(localStorage.getItem('items'));
    console.log(this.items);
    this.isLogin = this.items.isLogin;
  },
  methods: {
    pages(id) {
      // const active = document.querySelector('.pagination-link');
      // if (this.currentPage === id) {
      //   active.classList.add('is-current');
      // }
      this.currentPage = 0 + id;
      axios
        .get(this.url + this.currentPage)
        // .get('http://localhost:5000/api/library/book?page=2')
        .then((res) => {
          this.totalPage = Math.ceil(res.data.books.count / this.limit);
          this.books = res.data.books.rows;
          console.log(res.data.books.rows);
          console.log(this.books.length);
          // console.log(this.currentPage);
        })
        .catch(() => {
          console.log('Error when load data!');
        });
    },
    sidebarShow() {
      const sidebar = document.querySelector('.sidebar');
      sidebar.classList.toggle('show-sidebar');
      console.log('Navbar');
    },
    active1() {
      const dropdown1 = document.querySelector('.satu');
      dropdown1.classList.toggle('is-active');
    },
    active2() {
      const dropdown2 = document.querySelector('.dua');
      dropdown2.classList.toggle('is-active');
      console.log(this.sort);
    },
    getAllBooks() {
      // this.url = `http://localhost:5000/api/library/book?page=${this.currentPage}`;
      // console.log(this.url);
      axios
        .get(this.url + this.currentPage)
        // .get('http://localhost:5000/api/library/book?page=2')
        .then((res) => {
          this.totalPage = Math.ceil(res.data.books.count / this.limit);
          this.books = res.data.books.rows;
          console.log(res.data.books.rows);
          console.log(this.books.length);
          // console.log(this.currentPage);
        })
        .catch(() => {
          console.log('Error when load data!');
        });
    },
    getBooksByTitle() {
      const title = '&title=ASC';
      axios
        .get(this.url + this.currentPage + title)
        .then((res) => {
          this.books = res.data.books.rows;
          // console.log(res.data.books.rows);
        })
        .catch(() => {
          console.log('Error when load data!');
        });
    },
    getBooksByAuthor() {
      axios
        .get('http://localhost:5000/api/library/book?page=1&author=ASC')
        .then((res) => {
          this.books = res.data.books.rows;
          console.log(res.data.books.rows);
        })
        .catch(() => {
          console.log('Error when load data!');
        });
    },
    getBooksByYear() {
      axios
        .get('http://localhost:5000/api/library/book?page=1&year=ASC')
        .then((res) => {
          this.books = res.data.books.rows;
          console.log(res.data.books.rows);
        })
        .catch(() => {
          console.log('Error when load data!');
        });
    },
    getBooksByYear2() {
      axios
        .get('http://localhost:5000/api/library/book?page=1&year=DESC')
        .then((res) => {
          this.books = res.data.books.rows;
          console.log(res.data.books.rows);
        })
        .catch(() => {
          console.log('Error when load data!');
        });
    },
    searchBooks() {
      axios
        .get(`http://localhost:5000/api/library/book?search=${this.search}`)
        .then((res) => {
          this.books = res.data.books.rows;
          console.log(res.data.books.rows);
          const slider = document.querySelector('.slider');
          slider.style.display = 'none';
        })
        .catch(() => {
          console.log('Error when load data!');
        });
    },
    nextPages() {
      if (this.currentPage === this.totalPage) {
        this.currentPage = this.totalPage;
      } else {
        this.currentPage += 1;
      }
      this.getAllBooks();
    },
    prevPages() {
      if (this.currentPage === 1) {
        this.currentPage = 1;
      } else {
        this.currentPage -= 1;
      }
      this.getAllBooks();
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
  }
  .book h1{
    transition: 0.5s;
    font-size: 2em;
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
    .book h1{
      font-size: 1.5em;
    }
  }
  @media (max-width: 450px) {
    .search-box {
      display: none;
    }
  }
</style>
