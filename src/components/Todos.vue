<template>
  <div>
    <h2>To Do</h2>
    <form v-on:submit.prevent="addTodo">
      <div class="form-row">
        <div class="form-group col">
          <label for="text">Task</label>
          <input required type="text" v-model="todoText" placeholder="Enter new To Do task" class="form-control form-control-sm" name="text">
        </div>
      </div>
      <button type="submit" class="btn btn-primary">Add</button>
    </form>
    <div class="pt-1 rounded">
      <ul v-for="todo in todos" v-bind:key="todo.id" class="list-group">
        <li class="list-group-item">
          <input type="checkbox" @change="updateTodo(todo.id)">
          {{ todo.text }}
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  name: "Todos",
  data() {
    return {
      todos:[],
      todoText: '',
    }
  },
  methods: {
    addTodo () {
      let todoEntry = {
        id: this.todos.length,
        text: this.todoText,
        complete: false
      }
      this.todos = [...this.todos, todoEntry]
      localStorage.setItem('todos', JSON.stringify(this.todos))
    },
    updateTodo (id) {
      this.todos[id].complete = !this.todos[id].complete
      localStorage.setItem('todos', JSON.stringify(this.todos))
    }
  },
  mounted() {
    const existingTodos = localStorage.getItem('todos')
    this.todos = JSON.parse(existingTodos) || []
  }
}
</script>