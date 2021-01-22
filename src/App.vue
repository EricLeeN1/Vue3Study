<template>
<img alt="Vue logo" src="./assets/logo.png" />
<HelloWorld :msg="msg" />
<button @click="reverseMessage">反转 Message</button>
<input type="text" v-model="msg">
<ol>
    <ToDo v-for="(item,index) in todos" :todo="item" :key="index" :data-id="index" />
</ol>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'
import ToDo from './components/ToDo.vue'

export default {
    name: 'App',
    data() {
        return {
            msg: 'Hello Vue 3.0 + Vite',
            todos: [{
                    text: 'Learn JavaScript'
                },
                {
                    text: 'Learn Vue'
                },
                {
                    text: 'Build something awesome'
                }
            ]
        }
    },
    components: {
        HelloWorld,
        ToDo
    },
    methods: {
        reverseMessage() {
            this.msg = this.msg
                .split('')
                .reverse()
                .join('')
        }
    }
}
</script>
