<template>
  <div class="card">
    <div class="card-image">
      <figure class="image is-2by2">
        <img :src="image" :alt="image">
      </figure>
    </div>
    <div class="card-content">
      <div class="media">
        <div class="media-content">
          <p class="title is-4">{{ bookTitle }}</p>
        </div>
      </div>

      <div class="content">
        {{ bookAuthor }} - {{ year }}
      </div>

    </div>
  </div>
</template>

<script>
export default {
  name: 'Card',
  props: [
    'bookTitle',
    'bookAuthor',
    'year',
    'image',
  ],
};
</script>

<style scoped>
  .card{
    transition: 0.5s;
    width: 250px !important;
    height: 350px;
    margin: 10px  ;
  }
  .card-image{
    height: 250px;
    overflow: hidden;
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
    /* height: 85px; */
    overflow: hidden;
  }
  .card-content{
    padding: 10px 20px;
  }
  .card-content .media{
    margin-bottom: 16px !important;
  }
</style>
