<template>
    <button @click="$emit('clicked')">{{text}}</button>
</template>

<script setup>
    defineProps({
      text: {
        type: String,
        default: "button"
      },
    })
</script>

<style lang="scss" scoped>
    button{
        width: 120px;
        height: 60px;
        border-radius: 10%;
        background-color: rgb(95, 247, 95);
        font-size: 18px;
        cursor: pointer;
    }
</style>