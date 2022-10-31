<template>
    <div>
        <div  >
            <TodoItem 
                v-for="todo in todos"
                :key="todo.id"
                v-bind:todo="todo"
                v-on:del-todo="$emit('del-todo', todo.id)" 
                @toggle-todo="toggle"
            />
        </div>
    </div>
</template>

<script>
import TodoItem from './TodoItem'
export default {
    name: 'All-Todos',
    components: {
        TodoItem
    },
    props: ["todos"],
    methods: {
        toggle(todo) {
            this.todo = todo;
        }
    }
}
</script>

<style scoped>

</style>