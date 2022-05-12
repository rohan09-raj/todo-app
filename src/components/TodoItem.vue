<script setup>
import { ref, computed } from "vue";

let id = 0;

const newTodo = ref("");
const hideCompleted = ref(false);
const todos = ref([
  { id: id++, text: "Learn HTML", done: true },
  { id: id++, text: "Learn JavaScript", done: true },
  { id: id++, text: "Learn Vue", done: false },
]);

const filteredTodos = computed(() => {
  return hideCompleted.value ? todos.value.filter((t) => !t.done) : todos.value;
});

function addTodo() {
  todos.value.push({ id: id++, text: newTodo.value, done: false });
  newTodo.value = "";
}

function removeTodo(todo) {
  todos.value = todos.value.filter((t) => t !== todo);
}
</script>

<template>
  <div class="todo">
    <form @submit.prevent="addTodo" class="todo__form">
      <input
        v-model="newTodo"
        class="todo__input"
        required
        placeholder="Enter your todo"
      />
      <button class="todo__addbtn" style="--content: 'Add Todo'">
        <div class="left"></div>
        Add Todo
        <div class="right"></div>
      </button>
    </form>
    <ul class="todo__list">
      <li class="todo__item" v-for="todo in filteredTodos" :key="todo.id">
        <input type="checkbox" v-model="todo.done" />
        <span :class="{ done: todo.done }">{{ todo.text }}</span>
        <button class="todo__remove" @click="removeTodo(todo)">X</button>
      </li>
    </ul>
    <button class="todo__hidebtn" @click="hideCompleted = !hideCompleted">
      {{ hideCompleted ? "Show all" : "Hide completed" }}
    </button>
  </div>
</template>

<style scoped>
@import "../assets/base.css";

.todo {
  display: flex;
  align-items: center;
  justify-content: center;
  flex-direction: column;
  margin: 0px 20px 20px;
}

.todo__form {
  display: flex;
  align-items: center;
  justify-content: center;
}

.todo__input {
  padding: 10px;
  margin: 10px;
  border: 4px solid var(--color-border);
  border-radius: 8px;
}

.todo__addbtn {
  padding: 10px 20px;
  margin-right: 10px;
  border: none;
  background: none;
  cursor: pointer;

  font-size: 20px;
  font-weight: 900;
  text-transform: uppercase;
  color: var(--color-todo-bg);

  background-color: var(--color-primary-highlight);
  border-radius: 8px;
  z-index: 0;
  overflow: hidden;
}

.todo__addbtn:focus {
  outline-color: transparent;
}

.right::after,
.todo__addbtn::after {
  content: var(--content);
  display: block;
  position: absolute;
  white-space: nowrap;
  padding: 40px 40px;
  pointer-events: none;
}

.todo__addbtn::after {
  font-weight: 200;
  top: -30px;
  left: -20px;
}

.right,
.left {
  position: absolute;
  width: 100%;
  height: 100%;
  top: 0;
}
.right {
  left: 66%;
}
.left {
  right: 66%;
}
.right::after {
  top: -30px;
  left: calc(-66% - 20px);

  background-color: var(--color-background);
  color: transparent;
  transition: transform 0.4s ease-out;
  transform: translate(0, -90%) rotate(0deg);
}

.todo__addbtn:hover .right::after {
  transform: translate(0, -47%) rotate(0deg);
}

.todo__addbtn .right:hover::after {
  transform: translate(0, -50%) rotate(-7deg);
}

.todo__addbtn .left:hover ~ .right::after {
  transform: translate(0, -50%) rotate(7deg);
}

.todo__list {
  border: 4px solid var(--color-border);
  width: 90%;
  margin: 20px;
  padding: 20px;
  border-radius: 8px;
  list-style: none;
}

.done {
  text-decoration: line-through;
}

.todo__hidebtn {
  border: none;
  padding: 10px;
  background-color: var(--color-secondary-highlight);
  color: var(--color-todo-bg);
  border-radius: 10px;
  cursor: pointer;
  transition: 250ms all linear;
}

.todo__hidebtn:hover {
  transform: scale(1.1);
  background-color: var(--color-primary-highlight);
}

.todo__item {
  display: flex;
  align-items: center;
  justify-content: center;
  margin: 8px 0px;
}

.todo__remove {
  font-size: 20px;
  margin-left: auto;
  border-radius: 8px;
  cursor: pointer;
}

.todo__remove:hover {
  background-color: var(--color-red);
  border: 2px solid var(--color-red);
  color: var(--color-white);
}

@media screen and (max-width: 425px) {
  .todo__form {
    flex-direction: column;
  }
}
</style>
