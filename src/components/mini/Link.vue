<template>
  <div :key="link.link_name" v-for="link in links">
    <div v-if="needBtn">
      <div class="mor">
            <a :href="link.link_url" >{{ link.link_name }}</a>
            <div class="can">
                <Icon :name="'delete'" @iconClicked="this.$emit('delClicked')" />
            </div>
        </div>
    </div>
    <div v-else>
      <div class="mor">
        <a :href="link.link_url">{{ link.link_name }}</a>
      </div>
    </div>
  </div>
</template>

<script>
import Icon from "../mini/Icon.vue"
export default {
  name: "Link",
  components: {
    Icon
  },
  props: {
    links: Array,
    needBtn: Boolean,
  },
};
</script>

<style scoped>
.mor {
  margin: 5px;
  padding: 15px;
  border: 2px;
  border-color: greenyellow;
  border-radius: 5px;
  border-style: solid;
  text-align: center;
  font-size: 20px;
}
a {
  color: red;
  text-transform: capitalize;
}
.can {
    float: right;
}

</style>
