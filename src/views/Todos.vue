<template>
  <div>
    <h2>Todo application</h2>
    <AddTodo v-on:add-todo="addTodo" />
    <select v-model="filter">
      <option value="all">All</option>
      <option value="completed">Completed</option>
      <option value="not-completed">Not completed</option>
    </select>
    <Loader v-if="loading" />
    <TodoList
      v-else-if="filteredTodos.length"
      v-bind:todos="filteredTodos"
      v-on:remove-item="removeItem"
    >
    </TodoList>
    <p v-else>No todos!</p>
    <router-link to="/">Home</router-link>
  </div>
</template>

<script>
import TodoList from "../components/TodoList";
import AddTodo from "../components/AddTodo";
import Loader from "../components/Loader";
export default {
  name: "App",
  data() {
    return {
      todos: [],
      loading: true,
      filter: "all",
    };
  },
  components: {
    TodoList,
    AddTodo,
    Loader,
  },
  computed: {
    filteredTodos() {
      if (this.filter === "all") {
        return this.todos;
      }
      if (this.filter === "completed") {
        return this.todos.filter((item) => item.completed);
      }
      if (this.filter === "not-completed") {
        return this.todos.filter((item) => !item.completed);
      }
    },
  },
  mounted() {
    fetch("https://jsonplaceholder.typicode.com/todos?_limit=3")
      .then((response) => response.json())
      .then((json) => {
        this.todos = json;
        this.loading = false;
      });
  },
  methods: {
    removeItem(id) {
      this.todos = this.todos.filter((item) => item.id !== id);
      console.log(id);
    },
    addTodo(newTodo) {
      this.todos.push(newTodo);
    },
  },
};
</script>