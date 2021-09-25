<template>
  <div v-if="isAuth">
    <Button text="Edit" @btnClicked="go" />
  </div>
  <br />
  <div v-if="!usernameValid">
    <Profile :profile="profile_pic" :username="userdata.username" />
    <div class="container">
      <div class="container">
        <Link :links="userdata.links" :needBtn="false" />
      </div>
    </div>
  </div>
  <div v-else>
    <div class="row" v-show="usernameValid">
      <h1>Username not found</h1>
    </div>
  </div>
</template>

<script>
import Link from "../components/mini/Link.vue";
import Profile from "../components/mini/Profile.vue";
import Button from "../components/mini/Button.vue";

export default {
  name: "View",
  components: {
    Link,
    Profile,
    Button,
  },
  data() {
    return {
      username: this.$route.params.username,
      allUsers: [],
      userdata: {},
      profile_pic: `https://robohash.org/${this.$route.params.username}`,
      isAuth: localStorage.getItem("isAuth"),
    };
  },
  methods: {
    go() {
      this.$router.push("/");
    },
  },
  async created() {
    const res = await fetch("http://127.0.0.1:8000/alluser");
    await res.json().then((data) => {
      this.allUsers = data["all_user_names"];
    });

    const response = await fetch(`http://127.0.0.1:8000/view/${this.username}`);
    await response.json().then((data) => {
      this.userdata = data;
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
