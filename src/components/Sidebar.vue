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
        src="../assets/img/niki.png"
        alt="Cewe Cantik"
      />
      <h4>Niki Zefanya</h4>
    </div>
    <!-- User Profile -->
    <!-- Sidebar Menu -->
    <div class="sidebar-menu">
      <p>Explore</p>
      <p>History</p>
      <p data-toggle="modal" v-on:click="showModal">Add Book*</p>
      <p><router-link to="/auth/login">Logout</router-link></p>
    </div>
    <!-- Sidebar Menu -->
    <Modal modalTitle="Add Book" />
  </section>
</template>

<script>
import Modal from './Modal.vue';

export default {
  name: 'Sidebar',
  components: {
    Modal,
  },
  methods: {
    sidebarHide() {
      const sidebar = document.querySelector('.sidebar');
      sidebar.classList.toggle('show-sidebar');
      console.log('Sidebar');
    },
    showModal() {
      const modal = document.querySelector('.modal');
      modal.classList.toggle('is-active');
    },
  },
};
</script>
<style>
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
    padding: 50px;
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
    margin: 10px 0 50px;
  }

  .profile img {
    width: 150px;
    height: 150px;
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

  .sidebar-menu > p {
    color: #000000;
    cursor: pointer;
    font-size: 1em;
    margin: 1em 0;
    display: flex;
    flex-direction: column;
    transition: 0.5s;
  }

  .sidebar-menu > p:hover {
    color: #424242;
    transition: 0.5s;
  }
</style>
