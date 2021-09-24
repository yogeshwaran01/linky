<template>
    <button class="material-icons" @click="this.$emit('iconClicked')">{{ name }}</button>
</template>

<script>
import Button from './Button.vue'
export default {
  components: { Button },
    name: 'Icon',
    props: {
        name: String
    }
}
</script>

<style scoped>
button {
    background-color: #5cbe09;
    color: black;
}
button:hover {
    background-color: #5cbe09;
}
button:focus-within {
    background-color: #5cbe09;
}
</style>
