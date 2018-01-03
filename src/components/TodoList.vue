<template>
  <div> 
    <p class="tasks">Completed Tasks: {{todos.filter(todo => {return todo.done === true}).length}}</p>
    <p class="tasks">Pending Tasks: {{todos.filter(todo => {return todo.done === false}).length}}</p>
    <todo v-for="todo in todos" v-on:delete-todo="deleteTodo" v-on:complete-todo="completeTodo" v-bind:todo="todo" v-bind:key="todo.id" :todo.sync="todo"></todo>
    <create-todo v-on:add-todo="addTodo"></create-todo>
  </div>
</template>

<script type = "text/javascript">
import Todo from './Todo'
import CreateTodo from './CreateTodo'

export default {
  components: {
    Todo,
    CreateTodo
  },
  methods: {
    deleteTodo (todo) {
      const todoIndex = this.todos.indexOf(todo)
      this.todos.splice(todoIndex, 1)
    },
    addTodo (todo) {
      this.todos.push(todo)
    },
    completeTodo (todo) {
      const todoIndex = this.todos.indexOf(todo)
      this.todos[todoIndex].done = true
    }
  },
  data () {
    return {
      todos: [
        {
          id: 1,
          title: 'Todo A',
          project: 'Project A',
          done: false
        },
        {
          id: 2,
          title: 'Todo B',
          project: 'Project B',
          done: true
        },
        {
          id: 3,
          title: 'Todo C',
          project: 'Project C',
          done: false
        }
      ]
    }
  }
}
</script>

<style>
p.tasks {
  text-align: center;
}
</style>
