<template>
  <Profile :profile="userdata.metadata.pic" :username="userdata.username" />
  <div class="container">
      <div class="container">
        <Link :links="userdata.links" :needBtn="false"/>
      </div>
  </div>
</template>

<script>

import Link from '../components/mini/Link.vue'
import Profile from '../components/mini/Profile.vue'

export default {
  name: "View",
  components: {
      Link,
      Profile,
  },
  data() {
    return {
      username: this.$route.params.username,
      userdata: {}
    };
  },
  created() {
      this.userdata = {
          links: [
              {'link': 'https://github.com', 'link_name': 'Github'},
              {'link': 'https://youtube.com', 'link_name': 'Youtube'}
          ],
          username: 'yogeshwaran01',
          metadata: {
              pic : `https://robohash.org/${this.username}`
          }  
      }
  }

};
</script>
