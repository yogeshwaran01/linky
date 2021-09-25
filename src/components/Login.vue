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
        <div class="row" v-show="usernameValid">
          <span class="helper-text" style="text-align: center; color: red"
            >Username not found</span
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
  name: "Login",
  components: {
    Button,
  },
  data() {
    return {
      username: "",
      password: "",
      allUsers: [],
    };
  },
  methods: {
    async submited(e) {
      e.preventDefault();
      let api = "http://127.0.0.1:8000/token";
      let post_datas = {
        username: this.username,
        password: this.password,
        grant_type: "",
        scope: "",
        client_id: "",
        client_secret: "",
      };
      var form = [];
      for (var post_data in post_datas) {
        form.push(
          encodeURIComponent(post_data) +
            "=" +
            encodeURIComponent(post_datas[post_data])
        );
      }
      var body = form.join("&");
      await fetch(api, {
        method: "POST",
        headers: {
          "Content-Type": "application/x-www-form-urlencoded",
        },
        body: body,
      })
        .then((res) => {
          if (res.ok) {
            return res.json();
          } else {
            throw new Error("error");
          }
        })
        .then((data) => {
          localStorage.setItem("username", data.username);
          localStorage.setItem("token", data.Access_Token);
          localStorage.setItem("isAuth", true);
          this.$router.push(this.username);
        })
        .catch(() => {
          alert("Authentication Failed");
        });
    },
  },
  async created() {
    const res = await fetch("http://127.0.0.1:8000/alluser");
    await res.json().then((data) => {
      this.allUsers = data["all_user_names"];
    });
  },
  computed: {
    usernameValid() {
      if (this.allUsers.includes(this.username)) {
        return false;
      } else {
        return true;
      }
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
