<template>
  <div class="card">
    <div class="card-image">
      <figure class="image is-4by3">
        <img src="https://bulma.io/images/placeholders/1280x960.png" alt="Placeholder image">
      </figure>
    </div>
    <div class="card-content">
      <div class="media">
        <div class="media-content">
          <p class="title is-4">{{ bookTitle }}</p>
        </div>
      </div>

      <div class="content">
        {{ bookDesc }}
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Card',
  props: [
    'bookTitle',
    'bookDesc',
  ],
};
</script>

<style scoped>
  .card{
    width: 250px !important;
    height: 350px;
    margin: 10px 5px;
  }
  .title{
    font-size: 18px;
  }
  .media-content{
    height: 20px;
    overflow: hidden;
  }
  .content{
    font-size: 14px;
    height: 85px;
    overflow: hidden;
  }
  .card-content .media{
    margin-bottom: 16px !important;
  }
</style>
