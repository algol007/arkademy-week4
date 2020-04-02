<template>
  <div class="dashboard">
    <Navbar/>
    <Slider/>
    <div class="book">
      <h1>List Book</h1>
      <div class="list-book">
        <router-link to="/book/detail"><Card/></router-link>
      </div>
    </div>
  </div>
</template>

<script>
import Navbar from '../components/Navbar.vue';
import Slider from '../components/Slider.vue';
import Card from '../components/Card.vue';

export default {
  name: 'Dashboard',
  components: {
    Navbar,
    Slider,
    Card,
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
    display: flex;
  }
  .list-book h1{
    display: block;
  }
</style>
