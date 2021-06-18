<template>
<div class="main">
  <div class="mainBox">
    <h1>Even the prettiest flowers have their bad days.</h1>
    <form class="registerInfo">
      <fieldset>
        <p>If you don't have an account already, please register.</p>
        <input placeholder="first name" v-model="firstName">
      </fieldset>
      <fieldset>
        <input placeholder="last name" v-model="lastName">
      </fieldset>
      <fieldset>
        <input placeholder="username" v-model="username">
      </fieldset>
      <fieldset>
        <input type="password" placeholder="password" v-model="password">
      </fieldset>
      <fieldset>
        <button type="submit" class="registerButton registerButton-primary" @click.prevent="register">Register for an Account!</button>
      </fieldset>
    </form>
    <p v-if="error" class="error">{{error}}</p>
    <form class="registerInfo">
      <fieldset>
        <p>Login</p>
        <input placeholder="username" v-model="usernameLogin">
        <input type="password" placeholder="password" v-model="passwordLogin">
      </fieldset>
      <fieldset>
        <button type="submit" class="registerButton registerButton-primary" @click.prevent="login">Login to Your Account!</button>
      </fieldset>
    </form>
    <p v-if="errorLogin" class="error">{{errorLogin}}</p>
  </div>
</div>
</template>

<script>
import axios from 'axios';
export default {
  name: 'HomePage',
  data() {
    return {
      firstName: '',
      lastName: '',
      username: '',
      password: '',
      usernameLogin: '',
      passwordLogin: '',
      error: '',
      errorLogin: '',
    }
  },
  methods: {
  async register() {
    this.error = '';
    this.errorLogin = '';
    if (!this.firstName || !this.lastName || !this.username || !this.password)
      return;
    try {
      let response = await axios.post('/api/users', {
        firstName: this.firstName,
        lastName: this.lastName,
        username: this.username,
        password: this.password,
      });
      this.$root.$data.user = response.data.user;
    } catch (error) {
      this.error = error.response.data.message;
      this.$root.$data.user = null;
    }
  },
  async login() {
     this.error = '';
     this.errorLogin = '';
     if (!this.usernameLogin || !this.passwordLogin)
       return;
     try {
       let response = await axios.post('/api/users/login', {
         username: this.usernameLogin,
         password: this.passwordLogin,
       });
       this.$root.$data.user = response.data.user;
     } catch (error) {
       this.errorLogin = "Error: " + error.response.data.message;
       this.$root.$data.user = null;
     }
   }
}
}
</script>

<style scoped>
.registerButton{
  background-color: #1d3557;
  color:white;
}
h1 {
  font-size: 30px;
  color:#8e9aaf;
}

.main {
  padding: 30px;
  display: flex;
  justify-content: left;
}

.mainBox {
  background: white;
  padding: 20px;
  font-size: 20px;
  text-align: left;
}

.main::after {
  content: "";
  background-size: 100%;
  background-repeat: no-repeat;
  top: 0;
  left: 0;
  bottom: 0;
  right: 0;
  position: absolute;
  z-index: -1;
}

.main img {
  height: 20px;
  margin: 0px;
}

.main form {
  font-size: 14px;
}

.main form p {
  font-size: 20px;
}

input {
  margin-right: 10px;
}

.error {
  margin-top: 20px;
  display: inline;
  padding: 5px 20px;
  border-radius: 30px;
  font-size: 10px;
  background-color: #d9534f;
  color: #fff;
}
</style>
