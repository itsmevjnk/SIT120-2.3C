<script setup>
/* 10.a. Props */
const props = defineProps({
    index: Number,
    color: Number,
    content: String    
})
/* 10.b. Events using $emit */
defineEmits(['delete'])
</script>

<template>
    <div v-bind:class="'todo-item color-' + color">
        <div class="content">{{ props.content }}</div>
        <div class="button" @click="$emit('delete', props.index)">❌</div>
    </div>
</template>

<style scoped>
/* color palette: https://colorhunt.co/palette/fdfdbdc8ffd4b8e8fcb1afff */
.todo-item.color-0 { background-color: #fdfdbd; }
.todo-item.color-1 { background-color: #c8ffd4; }
.todo-item.color-2 { background-color: #b8e8fc; }
.todo-item.color-3 { background-color: #b1afff; }

.todo-item {
    align-items: flex-start;
    margin: 6px 0;
    padding: 10px;
    border-radius: 10px;;
}

.todo-item .content {
    flex: 1;
    white-space: pre-line;
    padding: 6px;
}

.todo-item .button {
    flex: 0;
    cursor: pointer;
    padding: 4px;
}
</style>