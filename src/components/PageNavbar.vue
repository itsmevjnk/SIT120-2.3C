<script setup>
/* 11. Router */
import { RouterLink } from 'vue-router'
</script>

<template>
    <nav>
        <!-- 11. Router -->
        <RouterLink to="/">Home</RouterLink>
        <RouterLink to="/todo">Todo</RouterLink>
    </nav>
</template>

<style scoped>
nav {
    display: flex;
    flex-direction: row;
    justify-content: center;
}

nav a {
    display: block;
    width: 10vw;
    padding: 1rem 0;
    text-decoration: none;
    color: black;
    text-align: center;
    transition: .5s;
    border-top-left-radius: 1rem;
    border-top-right-radius: 1rem;
}

nav a:visited {
    color: black;
}

nav a.router-link-active,
nav a:hover {
    background-color: white;
}

</style>