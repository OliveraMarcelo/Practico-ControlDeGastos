<template>
    <div class="header">
        <img class="img-header" src="../assets/cashflow-icon_73798840-dd9d-4253-9c6d-821fe57c686a.svg" alt="logo"
            @click="reload">
        <h1><span class="green">Cash</span><span class="sky-blue">Flow</span></h1>
    </div>
</template>

<script setup>
const reload = () => {
    console.log("Hello");
    location.reload()
}
</script>

<style scoped>
.header {
    margin: 0 0 0 10vw;
    display: flex;
    flex-direction: row;
    align-items: center;
}

.img-header {
    width: 20vw;
    height: 10vh;
    margin-right: 20px;
}

.green {
    color: rgb(0, 255, 21);
}

.sky-blue {
    color: rgb(15, 186, 253);
}
</style>