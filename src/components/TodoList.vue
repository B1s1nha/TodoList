<template>
  <main>
    <section class="todo-list">
      <h3>To do Today:</h3>
      <div class="all-todos">
        <div
          class="single-todo"
          v-for="todo in todos"
          :key="todo.text"
          :class="todo.done ? 'done' : ''"
          @click="todo.done = !todo.done; storeTodos();"
        >
          <p>{{ todo.text }}</p>
        </div>
      </div>

      <button
        v-if="todos.length"
        class="clear"
        @click="todos = []; storeTodos();"
      >
        Clean
      </button>

      <input
        type="text"
        placeholder="Escreva uma nova tarefa..."
        v-model="newTodo.text"
      />
      <button
        class="add"
        @click="addTodo();storeTodos()"
      >
        Add
      </button>
      <div class="instructions">
        Instructions:
        <ul>
          <li>To finish a task, just click on it</li>
          <li>If you want to restart your list, just click on "Clean" button</li>
        </ul>
      </div>
    </section>
  </main>
</template>

<script>
export default {
  name: "TodoList",
  data() {
    return {
      todos: [],
      newTodo: {
        done: false,
      },
    };
  },
  methods: {
    addTodo: function () {
      if (this.newTodo.text && this.newTodo.text.trim() !== "") {
        this.todos.push(this.newTodo);
        this.newTodo = {
          done: false,
        };
        localStorage.setItem("todos", JSON.stringify(this.todos));
      } else {
        alert("Você precisa preencher a descrição da tarefa.");
      }
    },
    storeTodos() {
      localStorage.setItem("todos", JSON.stringify(this.todos));
    },
  },
  created() {
    this.todos = localStorage.getItem("todos")
      ? JSON.parse(localStorage.getItem("todos"))
      : this.todos;
  },
};
</script>
