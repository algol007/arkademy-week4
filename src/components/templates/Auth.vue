<template>
  <div class="column is-gapless is-three-fifths auth-image">
    <div class="overlay"></div>
    <div class="text-image">
      <div class="text-slogan">
        <h1>Book is a window</h1>
        <h1>to the world</h1>
      </div>
      <div class="text-footer">
        <p>Photo by Mark Pan4ratte on Unsplash</p>
      </div>
    </div>
  </div>
</template>

<script>

export default {
  name: 'Auth',
};
</script>

<style scoped>
  .auth-image{
    background-image: url('../../assets/img/mollie-sivaram-_1gBVgy8gIU-unsplash.png');
    background-size: cover;
    background-position: center center;
    min-height: 700px;
    height: 100vh;
    z-index: -1;
    padding: 0 !important;
  }
  .overlay{
    background-color: rgba(0, 0, 0, 0.5);
    min-height: 700px;
    height: 100vh;
    width: 60%;
    position: absolute;
  }
  .text-image{
    position: absolute;
    padding: 30px;
    color: #ffffff;
    display: flex;
    flex-direction: column;
    align-content: space-between;
    min-height: 700px;
    height: 100vh;
  }
  .text-slogan h1{
    font-size: 50px;
    font-weight: bold;
  }
  .text-footer{
    position: absolute;
    bottom: 20px;
  }
  @media (max-width: 992px) {
    .auth-image {
      display: none;
    }
  }
</style>
