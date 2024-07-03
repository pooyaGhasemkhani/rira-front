<template>
  <div class="todo-list">
    <h1>rira todo list</h1>
    <form @submit.prevent="addTodo()">
      <input v-model="newTodo" name="newTodo" autocomplete="off" />
      <button>Add</button>
    </form>
    <Rira-Table
    v-for="(todo, index) in todos"
      @remove="removeTodo"
      @done="doneTodo"
      :key="index"
      :content="todo.content"
      :done="todo.done"
      :id="index"
    />
    <!-- <h4 v-if="todos.length === 0">Empty list.</h4> -->
  </div>
</template>

<script>
import { ref } from "vue";
import RiraTable from "@/components/RiraTable/index.vue";
export default {
  name: "App",
  setup() {
    function createStorage(){
      if(!localStorage.getItem("todos")){
        localStorage.setItem("todos",JSON.stringify([]))
      }
    }
    createStorage()
    const newTodo = ref("");
    const todosData = JSON.parse(localStorage.getItem("todos"));
    const todos = ref(todosData);
    function addTodo() {

      if (newTodo.value.trim()) {
        todos.value.push({
          done: false,
          content: newTodo.value,
        });
        newTodo.value = "";
      }
      saveData();
    }
    function doneTodo({index , done}) {
        todos.value[index].done = done
      saveData();
    }
    function removeTodo(index) {
      todos.value.splice(index, 1);
      saveData();
    }
    function saveData() {
      const storageData = JSON.stringify(todos.value);
      localStorage.setItem("todos", storageData);
    }
    return {
      todos,
      newTodo,
      addTodo,
      doneTodo,
      removeTodo,
      saveData,
    };
  },
  components: {
    RiraTable,
  },
};
</script>
