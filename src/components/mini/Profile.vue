<template>
  <div class="container">
    <img :src="profile" :alt="username" />
    <h5>{{ username }}</h5>
  </div>
</template>

<script>
export default {
  name: "Profile",
  props: {
    profile: String,
    username: String,
  },
};
</script>

<style scoped>
img {
  border-radius: 50%;
  border: 5px greenyellow solid;
  margin-bottom: 1rem;
  width: 200px;
}

h5 {
    font-weight: normal;
}
</style>
