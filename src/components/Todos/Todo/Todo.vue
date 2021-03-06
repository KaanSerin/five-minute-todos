<template>
  <li class="todo" :class="{ done: done }">
    <input @change="check" type="checkbox" v-model="done" />
    <div class="todo-text">{{ todoData.text }}</div>
    <div class="time-left" v-if="timeLeft">{{ timeLeft }}</div>
    <div class="remove">
      <i
        @click="$emit('removeTodo', todoData.id)"
        class="fas fa-trash"
        :class="{ done: done }"
      ></i>
    </div>
  </li>
</template>

<script>
export default {
  name: 'Todo',
  data() {
    return {
      todoData: this.todo,
      done: false,
      timeInterval: null,
    };
  },
  props: {
    todo: Object,
  },
  mounted() {
    this.timeInterval = setInterval(() => {
      this.todoData.timeLeft--;
    }, 1000);
  },
  methods: {
    check() {
      if (this.done) {
        clearInterval(this.timeInterval);
        this.timeInterval = null;
      } else {
        this.timeInterval = setInterval(() => {
          this.todoData.timeLeft--;
        }, 1000);
      }
    },
  },
  computed: {
    timeLeft() {
      if (this.todo.timeLeft <= 0) {
        this.$emit('removeTodo', this.todo.id);
        return;
      }
      return `${Math.floor(this.todo.timeLeft / 60)
        .toString()
        .padStart(2, '0')}:${(this.todo.timeLeft % 60)
        .toString()
        .padStart(2, '0')}`;
    },
  },
};
</script>

<style>
.todo {
  display: grid;
  grid-template-columns: 1fr 3fr 3fr 1fr;

  align-items: center;
  text-align: start;

  margin-top: 15px;
  padding: 10px 20px 10px 0;

  color: #222;
  background-color: #fff;

  border-radius: 12px;
  box-shadow: 0 0 6px rgba(255, 255, 255, 0.25);
  transition: color 0.25s, background-color 0.25s;
}

.todo .todo-text {
  word-wrap: break-word;
  word-break: keep-all;
}

.todo.done {
  color: #fff;
  background-color: #2762e0;
}

.todo .time-left {
  text-align: center;
}

.todo .remove {
  text-align: end;
}

.todo .remove i.fa-trash {
  font-size: 1.125rem;
  color: #2762e0;

  margin-left: 10px;
  padding: 4px;

  border: 1px solid #2762e0;
  border-radius: 3px;

  transition: all 0.25s;
}

.todo .remove i.fa-trash.done {
  color: white;
  border-color: white;
}

.todo .remove i.fa-trash:hover {
  background-color: #2762e0;
  color: white;
}

.todo .remove i:hover {
  cursor: pointer;
}
</style>
