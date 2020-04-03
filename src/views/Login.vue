<template>
  <div class="columns is-gapless login">
    <Auth />
    <div class="column">
      <div class="auth-form">
        <router-link to='/' class="logo">
          <img src="../assets/img/bookshelf.png" alt="Logo" height="80px" width="80px">
        </router-link>
        <div class="auth-intro">
          <h1>Login</h1>
          <h5>Welcome back, Please login</h5>
          <h5>to your account</h5>
        </div>
        <form action="" class="form">
          <div class="form-group">
            <label for="email">Email Address</label>
            <input type="email" name="email" id="email" placeholder="Email Address" v-model="email">
          </div>
          <div class="form-group">
            <label for="password">Password</label>
            <input type="password" name="password" id="password" placeholder="Password"
            v-model="password">
          </div>
          <Checkbox />
          <button class="button is-black" @click="signIn">Login</button>
          <router-link to='/auth/register' class="button is-white">Signup</router-link>
        </form>
        <div class="footer-login">
          <p class="intro-end">
            By signing up, you agree to Book's
          </p>
          <p class="intro-end">
            <a href="#">Terms and Conditions</a> &
            <a href="#">Privacy Policy</a>
          </p>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios';
import Auth from '../components/templates/Auth.vue';
// import FormLogin from '../components/FormLogin.vue';
import Checkbox from '../components/Checkbox.vue';

export default {
  name: 'Login',
  components: {
    Auth,
    // FormLogin,
    Checkbox,
  },
  data() {
    return {
      email: null,
      password: null,
    };
  },
  props: [
    'isLogin',
  ],
  methods: {
    signIn(event) {
      event.preventDefault();
      axios
        .post('http://localhost:5000/api/library/auth/signin', {
          email: this.email,
          password: this.password,
        })
        .then((res) => {
          this.$router.push('/');
          console.log(res);
          this.isLogin = true;
        })
        .catch((err) => {
          console.log(err);
        });
    },
  },
};
</script>

<style scoped>
  .logo{
    position: absolute;
    top: 10px;
    right: 10px;
  }
  .auth-form{
    padding: 50px 50px 20px;
  }
  .auth-intro {
    padding: 40px 0;
  }
  .auth-intro h1{
    font-size: 48px;
    font-weight: bold;
  }
  .password{
    border-radius: 5px;
    box-shadow: 0px 10px 15px rgba(0, 0, 0, 0.1);
  }
  .button{
    border: 1px solid #000000;
    font-family: Airbnb;
  }
  .is-white{
    margin-left: 5px;
  }
  .is-white:hover{
    transition: 0.5s;
    color: #ffffff;
    background: #000000;
  }
  .footer-login{
    margin-top: 50px;
  }
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
  @media (max-width: 992px) {
    .auth-form {
      transition: 1s;
      width: 100%;
    }
  }
  @media (max-width: 576px) {
    .auth-form {
      transition: 1s;
      padding-left: 1em;
      padding-right: 1em;
    }
  }

</style>
