<template>
  <Button text="Log out" type="submit" @btnClicked="clear" />
  <br />
  <br />
  <Profile :profile="profile_pic" :username="userdata.username" />
  <div class="container">
    <div class="container">
      <div class="row">
        <form @submit="submitted" class="col s12">
          <div class="row">
            <div class="input-field col s6">
              <input
                id="name"
                col="change"
                type="text"
                class="validate"
                v-model="name"
              />
              <label for="name">Name</label>
            </div>
            <div class="input-field col s6">
              <input
                id="link"
                col="change"
                type="url"
                class="validate"
                v-model="link"
              />
              <span
                class="helper-text"
                data-error="wrong"
                data-success="right"
              ></span>
              <label for="link">Link</label>
            </div>
          </div>
          <Button text="Add Link" type="submit" />
        </form>
      </div>
    </div>
  </div>
  <div class="container">
    <div class="container">
      <Link
        :links="userdata.links"
        :needBtn="true"
        @delClicked="btnClicked()"
      />
    </div>
  </div>
</template>

<script>
import Button from "../components/mini/Button.vue";
import Link from "../components/mini/Link.vue";
import Profile from "../components/mini/Profile.vue";
export default {
  name: "EditView",
  props: {
    username: String,
  },
  components: {
    Button,
    Link,
    Profile,
  },
  methods: {
    btnClicked() {
      console.log("code");
    },
    async submitted(e) {
      e.preventDefault();
      let data = {
        username: this.username,
        links: [
          {
            link_name: this.name,
            link_url: this.link,
          },
        ],
      };
      await fetch("http://127.0.0.1:8000/postlinks", {
        method: "POST",
        headers: {
          "Content-Type": "application/json",
          Authorization: `Bearer ${localStorage.getItem("token")}`,
        },
        body: JSON.stringify(data),
      })
        .then((res) => {
          if (res.ok) {
            return res.json();
          } else {
            throw new Error("error");
          }
        })
        .then((data) => {
          this.userdata = data;
        })
        .catch(() => {
          alert("Invalid link");
        });
    },
    clear() {
      localStorage.clear();
      this.$router.go();
    },
  },
  data() {
    return {
      userdata: {},
      profile_pic: `https://robohash.org/${this.username}`,
      name: "",
      link: "",
    };
  },
  async created() {
    const response = await fetch(`http://127.0.0.1:8000/view/${this.username}`);
    await response.json().then((data) => {
      this.userdata = data;
    });
  },
};
</script>

<style scoped>
.input-field input[col="change"]:focus + label {
  color: #5cbe09;
}

.input-field input[col="change"]:focus {
  border-bottom: 1px solid #5cbe09;
  box-shadow: 0 1px 0 0 #5cbe09;
}
</style>
