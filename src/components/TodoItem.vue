<template>
    <div class="todo-item" v-bind:class="{'is-complete':todo.completed}">
        <div class="">
            <div class="col-sm">
                <input type="checkbox" class="" v-on:change="markComplete">
                {{ todo.title }}
                <button @click="$emit('del-todo',todo.id)" class="del">x</button>
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        name: "Todoitem",
        props: ["todo"],
        methods: {
            markComplete(){
                this.todo.completed = !this.todo.completed;
            }
        }
    }
</script>

<style scoped>
    .todo-item {
        background: #f4f4f4;
        padding: 10px;
        border-bottom: 1px #ccc dotted;
    }
    .is-complete {
        text-decoration: line-through;
    }
    .del {
        background: red;
        color: #ffffff;
        border: none;
        border-radius: 50%;
        cursor: pointer;
        float:  right;
    }
</style>