<template>
    <div v-show="message" :class="`container ${type}`">
        <p>{{ message }}</p>
    </div>
</template>

<script>
export default {
    props: ["message", "type"]
}
</script>


<style scoped>
.container {
    margin: 10px 0;
    padding: 15px 10px;
    border-radius: 4px;
}

.success{
    color: #22aa33;
    border: #88ff99 solid 1px;
    background-color: #bbffcc;
}

.error{
    color: #aa2233;
    border: #ff8899 solid 1px;
    background-color: #ffbbcc;
}

.container p{
    margin-right: auto;
}
</style>