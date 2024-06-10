<template>
  <div id="app">
    <h1>Daftar Tugas</h1>
    <div class="input-group">
      <input v-model="newTodo" @keyup.enter="addTodo" placeholder="Add a new list" />
      <button @click="addTodo" class="btn btn-primary">Add</button>
    </div>
    <ul>
      <li v-for="(todo, index) in todos" :key="index" :class="{ completed: todo.completed }">
        <div class="todo-item">
          <input type="checkbox" v-model="todo.completed" @change="toggleTodo(index)" />
          <span>{{ todo.text }}</span>
          <button @click="confirmDelete(index)" class="btn btn-danger">Delete</button>
        </div>
      </li>
    </ul>
    <p class="unfinished-todos">Unfinished Todos: <strong>{{ unfinishedTodos }}</strong></p>
  </div>
</template>

<script>
export default {
  data() {
    return {
      newTodo: '',
      todos: []
    }
  },
  computed: {
    unfinishedTodos() {
      return this.todos.filter(todo => !todo.completed).length;
    }
  },
  methods: {
    addTodo() {
      if (this.newTodo.trim() !== '') {
        this.todos.push({ text: this.newTodo, completed: false });
        this.newTodo = '';
      }
    },
    confirmDelete(index) {
      if (confirm('Are you sure you want to delete this todo?')) {
        this.removeTodo(index);
      }
    },
    removeTodo(index) {
      this.todos.splice(index, 1);
    },
    toggleTodo(index) {
      this.todos[index].completed = !this.todos[index].completed;
    }
  }
}
</script>

<style>
#app {
  max-width: 600px;
  margin: 50px auto;
  padding: 20px;
  text-align: center;
  font-family: 'Montserrat';
}

.input-group {
  margin-bottom: 20px;
}

input[type="text"] {
  width: 70%;
  padding: 10px;
  margin-right: 10px;
}

.btn {
  padding: 10px 20px;
  border: none;
  border-radius: 5px;
  cursor: pointer;
}

.btn-primary {
  background-color: #007bff;
  color: #181212;
}

.btn-danger {
  background-color: #dc3545;
  color: #1e1111;
}

ul {
  list-style-type: none;
  padding: 0;
}

.todo-item {
  display: flex;
  align-items: center;
  justify-content: space-between;
  margin-bottom: 10px;
  padding: 10px;
  background-color: #181d21;
  border: 1px solid #171111;
  border-radius: 5px;
}

.completed span {
  text-decoration: line-through;
  color: #271a1a;
}

.unfinished-todos {
  font-weight: bold;
  margin-top: 20px;
}
</style>
