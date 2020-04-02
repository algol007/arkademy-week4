<template>
  <div class="dropdown">
    <div class="dropdown-trigger">
      <a class="button" aria-haspopup="true" aria-controls="dropdown-menu" v-on:click="active">
        <span>{{sortBy}}</span>
        <span class="icon is-small">
          <i class="fas fa-angle-down" aria-hidden="true"></i>
        </span>
      </a>
    </div>
    <div class="dropdown-menu" id="dropdown-menu" role="menu">
      <div class="dropdown-content">
        <a href="#" class="dropdown-item">
          {{item1}}
        </a>
        <hr class="dropdown-divider">
        <a href="#" class="dropdown-item">
          {{item2}}
        </a>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Dropdown',
  props: [
    'sortBy',
    'item1',
    'item2',
  ],
  methods: {
    active() {
      const dropdown = document.querySelector('.dropdown');
      dropdown.classList.toggle('is-active');
      // console.log('Hello');
    },
  },
};
</script>

<style scoped>
  .button{
    border: none;
  }
  .button span{
    font-size: 14px;
  }
</style>
