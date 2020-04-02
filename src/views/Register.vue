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
          <FormLogin label='Full Name' name='name' type='text'
          placeholder="Full Name"/>
          <FormLogin label='Email Address' name='email' type='email'
          placeholder="Email Address"/>
          <FormLogin label='Password' name='password' type='password'
          placeholder="Password"/>
          <FormLogin class="password" label='Repeat Password' name='password1' type='password'
          placeholder="Repeat Password"/>
          <div class="button-group">
            <router-link to='/auth/register' class="button is-black">Signup</router-link>
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
import Auth from '../components/templates/Auth.vue';
import FormLogin from '../components/FormLogin.vue';

export default {
  name: 'Login',
  components: {
    Auth,
    FormLogin,
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
