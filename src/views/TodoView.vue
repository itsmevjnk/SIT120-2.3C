<script setup>
import TodoItem from '../components/TodoItem.vue'
</script>

<template>
    <main>
        <div class="container-l3">
            <section>
                <h2 class="margin-center">What are you planning to do today?</h2>
                <textarea rows="6" v-model="input"></textarea>
                <button @click="add_item" :disabled="input == ''" class="block margin-center">Add</button>
            </section>
            <section>
                <!-- 6.a. v-for with an Object -->
                <!-- 6.e. v-for with a Component -->
                <TodoItem v-for="([color, content], i) in items" :key="i" :index="i" :color="color" :content="content" @delete="delete_item"/>
            </section>
        </div>
    </main>
</template>

<script>
export default {
    data() {
        return {
            input: '',
            items: [] // each element is an array: first element is the color number, and the second element is the content
        };
    },

    methods: {
        add_item() {
            /* pick color */
            let color = Math.floor(Math.random() * 3);
            if(this.items.length > 0) {
                let last_color = this.items[this.items.length - 1][0];
                if(color == last_color) color = (color + 1) % 4;
            }
            /* add new item */
            this.items.push([color, this.input]);
            /* clear textbox */
            this.input = '';
        },

        delete_item(i) {
            // console.log(i);
            this.items.splice(i, 1);
        }
    }
};
</script>