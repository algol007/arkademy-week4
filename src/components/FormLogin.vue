<template>
  <div class="form-group">
    <label :for="name">{{ label }}</label>
    <input :type="type" :name="name" :id="name" :placeholder="placeholder"
    v-model="modelInput">
  </div>
</template>
<script>
export default {
  name: 'FormLogin',
  props: [
    'name',
    'type',
    'label',
    'placeholder',
    'model',
  ],
  methods: {
    modelIInput() {
      this.$emit('mInput', 'something');
    },
  },
};
</script>
<style scoped>
  .form-group{
    border-radius: 5px;
    padding: 10px 20px;
    border: 1px solid #e0e0e0;
  }
  .form-group input{
    font-family: Airbnb;
    border: none;
    display: block;
    font-size: 16px;
    outline: none;
    width: 100%;
    color: #424242;
  }
  .form-group input:focus{
    background: none;
  }
  .form-group label{
    color: #d0cccc;
    font-size: 14px;
    display: block;
  }
</style>
