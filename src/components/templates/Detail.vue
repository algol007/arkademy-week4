<template>
  <section>
    <div class="detail-nav">
      <div class="nav-back">
        <router-link to="/"><div class="back"></div></router-link>
      </div>
      <div class="nav-option">
        <button v-on:click="showModal">Edit</button>
        <button v-on:click="deleteBook">Delete</button>
      </div>
    </div>
    <div class="detail-cover" style="backgroundImage:" :url="image"></div>
    <div class="detail-book" style="backgroundImage: url('https://www.grobmart.com/image/cache/catalog/0produk0/201904/komet%20minor-550x550h.jpg')"></div>
    <!-- <Modal modalTitle="Edit Book" save="addBook"/> -->
  </section>
</template>

<script>
import axios from 'axios';
// import Modal from '../Modal.vue';

export default {
  name: 'Detail',
  components: {
    // Modal,
  },
  props: [
    'image',
  ],
  methods: {
    deleteBook() {
      axios
        .delete(`http://localhost:5000/api/library/admin/book/${this.$route.params.id}`)
        .then((res) => {
          console.log(res);
          this.$swal.fire({
            icon: 'success',
            html: `Book ${this.book.title} has been deleted!`,
            showConfirmButton: false,
            timer: 3000,
          });
          this.$router.push('/');
        })
        .catch((err) => {
          console.log(err);
        });
    },
    showModal() {
      const modal = document.querySelector('.modal');
      modal.classList.toggle('is-active');
    },
    addBook() {
      const save = document.querySelector('.button-save');
      save.addEventListener('click', console.log('Clicked'));
      console.log('Hello');
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
    z-index: -1;
    background-size: cover;
    background-repeat: no-repeat;
    background-position: center center;
  }
  .detail-book{
    background-size: cover;
    background-repeat: no-repeat;
    background-position: center center;
    width: 200px;
    height: 300px;
    background-color: salmon;
    position: absolute;
    top: 250px;
    right: 50px;
  }
</style>
