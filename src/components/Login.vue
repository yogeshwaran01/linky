<template>
  <h1>Login</h1>
  <div class="container">
    <div class="row">
      <form @submit="submited" class="col s12">
        <div class="row">
          <div class="input-field col s12">
            <input
              type="text"
              id="username"
              name="username"
              col="change"
              v-model="username"
            />
            <label for="username">Username</label>
          </div>
        </div>
        <div class="row">
          <div class="input-field col s12">
            <input
              type="password"
              id="password"
              name="password"
              col="change"
              v-model="password"
            />
            <label for="password">Password</label>
          </div>
        </div>
        <div class="row">
          <Button text="Submit" type="submit" />
        </div>
      </form>
    </div>
  </div>
</template>

<script>
import Button from "./mini/Button.vue";

export default {
  name: "Login",
  components: {
    Button,
  },
  data() {
    return {
      username: "",
      password: "",
    };
  },
  methods: {
    submited(e) {
      console.log("Done");
      e.preventDefault();
    },
  },
};
</script>

<style scoped>
h1 {
  text-align: center;
  color: #5cbe09;
  text-decoration: underline;
  font-size: xx-large;
}

.input-field input[col="change"]:focus + label {
  color: #5cbe09;
}

.input-field input[col="change"]:focus {
  border-bottom: 1px solid #5cbe09;
  box-shadow: 0 1px 0 0 #5cbe09;
}
</style>
