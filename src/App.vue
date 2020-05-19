<template>
  <div id="app">
    <div class="container grid-xs py-2">
      <img class="img-responsive img-logo" src="@/assets/logo.png" alt="Vue.JS" />
      <h2 class="text-center">Vue Task</h2>
      <form @submit.prevent="addTodo(todo)">
        <div class="input-group">
          <input type="text" v-model="todo.description" class="form-input" placeholder="Nova Task" />
          <button class="btn btn-primary input-group-btn">Adicionar</button>
        </div>
        <div class="todo-list">
          <todo v-for="t in todos" :key="t.id" @toggle="toggleTodo" @delete="deleteTodo" :todo="t" />
        </div>
      </form>
    </div>
  </div>
</template>

<script>
import Todo from "./components/Todo";

export default {
  name: "App",
  components: {
    Todo
  },
  data() {
    return {
      todos: [],
      todo: { checked: false }
    };
  },
  mounted() {
    if (localStorage.getItem("todos")) {
      try {
        this.todos = JSON.parse(localStorage.getItem("todos"));
      } catch (e) {
        localStorage.removeItem("todos");
      }
    }
  },
  methods: {
    addTodo(todo) {
      if (!todo.description) {
        return;
      }

      todo.id = Date.now();
      this.todo = { checked: false };
      this.todos.push(todo);

      this.updateTodos();
    },

    toggleTodo(todo) {
      const index = this.todos.findIndex(item => item.id === todo.id);

      if (index > -1) {
        const checked = !this.todos[index].checked;
        this.$set(this.todos, index, { ...this.todos[index], checked });
        this.updateTodos();
      }
    },

    updateTodos() {
      const parsed = JSON.stringify(this.todos);
      localStorage.setItem("todos", parsed);
    },

    deleteTodo(id) {
      const index = this.todos.findIndex(item => item.id === id);
      if (index > -1) {
        this.$delete(this.todos, index);
        this.updateTodos();
      }
    }
  }
};
</script>

<style scoped>
.img-logo {
  max-width: 200px;
  margin: 0 auto;
}

.todo-list {
  margin-top: 2rem;
}

.item {
  border-bottom: 1px solid #eee;
}
</style>
