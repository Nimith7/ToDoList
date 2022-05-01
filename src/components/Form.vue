<template>
  <form @submit.prevent="addTask">
    <label for="task">Tâche à ajouter</label>
    <br />
    <input type="text" name="task" v-model="taskToDo" />
    <br />
    <button type="submit">ajouter</button>
  </form>
</template>

<script>
import { ref } from "@vue/reactivity";
export default {
  setup(props, ctx) {
    let taskToDo = ref("");

    const addTask = function () {
      console.log("Form | addTask() | taskToDo.value", taskToDo.value);
      ctx.emit("add", taskToDo.value);
      taskToDo.value = "";
    };

    return {
      taskToDo,
      addTask,
    };
  },
};
</script>

<style></style>
