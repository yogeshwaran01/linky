<template>
  <div v-if="isAuth">
    <EditView :username="username"/>
  </div>
  <div v-else>
    <Button @btnClicked="this.showLogin = false; this.showRegister = true" text="Register" /> | 
    <Button @btnClicked="this.showRegister = false; this.showLogin = true" text="Login"/>

    <div v-if="showLogin" class="container" id="login">
      <Login />
    </div>

    <div v-if="showRegister" class="container" id="register">
      <Register />
    </div>
  </div>
</template>

<script>

import EditView from "../components/EditView.vue"
import Login from "../components/Login.vue"
import Register from "../components/Register.vue"
import Button from "../components/mini/Button.vue"

export default {
  name: 'Home',
  components: {
    EditView,
    Login,
    Register,
    Button
  },
  data() {
    return {
      'isAuth': localStorage.getItem('isAuth') || false,
      'showLogin': false,
      'showRegister': true,
      'username': localStorage.getItem('username')
    }
  },
  methods() {
    toggle = () => {
      this.showLogin = !this.showLogin
    }
  }
}
</script>
