<template>
  <nav class="columns is-gapless custom-navbar">
    <Sidebar class="sidebar-start" />
    <div class="toggle-menu" v-on:click="sidebarShow">
      <img src="../assets/img/menu.png" alt="toggle-menu">
    </div>
    <div class="column sort-book">
      <div class="dropdown satu">
        <div class="dropdown-trigger">
          <a class="button" aria-haspopup="true" aria-controls="dropdown-menu" v-on:click="active1">
            <span>Sort Book</span>
            <span class="icon is-small">
              <i class="fas fa-angle-down" aria-hidden="true"></i>
            </span>
          </a>
        </div>
        <div class="dropdown-menu" id="dropdown-menu" role="menu">
          <div class="dropdown-content">
            <div class="dropdown-item">
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
</template>

<script>
import Sidebar from './Sidebar.vue';
// import Dropdown from './Dropdown.vue';

export default {
  name: 'Navbar',
  components: {
    Sidebar,
    // Dropdown,
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
    active2() {
      const dropdown2 = document.querySelector('.dua');
      dropdown2.classList.toggle('is-active');
    },
  },
};
</script>

<style scoped>
  .custom-navbar{
    max-width: 100%;
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
  }
  @media (max-width: 450px) {
    .search-box {
      display: none;
    }
  }
</style>
