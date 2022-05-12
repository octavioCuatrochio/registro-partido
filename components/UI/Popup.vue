<template>
    <p class="notificator">{{ message }}</p>
</template>

<script>
export default {
    name: "Popup",
    props: ['message']
}
</script>

<style>
.notificator {
    position: fixed;
    display: flex;
    align-items: center;
    bottom: 0;
    width: 100%;
    color: white;
    font-size: 1.5rem;
    font-weight: 300;
    padding: 10% 5%;
}

.error {
    background-color: #ff3333;
}

.success {
    background-color: #4BB543;
}
</style>