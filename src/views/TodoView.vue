<script setup>
import { ref, watch } from 'vue'
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
                <TodoItem v-if="input != ''" :color="new_color" :content="input" class="opaque"/>
            </section>
        </div>
    </main>
</template>

<script>
export default {
    data() {
        return {
            input: '',
            new_color: 0,
            items: [] // each element is an array: first element is the color number, and the second element is the content
        };
    },

    methods: {
        add_item() {
            /* add new item */
            this.items.push([this.new_color, this.input]);
            /* clear textbox */
            this.input = '';
        },

        delete_item(i) {
            // console.log(i);
            this.items.splice(i, 1);
        }
    },

    watch: {
        /* 9. Watchers */
        input(new_input, old_input) {
            if(old_input == '' && new_input != '') {
                /* new input entered, time for random color */
                this.new_color = Math.floor(Math.random() * 3);
                if(this.items.length > 0) {
                    let last_color = this.items[this.items.length - 1][0];
                    if(this.new_color == last_color) this.new_color = (this.new_color + 1) % 4;
                }
            }
        }
    }
};
</script>