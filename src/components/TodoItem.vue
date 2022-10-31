<template>
    <div class="todo-item" v-bind:class="{'is-completed': todo.completed}">
        <p>
            <input type="checkbox" v-on:change="markCompleted">
            {{todo.title}}
            <button v-on:click="$emit('del-todo', todo.id)" class="del">x</button>
        </p>
    </div>
</template>

<script>
export default {
    name: "Todo-Item",
    props: ["todo"],
    methods: {
      // Here I avoided to mutate the props, which prompt for an error
        markCompleted: function() {
          let workingTodo = this.todo;
          workingTodo.completed = !workingTodo.completed;
          this.$emit('toggle-completed', workingTodo)
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
  .is-completed {
    text-decoration: line-through;
  }
  .del {
    background: #ff0000;
    color: #fff;
    border: none;
    padding: 5px 9px;
    border-radius: 50%;
    cursor: pointer;
    float: right;
  }
</style>