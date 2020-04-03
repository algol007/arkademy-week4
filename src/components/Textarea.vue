<template>
  <div class="field is-horizontal">
    <div class="field-label is-normal">
      <label class="label">{{name}}</label>
    </div>
    <div class="field-body">
      <div class="field">
        <div class="control">
          <textarea class="textarea" :placeholder="name"
          :value="value"></textarea>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Textarea',
  props: [
    'name',
    'value',
  ],
};
</script>

<style></style>
