<template>
  <div class="container">
    <input
      type="text"
      v-model="newContent"
      placeholder="type something"
      @keyup.enter="addTodo"
    />

    <button class="add" @click="addTodo">ADD TODO</button>

    <ul class="list">
      <TodoItem
        v-for="todo in todos"
        v-bind:key="todo.id"
        v-bind:todoData="todo"
        @check="checkTodo(todo)"
        @remove="removeTodo(todo)"
      />
    </ul>

    <h3>You have {{ todosToBeDone }} todos left</h3>
  </div>
</template>

<script>
import TodoItem from "./TodoItem";
export default {
  components: { TodoItem },
  data() {
    return {
      newContent: "",
      todos: [],
      todosToBeDone: 0,
    };
  },

  computed: {
    unfinishedTodos() {
      return this.todos.filter((todo) => todo.done == false).lenght;
    },
  },

  methods: {
    addTodo() {
      const newTodo = {
        id: Date.now(),
        content: this.newContent,
        done: false,
      };

      this.todos.push(newTodo);
      this.newContent = "";
      this.todosToBeDone += 1;
    },
    removeTodo(theTodo) {
      this.todos = this.todos.filter((todo) => todo.id != theTodo.id);
      this.todosToBeDone -= 1;
    },

    checkTodo(theTodo) {
      theTodo.done = !theTodo.done;
      if (theTodo.done) {
        this.todosToBeDone -= 1;
      } else {
        this.todosToBeDone += 1;
      }
    },
  },
};
</script>

<style scoped>
.list {
  padding-left: 1px;
}
.container {
  max-width: 350px;
  margin: auto;
  margin-top: 50px;
  background-color: rgba(250, 192, 150, 0.427);
}
</style>