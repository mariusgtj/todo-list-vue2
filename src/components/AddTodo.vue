<template>
    <div>
        <form @submit="addTodo">
            <input type="text" v-model="title" name="title" placeholder="Add Todo...">
            <input type="submit" value="Submit" class="btn">
        </form>
    </div>
</template>

<script>
// Use uuid for making unique ids
// import { v4 as uuidv4 } from 'uuid';
export default {
    name: "Add-Todo",
    data() {
        return {
            title: ''
        }
    },
    methods: {
        addTodo: function(e) {
            // alert(uuidv4())

            // prevent page reload. Could have been done in form with: @submit.prevent="".
            e.preventDefault();

            // Construct the object
            // const newTodo = {
            //     id: uuidv4(),
            //     title: this.title,
            //     completed: false
            // }
            const newTodo = {
                title: this.title,
                completed: false
            }


            // Send up to parent by emitting an event
            this.$emit('add-todo', newTodo); // "add-todo" method will be invoked in App.vue with: "<AddTodo v-on:add-todo="addTodo" />". In App.vue, another "addTodo" method is defined (could be any name).
            this.title = '';
        }
    }
}
</script>

<style scoped>
    form {
        display: flex;
    }
    input[type="text"] {
        flex: 10;
        padding: 5px;
    }
    input[type="submit"] {
        flex: 2;
    }

    .btn {
        display: inline-block;
        border: none;
        background: #555;
        color: #fff;
        padding: 7px 20px;
        cursor: pointer;
    }

    .btn:hover {
        background: #666;
    }
</style>

