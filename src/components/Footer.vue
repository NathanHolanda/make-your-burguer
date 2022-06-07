<template>
    <footer>
        Make Your Burguer &copy; {{new Date().getFullYear()}}
    </footer>
</template>

<script>
    export default {}
</script>

<style scoped>
    footer{
        height: 200px;
        background-color: #222;
        border-top: 4px solid #111;
        color: #fcba03;
        display: flex;
        align-items: center;
        justify-content: center;
        width: 100%;
    }
</style>