<template>
  <div class="home">
    <h2>Todo app</h2>
    <button style="submit" @click="deleteAll">DeleteAll</button>
    <h3>Enter todo</h3>
    <p>Name:</p>
    <input type="text" v-model="todo.name">
    <p>Description:</p>
    <input type="text" v-model="todo.description">
    <p>Deadline:</p>
    <input type="text" v-model="todo.deadline">
    <br><br>
    <button style="submit" @click="create">Create</button>
    <hr>
    <button style="submit" @click="read">Read</button>
    <hr>
    <div v-for="todo in todos" :key="todo.name">
      <li>Name: {{ todo.name }}</li>
      <li>description: {{ todo.description }}</li>
      <li>deadline: {{ todo.deadline }}</li>
      <button style="submit" @click="deleteTodo(todo)">Delete</button>
      <hr>
    </div>
  </div>
</template>

<script>
export default {
  name: 'HomeView',
  data() {
    return {
      name: 'todos',
      todos: [],
      todo: {
        name: '',
        description: '',
        deadline: '',
      }
    }
  },
  methods: {
    read() {
      const data = sessionStorage.getItem(this.name)
      if (data) {
        this.todos = JSON.parse(data)
      }
    },
    create() {
      this.todos.push(this.todo)
      sessionStorage.setItem(this.name, JSON.stringify(this.todos))
      this.todo = {
        name: '',
        description: '',
        deadline: '',
      }
    },
    deleteTodo(todo) {
      this.todos = this.todos.filter((item) => item.name !== todo.name)
      sessionStorage.setItem(this.name, JSON.stringify(this.todos))
    },
    deleteAll() {
      sessionStorage.clear()
      this.todos = []
    }
  }
}
</script>
