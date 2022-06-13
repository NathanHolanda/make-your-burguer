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
    margin: 10px auto;
    padding: 15px 10px;
    border-radius: 4px;
    max-width: 450px;
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

.info{
    color: #2233aa;
    border: #8899ff solid 1px;
    background-color: #bbccff;
}

.container p{
    margin-right: auto;
}
</style>