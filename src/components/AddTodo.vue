<template>
    <div class="container">
        <form @submit="addTodo">
            <div class="input-group">
                <input v-model="title" type="text" name="title" placeholder="Add Todo...">
            </div>
            <div class="input-group">
                <input type="submit" value="submit" class="btn btn-primary btn-sm">
            </div>
        </form>
    </div>
</template>

<script>
    //import uuid from 'uuid';
    export default {
        name: "AddTodo",
        data(){
            return {
                title: '',
            }
        },
        methods: {
            addTodo(e){
                e.preventDefault();
                const newTodo = {
                    //id: uuid.v4(),
                    title: this.title,
                    completed: false,
                };
                this.$emit('add-todo',newTodo);
                this.title ='';
            }
        }
    }
</script>

<style scoped>
    form {
        display: flex;
    }
    input[type="text"]{
        flex: 10;
        padding: 5px;
    }
</style>