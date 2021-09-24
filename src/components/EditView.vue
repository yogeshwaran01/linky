<template>
  <Profile :profile="userdata.metadata.pic" :username="userdata.username" />
  <div class="container">
    <div class="container">
      <div class="row">
        <form @submit="submitted" class="col s12">
          <div class="row">
            <div class="input-field col s6">
              <input id="name" col="change" type="text" class="validate" />
              <label for="name">Name</label>
            </div>
            <div class="input-field col s6">
              <input id="link" col="change" type="url" class="validate" />
              <span class="helper-text" data-error="wrong" data-success="right"></span>
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
import Profile from "../components/mini/Profile.vue"
export default {
  name: "EditView",
  props: {
    username: String,
  },
  components: {
    Button,
    Link,
    Profile
  },
  methods: {
    btnClicked() {
      console.log("code");
    },
    submitted(e) {
      console.log("form");
      e.preventDefault();
    },
  },
  data() {
    return {
      userdata: {},
    };
  },
  created() {
    this.userdata = {
      links: [
        { link: "https://github.com", link_name: "Github" },
        { link: "https://youtube.com", link_name: "Youtube" },
      ],
      username: "yogeshwaran01",
      metadata: {
        pic: `https://robohash.org/${this.username}`,
      },
    };
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
