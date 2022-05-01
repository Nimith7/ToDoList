<script>
import { ref } from "@vue/reactivity";
import Form from "./components/Form.vue";
import TaskList from "./components/TaskList.vue";
export default {
  name: "App",
  components: {
    Form,
    TaskList,
  },
  setup() {
    let tasks = ref([]);

    const saveTask = function (data) {
      console.log("App | saveTask() | data", data);
      tasks.value = [...tasks.value, { task: data, id: Date.now() }];
      console.log("App | saveTask() | tasks.value", tasks.value);
    };

    const editTask = function (item) {
      tasks.value = tasks.value.map((t) => (t.id !== item.id ? t : item));
    };

    const deleteTask = function (item) {
      console.log("App | deleteTask() | item", item);
      tasks.value = tasks.value.filter((t) => t.id !== item.id);
    };
    return {
      saveTask,
      deleteTask,
      tasks,
      editTask,
    };
  },
};
</script>

<template>
  <header>
    <img
      alt="ToDoList logo"
      class="logo"
      src="./assets/logo.png"
      width="125"
      height="125"
    />

    <div class="wrapper">
      <h1>To Do List</h1>
      <Form @add="saveTask" />
    </div>
  </header>

  <main>
    <TaskList :tasks="tasks" @delete-task="deleteTask" @edit-task="editTask" />
  </main>
</template>

<style>
@import "./assets/base.css";

#app {
  max-width: 1280px;
  margin: 0 auto;
  padding: 2rem;

  font-weight: normal;
}

header {
  line-height: 1.5;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

ul {
  list-style-type: none;
}
</style>
