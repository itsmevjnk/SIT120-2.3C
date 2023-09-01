<script setup>
/* 10.a. Props */
const props = defineProps({
    title: String,
    subtitle: String
})
</script>

<template>
    <header>
        <h1>{{ props.title }}</h1>
        <i>{{ props.subtitle }}</i>
    </header>
</template>

<style scoped>
header {
    text-align: center;
    padding: 24px 5vw;
}
</style>