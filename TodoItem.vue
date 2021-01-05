<template>
  <li class="todo-item">
    <input type="checkbox" @input="checkTodo" :checked="todoData.done" />

    <p>{{ todoData.content }}</p>
    <button class="remove" @click="removeTodo">x</button>
  </li>
</template>

<script>
export default {
  props: {
    todoData: Object,
  },

  methods: {
    checkTodo() {
      this.$emit("check");
    },
    removeTodo() {
      this.$emit("remove");
    },
  },
};
</script>

<style>
body {
  background-color: rgba(250, 192, 150, 0.427);
}
.remove {
  border-radius: 50%;
}
.add {
  margin-left: 5px;
  background-color: rgba(133, 64, 14, 0.303);
  border-radius: 4px;
}
.todo-item {
  display: flex;
  justify-content: space-between;
  align-items: center;
  background-color: rgba(133, 64, 14, 0.303);
  border: rgba(189, 111, 29, 0.577);
  border-style: solid;
  border-radius: 4px;
}
.todo-item p {
  width: 100%;
}
.todo-item > * {
  padding: 0, 25rem;
  margin: 0, 25rem;
}
h3 {
  margin-left: 40px;
}
</style>