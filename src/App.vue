<template>
  <h1>Vue 3 Todo App</h1>
  <form @submit.prevent="addNewTodo">
    <label>New todo</label>
    <input
      v-model="newTodo"
      type="text"
      name="newTodo"
      placeholder="Enter your tasks"
    />
    <button>Add New todo</button>
  </form>

  <button @click="markAllDone">All Done</button>
  <button @click="removeAll">Remove all</button>
  <ul>
    <li v-for="(todo, index) in todos" :key="todo.id">
      <h3 :class="{ done: todo.done }" @click="toggleDone(todo)" class="todo">
        {{ todo.content }}
        <button @click="removeTodo(index)">Remove todo</button>
      </h3>
    </li>
  </ul>
</template>

<script>
import { ref } from "vue";

export default {
  setup() {
    const newTodo = ref("");
    const todos = ref([]);
    function addNewTodo() {
      todos.value.push({
        id: Date.now(),
        done: false,
        content: newTodo.value,
      });
      newTodo.value = "";
    }
    function toggleDone(todo) {
      todo.done = !todo.done;
    }
    function removeTodo(index) {
      todos.value.splice(index, 1);
    }
    function markAllDone() {
      todos.value.forEach((todo) => (todo.done = true));
    }
    function removeAll() {
      todos.value = [];
    }
    return {
      addNewTodo,
      newTodo,
      todos,
      toggleDone,
      removeTodo,
      markAllDone,
      removeAll,
    };
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
li {
  font-size: 2rem;
  color: black;
}
.todo {
  cursor: pointer;
}
.done {
  text-decoration: line-through;
  color: silver;
}
</style>
