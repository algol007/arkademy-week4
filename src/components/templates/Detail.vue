<template>
  <section>
    <div class="detail-nav">
      <div class="nav-back">
        <router-link to="/"><div class="back"></div></router-link>
      </div>
      <div class="nav-option">
        <button v-on:click="showModal">Edit</button>
        <button v-on:click="successInfo">Delete</button>
      </div>
    </div>
    <div class="detail-cover"></div>
    <div class="detail-book"></div>
    <Modal modalTitle="Edit Book"/>
  </section>
</template>

<script>
import Modal from '../Modal.vue';

export default {
  name: 'Detail',
  components: {
    Modal,
  },
  methods: {
    showModal() {
      const modal = document.querySelector('.modal');
      modal.classList.toggle('is-active');
    },
    successInfo() {
      this.$swal.fire({
        icon: 'success',
        html: 'Data <b>Dilan 1990</b> berhasil dihapus!',
        showConfirmButton: false,
        timer: 3000,
      });
    },
  },
};
</script>

<style>
  .detail-nav{
    width: 100%;
    padding: 10px 20px;
    position: absolute;
    display: flex;
    align-items: center;
    justify-content: space-between;
  }
  .back{
    height: 40px;
    width: 40px;
    background-color: white;
    background-image: url('../../assets/img/Arrow.png');
    background-position: center center;
    background-repeat: no-repeat;
    border-radius: 50%;
    cursor: pointer;
  }
  .nav-option button{
    padding: 0 10px;
    background: none;
    border: none;
    font-size: 16px;
    color: #ffffff;
    cursor: pointer;
    outline: none;
  }
  .detail-cover{
    width: 100%;
    height: 400px;
    background-color: #424242;
    z-index: -1;
  }
  .detail-book{
    width: 230px;
    height: 320px;
    background-color: salmon;
    position: absolute;
    top: 250px;
    right: 50px;
  }
</style>
