<template>
  <section>
    <DetailBook />
    <div class="description">
      <div class="column is-9 desc">
        <div class="availability">
          <div class="column desc-box">
            <div class="category">
              <button class="button is-rounded is-warning">Novel</button>
            </div>
            <div class="desc-title">Dilan 1990</div>
            <div class="desc-subtitle">30 Juni 2019</div>
          </div>
          <div class="column status">
            <p>Available</p>
          </div>
        </div>
        <div class="desc-text">
          <p>
            Lorem ipsum dolor sit amet, consectetur adipiscing elit. Proin ac diam eget
            est rutrum ultrices. Donec laoreet enim a massa dapibus, cursus egestas dui
            pulvinar. Proin sit amet accumsan lectus. Nullam auctor auctor consequat.
            Donec semper magna erat, sed fringilla lacus pretium eget. Cras porttitor,
            nibh sit amet interdum bibendum, nibh velit accumsan tellus, vel vehicula
            tellus leo vitae ipsum. Praesent sit amet libero sed orci ullamcorper
            efficitur. Pellentesque in euismod purus, sit amet ultrices tortor. Vestibulum
            ante dui, tempor at dui id, tincidunt euismod diam. Integer pellentesque massa
            nibh, ac eleifend odio malesuada sed. Phasellus orci sem, cursus nec orci ut,
            accumsan facilisis lacus. Nullam at elementum nibh, ac gravida felis. In
            sagittis rhoncus nisi tempus dignissim. Sed fringilla consequat ante vitae
            lobortis. Cras posuere ligula vel enim suscipit malesuada. Vivamus non
            nulla ut ante imperdiet euismod quis nec massa.
          </p>
        </div>
      </div>
      <div class="column is-2 button-borrow">
        <button class="button is-warning">Borrow</button>
      </div>
    </div>
  </section>
</template>

<script>
import DetailBook from '../components/templates/Detail.vue';

export default {
  name: 'Detail',
  components: {
    DetailBook,
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
    background-image: url('../assets/img/Arrow.png');
    background-position: center center;
    background-repeat: no-repeat;
    border-radius: 50%;
    cursor: pointer;
  }
  .nav-option a{
    padding: 0 10px;
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
  .description{
    padding: 40px 90px;
    justify-content: space-between;
    display: flex;
  }
  .availability{
    display: flex;
    align-items: center;
  }
  .desc-box{
    flex-direction: column;
  }
  .status{
    display: flex;
    flex-direction: row-reverse;
    color: #48c744;
    font-size: 20px;
  }
  .desc-title{
    margin-top: 20px;
    font-size: 40px;
  }
  .desc-subtitle{
    font-size: 20px;
  }
  .desc-text{
    margin-top: 20px;
  }
  .button-borrow{
    padding-bottom: 50px !important;
    display: flex;
    align-items: flex-end;
    justify-content: center;
  }
  @media (max-width: 992px) {
    .description {
      flex-direction: column;
      margin-top: 150px;
    }
    .desc{
      width: 100% !important;
    }
    .button-borrow{
      /* padding-left: 0.75rem !important; */
      justify-content: flex-start;
    }
  }
  @media (max-width: 768px) {
    .availability{
      flex-direction: column;
    }
    .availability .column{
      display: flex;
      width: 100%;
    }
    .status{
      flex-direction: row;
    }
  }
  @media (max-width: 576px) {
    .description{
      padding: 40px 20px;
    }
  }
</style>
