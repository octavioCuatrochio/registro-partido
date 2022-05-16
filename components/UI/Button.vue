<template>
    <button :type="type" class="button">
        <slot />
    </button>
</template>

<script>
export default {
    name: 'Button',
    props: ['type']
}
</script>

<style>
.button {
    font-size: 1rem;
    font-weight: 900;
    padding: 5% 20%;
    border: none;
    border-radius: 10px;
    color: white;
    background-color: #6e4d9c;
}
</style>