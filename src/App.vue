<script setup>
import TodoItem from "./components/TodoItem.vue";
</script>

<template>
  <main>
    <h1 class="title-app">Todo App</h1>
    <TodoItem />
  </main>

  <footer class="footer">
    <p class="footer__text">
      Link for the GitHub Repository:
      <a
        class="footer__link"
        href="https://github.com/rohan09-raj/lift-simulation"
        target="_blank"
        rel="noopener noreferrer"
        >Source Code</a
      >
    </p>
  </footer>
</template>

<style>
@import "./assets/base.css";

body {
  height: 100vh;
  width: 100vw;
  display: flex;
  align-items: center;
  justify-content: center;
}

main {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  background-color: var(--color-todo-bg);
  border-radius: 10px;
}

.title-app {
  font-size: 64px;
  margin: 30px;
}

.footer {
  position: fixed;
  bottom: 0;
  left: 0;
  right: 0;
  text-align: center;
  margin-bottom: 15px;
}

.footer__text {
  color: var(--color-todo-bg);
}

.footer__link {
  color: var(--color-primary-highlight);
}

.footer__link:hover {
  transition: all 0.5s ease-in-out;
  color: var(--color-red);
}
</style>
