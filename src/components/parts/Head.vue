<template>
    <div class="head">
        <h2>{{ title }}</h2>
        <p>{{msg}}</p>
    </div>
</template>

<script setup>
    defineProps({
      title: {
        type: String,
        default: "Generator"
      },
      msg: {
        type: String,
        default: ""
      },

    })
</script>

<style lang="scss" scoped>
    .head{
        display: flex;
        flex-direction: column;
        justify-content: flex-start;
        align-items: center;
        width: 80%;
        margin:20px auto 0 auto;
        border-top: dashed 1px rgb(95, 247, 95);
        h2{
        font-size: 32px;
    }

    }

</style>