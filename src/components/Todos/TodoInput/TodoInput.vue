<template lang="html">
  <div class="add-todo">
    <input
      placeholder="Tidy up your room..."
      @keyup.enter="onSubmit"
      type="text"
      :value="newTodoText"
      @change="newTodoText = $event.target.value"
    />
    <button @click="onSubmit">
      <i class="fas fa-plus-circle"></i>
    </button>
  </div>
</template>

<script>
export default {
  name: 'TodoInput',
  data() {
    return {
      newTodoText: '',
    };
  },
  methods: {
    onSubmit() {
      if (this.newTodoText.length < 2) return;
      this.$emit('addTodo', this.newTodoText);
      this.newTodoText = '';
    },
  },
  emits: ['addTodo'],
};
</script>

<style>
.add-todo {
  box-sizing: border-box;
  display: flex;
  width: 100%;
  padding: 8px 12px 8px 18px;
  border-radius: 18px;
  background-color: #fff;
  box-shadow: 0 0 6px rgba(255, 255, 255, 0.25);
}

.add-todo button {
  border: none;
  background: none;
}

.add-todo button:hover {
  cursor: pointer;
}

.add-todo button i.fa-plus-circle {
  font-size: 1.25rem;
  color: #2762e0;
}

.add-todo button i.fa-plus-circle:hover {
  color: #1f58d1;
}

.add-todo input {
  flex-grow: 1;
  padding: 6px 0 6px 0px;
  font-size: 1rem;
  border: none;
}

.add-todo input:focus {
  outline: none;
}
</style>
