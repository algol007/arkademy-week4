<template>
  <section class="sidebar">
    <!-- Toggle Button -->
    <div class="menu-button">
      <button class="sidebar-button" v-on:click="sidebarHide">
        <img src="../assets/img/menu.png" alt="toggle-menu" />
      </button>
    </div>
    <!-- Toggle Button -->
    <!-- User Profile -->
    <div class="profile">
      <img
        src="../assets/img/default-user.jpg"
        alt="Cewe Cantik"
      />
      <h4>{{ name }}</h4>
    </div>
    <!-- User Profile -->
    <!-- Sidebar Menu -->
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
    <div class="sidebar-menu">
      <p>Explore</p>
      <p><router-link to="/history" class="menu-list">History</router-link></p>
      <p data-toggle="modal" @click="showModal" v-if="this.role == 'admin'">Add Book*</p>
      <p class="none" v-else>Add Book*</p>
      <p @click="logout">Logout</p>
    </div>
    <!-- Sidebar Menu -->
    <div class="modal">
      <div class="modal-background"></div>
      <div class="modal-card">
        <header class="modal-card-head">
          <p class="modal-card-title">Add Book</p>
          <button class="delete" aria-label="close" @click="showModal"></button>
        </header>
        <section class="modal-card-body">
          <div class="form-login">
            <label for="title">Title</label>
            <input name="Title" id="title" placeholder="Title" v-model="title"/>
          </div>
          <div class="form-login">
            <label for="image">Image</label>
            <input name="image" id="image" placeholder="Image" v-model="image"/>
          </div>
          <div class="form-login">
            <label for="author">Author</label>
            <input name="author" id="author" placeholder="Author" v-model="author"/>
          </div>
          <div class="form-login">
            <label for="isbn">ISBN</label>
            <input name="isbn" id="isbn" placeholder="ISBN" v-model="isbn"/>
          </div>
          <div class="form-login">
            <label for="totalPage">Total Page</label>
            <input name="totalPage" id="totalPage" placeholder="Total Page" v-model="totalPage"/>
          </div>
          <div class="form-login">
            <label for="categoryId">Category</label>
            <input name="categoryId" id="categoryId" placeholder="Category" v-model="categoryId"/>
          </div>
          <div class="form-login">
            <label for="price">Price</label>
            <input name="price" id="price" placeholder="Price" v-model="price"/>
          </div>
          <div class="form-login">
            <label for="language">Language</label>
            <input name="language" id="language" placeholder="Language" v-model="language"/>
          </div>
          <div class="form-login">
            <label for="publishedBy">Publisher</label>
            <input name="publishedBy" id="publishedBy" placeholder="Publisher"
            v-model="publishedBy"/>
          </div>
          <div class="form-login">
            <label for="publishedAt">Published On</label>
            <input name="publishedAt" id="publishedAt" placeholder="Published On"
            v-model="publishedAt"/>
          </div>
          <div class="form-login">
            <label for="description">Description</label>
            <textarea name="description" id="description" placeholder="Description"
            v-model="description"
            rows="5"/>
          </div>
        </section>
        <footer class="modal-card-foot">
          <button class="button is-warning button-save" @click="addBook">Save</button>
        </footer>
      </div>
    </div>

  </section>
</template>

<script>
import axios from 'axios';
// import Modal from './Modal.vue';

export default {
  name: 'Sidebar',
  components: {
    // Modal,
  },
  data() {
    return {
      title: null,
      image: null,
      author: null,
      isbn: null,
      totalPage: null,
      categoryId: null,
      price: null,
      description: null,
      language: null,
      publishedBy: null,
      publishedAt: null,
      name: null,
      role: null,
      items: [],
    };
  },
  created() {
    this.items = JSON.parse(localStorage.getItem('items'));
    // console.log(this.items);
  },
  mounted() {
    this.getUserById();
  },
  methods: {
    logout() {
      localStorage.removeItem('items');
      this.$router.push('/auth/login');
    },
    sidebarHide() {
      const sidebar = document.querySelector('.sidebar');
      sidebar.classList.toggle('show-sidebar');
      console.log('Sidebar');
    },
    getUserById() {
      axios
        .get(`http://localhost:5000/api/library/user/${this.items.id}`)
        .then((res) => {
          console.log(res);
          this.name = res.data.user.name;
          this.role = res.data.user.role;
          // console.log(res.data.user.name);
        })
        .catch(() => {
          console.log('Error when load data!');
        });
    },
    addBook() {
      axios
        .post('http://localhost:5000/api/library/admin/book', {
          title: this.title,
          image: this.image,
          author: this.author,
          isbn: this.isbn,
          totalPage: this.totalPage,
          categoryId: this.categoryId,
          price: this.price,
          description: this.description,
          language: this.language,
          publishedBy: this.publishedBy,
          publishedAt: this.publishedAt,
        })
        .then((res) => {
          console.log(res);
          this.$router.go();
          this.$swal.fire({
            icon: 'success',
            html: `Book ${this.title} has been created!`,
            showConfirmButton: false,
            timer: 3000,
          });
          const modal = document.querySelector('.modal');
          const sidebar = document.querySelector('.sidebar');
          modal.classList.toggle('is-active');
          sidebar.classList.toggle('show-sidebar');
        })
        .catch((err) => {
          console.log(err);
        });
    },
    showModal() {
      const modal = document.querySelector('.modal');
      modal.classList.toggle('is-active');
    },
  },
};
</script>
<style>
  .none{
    display: none !important;
  }
  .sidebar-button{
    border: none;
    cursor: pointer;
  }
  .sidebar {
    top: 0;
    left: 0;
    bottom: 0;
    width: 300px;
    min-height: 900px;
    height: 100vh;
    background: #ffffff;
    text-align: center;
    padding: 50px 0;
    position: fixed;
    /* display: none; */
    transition: 1s;
    z-index: 2;
    margin-left: -300px;
    box-shadow: none;
  }
  .show-sidebar {
    margin-left: 0px;
    box-shadow: 3px 2px 20px #999999;
    transition: 1s;
  }
  .sidebar .menu-button {
    text-align: right;
    position: absolute;
    top: 20px;
    left: 240px;
  }
  .menu-button button {
    background: none;
  }
  .sidebar .profile {
    margin: 10px 0;
  }
  .profile img {
    width: 150px;
    height: 150px;
    border-radius: 50%;
  }
  .profile h4 {
    font-size: 20px;
    font-weight: bold;
    margin-top: 1em;
  }
  .sidebar .sidebar-menu {
    text-align: left;
    margin-top: 20px;
  }
  .sidebar-menu{
    padding: 0 30px;
  }
  .sidebar-menu p{
    margin: 1em 0;
  }
  .sidebar-menu p, .menu-list {
    color: #000000 !important;
    cursor: pointer;
    font-size: 1em;
    display: flex;
    flex-direction: column;
    transition: 0.5s;
  }
  .sidebar-menu p:hover, .menu-list {
    color: #424242;
    transition: 0.5s;
  }
  .search-box {
    width: 100%;
    flex-direction: row;
    padding: 10px 20px;
    border-radius: 20px;
    border: 1px solid #ced4da;
    display: none;
  }
  .search-box input{
    width: 100%;
    margin-left: 10px;
    border: none;
    outline: none;
  }
  @media (max-width: 450px) {
    .search-box {
      display: flex;
    }
  }
</style>
