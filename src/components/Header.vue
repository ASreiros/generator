<template>
    <div class="header">
        <h1>Generators</h1>
        
    </div>
</template>

<script>
    export default{
        name:"Header",
    }
</script>

<style scoped>
    .header{
        display: flex;
        width: 100%;
        flex-direction: column;
        justify-content: center;
        align-items: center;
    }

    h1{
        text-transform: uppercase;
        font-weight: bold;
        margin-top: 20px;
        font-size: 36px;
    }
</style>