<template>
    <button @click="this.$emit('btnClicked')" class="waves-effect waves-light btn"
    v-bind:type="type">{{ text }}</button>
</template>

<script>
export default {
    name: "Button",
    props: {
        text: String,
        type: String
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
