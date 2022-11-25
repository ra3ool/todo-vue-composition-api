<template>
  <h4 class="card-title">vue Todo list</h4>
  <TodoAddForm @todo-text="addTodo"></TodoAddForm>
  <div class="list-wrapper">
    <ul class="d-flex flex-column-reverse todo-list">
      <Todo
        v-for="(todo, index) in todos"
        :item="todo"
        :key="index"
        @edit-todo="editTodo"
        @delete-todo="deleteTodo"
        @do-todo="doTodo"
      >
      </Todo>
    </ul>
  </div>
</template>

<script setup>
import Todo from "./components/Todo.vue";
import TodoAddForm from "./components/TodoAddForm.vue";
import { ref } from "vue";

const todos = ref(JSON.parse(localStorage.getItem("todo")) || []);
// try {
//   todos = JSON.parse(localStorage.getItem("todo")) || [];
//   console.log("try");
// } catch (error) {
//   todos = [];
//   console.log("catch");
// }
// refreshTodos()

function refreshTodos() {
  localStorage.setItem("todo", JSON.stringify(todos.value));
}
function addTodo(val) {
  let now = new Date();
  todos.value.push({
    id: Date.now(),
    done: false,
    text: val,
    date:
      now.toLocaleDateString("fa", { weekday: "long" }) +
      " " +
      now.toLocaleDateString("fa") +
      " ساعت " +
      now.toLocaleTimeString("fa"),
  });
  refreshTodos();
}
function editTodo(id, text) {
  todos.value = todos.value.map((item) => {
    if (item.id == id) item.text = text;
    return item;
  });
  refreshTodos();
}
function deleteTodo(id, text) {
  let ok = confirm("are you sure want to delete following todo?" + "\n" + text);
  if (ok) todos.value = todos.value.filter((item) => item.id != id);
  refreshTodos();
}
function doTodo(id, done) {
  todos.value = todos.value.map((item) => {
    if (item.id == id) item.done = done;
    return item;
  });
  refreshTodos();
}
</script>

