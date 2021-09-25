<template>
  <h1>Register</h1>
  <div class="container">
    <div class="row">
      <form @submit="submited" class="col s12" id="form">
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
          <div class="input-field col s6">
            <input
              type="password"
              id="password"
              name="password"
              col="change"
              v-model="password"
            />
            <label for="password">Password</label>
          </div>
          <div class="input-field col s6">
            <input
              type="password"
              id="confirmPassword"
              name="confirmPassword"
              col="change"
              v-model="confirmPassword"
            />
            <label for="confirmPassword">Confirm Password</label>
          </div>
        </div>
        <div class="row">
          <div class="input-field col s12">
            <input
              type="email"
              id="email"
              name="email"
              col="change"
              class="validate"
              v-model="email"
            />
            <label for="email">E-Mail</label>
            <span
              class="helper-text"
              data-error="wrong"
              data-success="right"
            ></span>
          </div>
        </div>
        <div class="row" v-show="!usernameValid">
          <span class="helper-text" style="text-align: center; color: red"
            >Username already Found</span
          >
        </div>
        <div class="row" v-show="!passwordValid">
          <span class="helper-text" style="text-align: center; color: red"
            >Password not Matching</span
          >
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
  name: "Register",
  components: {
    Button,
  },
  data() {
    return {
      username: "",
      password: "",
      confirmPassword: "",
      email: "",
      allUsers: [],
    };
  },
  methods: {
    async submited(e) {
      e.preventDefault();
      let api = "http://127.0.0.1:8000/signup";
      let data = {
        username: this.username,
        email: this.email,
        password: this.password,
      };
      await fetch(api, {
        method: "POST",
        headers: {
          "Content-Type": "application/json",
        },
        body: JSON.stringify(data),
      })
        .then((res) => {
          if (res.ok) {
            return res.json();
          } else {
            throw new Error("error")
          }
        })
        .then((data) => {
          alert("Registeration done")
          this.username = ""
          this.password = ""
          this.confirmPassword = ""
          this.email = ""
        })
        .catch(() => {
          alert("Invalid form submission")
        })
    },
  },
  computed: {
    usernameValid() {
      if (this.allUsers.includes(this.username)) {
        return false;
      } else {
        return true;
      }
    },
    passwordValid() {
      if (this.password === this.confirmPassword) {
        return true;
      } else {
        return false;
      }
    },
  },
  async created() {
    const res = await fetch("http://127.0.0.1:8000/alluser");
    await res.json().then((data) => {
      this.allUsers = data['all_user_names']
    });
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
