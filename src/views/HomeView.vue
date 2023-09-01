<script setup>
import { ref } from 'vue';
import PageSection from '../components/PageSection.vue';
/* 3. Reactivity Fundamentals: use of ref() */
const section_id = ref({
    hello: 'hello-world',
    fiddle: 'html-fiddle',
    tryout: 'class-tryout',
    calculator: 'calc',
    modulo: 'modulo'
});
</script>

<template>
    <main>
        <div class="container">
            <PageSection title="Hello World" v-bind:id="section_id.hello">
                <!-- 8.a. v-model with <input type="text"> -->
                <!-- 8.b. v-model .trim modifier -->
                What is your name? <input type="text" v-model.trim="hello_name"><br/>
                <span v-show="hello_name != ''">
                    Hello, <b>{{ hello_name }}</b>!
                </span>
            </PageSection>
            <PageSection title="HTML Fiddle" v-bind:id="section_id.fiddle">
                HTML:
                <!-- 8.a. v-model with <textarea> -->
                <textarea rows="6" placeholder="Enter the HTML source code here..." v-model="fiddle.html" class="code"></textarea>
                CSS:
                <textarea rows="6" placeholder="Enter the CSS code here..." v-model="fiddle.css" class="code"></textarea>
                <!-- 1.b. Raw HTML (v-html) -->
                <!-- 5.b. Binding Inline Styles -->
                <div class="border" v-bind:style="fiddle.css" v-html="fiddle.html"></div>
                </PageSection>
            <PageSection title="Class Tryout" v-bind:id="section_id.tryout">
                Background colour: <input type="number" v-model="class_tryout.bg" min="0" max="15">
                Foreground colour: <input type="number" v-model="class_tryout.fg" min="0" max="15">
                <!-- 5.a. Binding HTML class -->
                <p v-bind:class="'bg-' + class_tryout.bg + ' text-' + class_tryout.fg">
                    <!-- 1.d. JavaScript expressions inside syntax -->
                    {{ lipsum() }}
                </p>
            </PageSection>
            <PageSection title="Calculator" v-bind:id="section_id.calculator">
                <!-- 8.b. v-model .number modifier -->
                <input class="number right" type="text" v-model.number="calculator.a">
                <!-- 8.a. v-model with <select> -->
                <select v-model="calculator.op">
                    <option>+</option>
                    <option>-</option>
                    <option>*</option>
                    <option>/</option>
                </select>
                <input class="number right" type="text" v-model.number="calculator.b">
                <!-- 4. Computed Properties -->
                <span class="horiz-spacing">= {{ calc_result }}</span>
                <!-- 7.a. Inline Event Handling -->
                <button :disabled="typeof calc_result != 'number' || calc_result === Infinity || calc_result === -Infinity || isNaN(calc_result)" @click="calculator.a = calc_result">Copy to a</button>
                <!-- 7.b. Method Event Handling -->
                <button @click="clear_calculator">Clear</button>
            </PageSection>
            <PageSection title="Modulo Example" v-bind:id="section_id.modulo">
                <div>
                    <!-- 8.b. v-model .lazy modifier -->
                    (<input class="center" type="number" v-model.lazy="modulo.from"> to <input class="center" type="number" v-model.lazy="modulo.to">) mod <input class="center" type="number" v-model.lazy="modulo.mod" min="1"><br/>
                    <i>Press Enter or focus out of the input box to update.</i><br/>
                    <!-- 8.a. v-model with <input type="checkbox"> -->
                    <input type="checkbox" v-model="modulo.filter"> Only display calculations with result: <input class="center" type="number" v-model="modulo.filter_val" :disabled="!modulo.filter" min="0" v-bind:max="modulo.mod - 1"><br/>
                    <!-- 8.a. v-model with <input type="radio"> -->
                    <input type="radio" v-model="modulo.show" value="true"> Show <input type="radio" v-model="modulo.show" value="false"> Hide<br/>
                </div>
                <div id="modulo-result">
                    <!-- 6.b. v-for with a range -->
                    <!-- 6.c. v-for on <template> -->
                    <!-- 6.d. v-for with v-if -->
                    <template v-if="modulo.show == 'true'" v-for="i in (modulo.to - modulo.from + 1)">
                        <div class="item" v-if="!modulo.filter || calc_modulo(modulo.from + i - 1) == modulo.filter_val">
                            {{ modulo.from + i - 1 }} mod {{ modulo.mod }} = {{ calc_modulo(modulo.from + i - 1) }}
                        </div>
                    </template>
                </div>
            </PageSection>
        </div>
    </main>
</template>

<script>
export default {
    data() {
        return {
            hello_name: '',
            fiddle: {
                html: '',
                css: ''
            },
            class_tryout: {
                bg: 15,
                fg: 0
            },
            calculator: {
                a: 0,
                b: 0,
                op: '+'
            },
            modulo: {
                from: 0,
                to: 10,
                mod: 3,
                filter: false,
                filter_val: 0,
                show: 'true'
            }
        };
    },

    methods: {
        /* 2. Methods */
        lipsum() {
            return 'Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum.';
        },

        clear_calculator() {
            this.calculator.a = 0; this.calculator.b = 0;
        },

        calc_modulo(i) {
            while(i < 0) i += this.modulo.mod;
            return i % this.modulo.mod;
        }
    },

    computed: {
        /* 4. Computed Properties */
        calc_result: function() {
            if(typeof this.calculator.a != 'number') return 'a is NOT a number!';
            if(typeof this.calculator.b != 'number') return 'b is NOT a number!';
            switch(this.calculator.op) {
                case '+': return this.calculator.a + this.calculator.b;
                case '-': return this.calculator.a - this.calculator.b;
                case '*': return this.calculator.a * this.calculator.b;
                case '/': return this.calculator.a / this.calculator.b;
            }
        }
    }
};
</script>

<style scoped>
main {
    padding-top: 1rem;
    padding-bottom: 1rem;
}

textarea.code {
    font-family: 'Courier New', Courier, monospace;
}

.horiz-spacing {
    margin-left: 0.25rem;
    margin-right: 0.25rem;
}

#modulo-result {
    display: flex;
    flex-direction: row;
    flex-wrap: wrap;
}

#modulo-result .item {
    flex: 1 0 21%;
    margin: 0.5rem;
    text-align: center;
}

</style>