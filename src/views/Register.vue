<template>
  <div class="columns is-gapless login">
    <Auth />
    <div class="column">
      <div class="auth-form">
        <router-link to='/' class="logo">
          <img src="../assets/img/bookshelf.png" alt="Logo" height="80px" width="80px">
        </router-link>
        <div class="auth-intro">
          <h1>Register</h1>
          <h5>Welcome back, Please register</h5>
          <h5>to create account</h5>
        </div>
        <form action="" class="form">
          <div class="form-group">
            <label for="name">Fullname</label>
            <input type="name" name="name" id="name" placeholder="Fullname" v-model="name">
          </div>
          <div class="form-group">
            <label for="email">Email Address</label>
            <input type="email" name="email" id="email" placeholder="Email Address" v-model="email">
          </div>
          <div class="form-group">
            <label for="password">Password</label>
            <input type="password" name="password" id="password" placeholder="Password"
            v-model="password">
          </div>
          <div class="form-group">
            <label for="password2">Repeat Password</label>
            <input type="password" name="password2" id="password2" placeholder="Repeat Password"
            v-model="password2">
          </div>
          <div class="button-group">
            <button @click="signUp" class="button is-black">Signup</button>
            <router-link to='/auth/login' class="button is-white">Login</router-link>
          </div>
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

export default {
  name: 'Login',
  components: {
    Auth,
    // FormLogin,
  },
  data() {
    return {
      name: null,
      email: null,
      password: null,
      password2: null,
    };
  },
  methods: {
    signUp(event) {
      event.preventDefault();
      if (this.password !== this.password2) {
        console.log('Password tidak sama!');
      } else {
        axios
          .post('http://localhost:5000/api/library/auth/signup', {
            name: this.name,
            email: this.email,
            password: this.password,
          })
          .then((res) => {
            this.$router.push('/auth/login');
            console.log(res);
          })
          .catch((err) => {
            console.log(err);
          });
      }
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
  .button-group{
    margin: 30px 0;
  }
  .button{
    font-family: Airbnb;
    border: 1px solid #000000;
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
