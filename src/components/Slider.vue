<template>
  <section id="slider">
    <h1>Book is a window</h1>
    <h1>to the world</h1>
  </section>
</template>
<script>
export default {
  name: 'Slider',
};
</script>
<style scoped>
  #slider{
    background-image: url('../assets/img/mollie-sivaram-_1gBVgy8gIU-unsplash.png');
    background-size: cover;
    background-position: center center;
    height: 450px;
    /* z-index: -1; */
    padding: 180px 0;
  }
  #slider h1{
    text-align: center;
    color: #ffffff;
    font-size: 3em;
    font-weight: bold;
    transition: 0.5s;
  }
  @media (max-width: 768px) {
    #slider h1{
      font-size: 2.5em;
    }
  }
  @media (max-width: 450px) {
    #slider h1{
      font-size: 2em;
    }
  }
</style>
