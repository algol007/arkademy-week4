<template>
  <div class="checkbox">
    <div class="check">
      <label class="checkbox-label">
        <input type="checkbox" id="checklist" checked />
        <span class="checkbox-custom"></span>
        <div class="remember">Remember Me</div>
      </label>
    </div>
    <div class="forgot">
      <a href="#" class="forgot-password">Forgot Password?</a>
    </div>
  </div>
</template>
<script>
export default {
  name: 'Checkbox',
};
</script>
<style scoped>
.checkbox {
  margin: 20px 0;
  width: 100%;
  display: flex;
  flex-direction: row;
  align-items: center;
  justify-content: space-between;
}

.check {
  display: inline-block;
}

.forgot-password {
  color: #424242;
  float: right;
}

.checkbox,
.button-group {
  border: none;
  padding: 0;
}

.remember {
  margin-left: 30px;
  color: #424242;
  width: 200px;
}

.remember,
.forgot-password {
  font-size: 14px !important;
}

.checkbox-label {
  display: block;
  position: relative;
  margin: auto;
  cursor: pointer;
  font-size: 22px;
  line-height: 24px;
  height: 24px;
  width: 24px;
  clear: both;
}

.checkbox-label input {
  position: absolute;
  opacity: 0;
  cursor: pointer;
}

.checkbox-label .checkbox-custom {
  position: absolute;
  top: 0px;
  left: 0px;
  height: 20px;
  width: 20px;
  background-color: transparent;
  border-radius: 2px;
  transition: all 0.3s ease-out;
  -webkit-transition: all 0.3s ease-out;
  -moz-transition: all 0.3s ease-out;
  -ms-transition: all 0.3s ease-out;
  -o-transition: all 0.3s ease-out;
  border: 1px solid #000000;
}

.checkbox-label input:checked ~ .checkbox-custom {
  /* background-color: ; */
  border-radius: 2px;
  -webkit-transform: rotate(0deg) scale(1);
  -ms-transform: rotate(0deg) scale(1);
  transform: rotate(0deg) scale(1);
  opacity: 1;
  border: 1px solid #000000;
}

.checkbox-label .checkbox-custom::after {
  position: absolute;
  content: "";
  left: 12px;
  top: 12px;
  height: 0px;
  width: 0px;
  border-radius: 5px;
  border: 2px solid #424242;
  border-width: 0 3px 3px 0;
  -webkit-transform: rotate(0deg) scale(0);
  -ms-transform: rotate(0deg) scale(0);
  transform: rotate(0deg) scale(0);
  opacity: 1;
  transition: all 0.3s ease-out;
  -webkit-transition: all 0.3s ease-out;
  -moz-transition: all 0.3s ease-out;
  -ms-transition: all 0.3s ease-out;
  -o-transition: all 0.3s ease-out;
}

.checkbox-label input:checked ~ .checkbox-custom::after {
  -webkit-transform: rotate(45deg) scale(1);
  -ms-transform: rotate(45deg) scale(1);
  transform: rotate(45deg) scale(1);
  opacity: 1;
  left: 6px;
  top: 0px;
  width: 6px;
  height: 12px;
  border: 2px solid #424242;
  border-width: 0 2px 2px 0;
  background-color: transparent;
  border-radius: 0;
}
</style>
