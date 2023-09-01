<script setup>
/* 10.a. Props */
const props = defineProps({
    title: String,
    id: {
        type: String,
        default: ''
    }
})
</script>

<template>
    <!-- 1.c. Attribute Bindings -->
    <section v-bind:id="props.id">
        <h2>{{ props.title }}</h2>
        <template v-if="props.id != ''">
            <!-- 1.a. Text Interpolation -->
            <i>Section ID: {{ props.id }}</i><br/>
        </template>
        <!-- 10.c. Slots -->
        <slot/>
    </section>
</template>

<style>
section {
    padding: 0.5rem;
    margin: 0.5rem;
}
</style>