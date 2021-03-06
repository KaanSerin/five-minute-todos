<template lang="html">
  <div class="todos">
    <TodoInput @add-todo="addTodo" />
    <transition-group
      tag="ul"
      :class="{ 'todo-list': todos.length > 0 }"
      name="fade"
    >
      <Todo
        @remove-todo="removeTodo"
        v-for="todo in todos"
        :key="todo.id"
        :todo="todo"
      />
    </transition-group>
  </div>
</template>

<script>
import TodoInput from './TodoInput/TodoInput.vue';
import Todo from './Todo/Todo.vue';
import { uuid } from 'vue-uuid';

export default {
  name: 'Todos',
  data() {
    return {
      todos: [],
    };
  },
  methods: {
    addTodo(todoText) {
      const newTodo = { id: uuid.v4(), text: todoText, timeLeft: 300 };
      this.todos.push(newTodo);
      console.log(todoText);
    },
    removeTodo(todoID) {
      console.log(`removed todo with id: ${todoID}`);
      this.todos = this.todos.filter((todo) => todo.id !== todoID);
    },
  },
  components: {
    Todo,
    TodoInput,
  },
};
</script>

<style lang="css">
.todos {
  max-width: 500px;
  margin: auto;
}

.todo-list {
  display: inline-block;
  width: 90%;

  list-style: none;

  margin-top: 0px;
  padding: 0;

  border-top: none;
}

.fade-enter-active {
  opacity: 0;
}

.fade-enter-to {
  opacity: 1;
}

.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.3s;
}

.fade-enter,
.fade-leave-to {
  opacity: 0;
}
</style>
