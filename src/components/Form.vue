<template>
  <form>
    <label for="task">Tâche à ajouter</label>
    <br />
    <input type="text" name="task" v-model="taskToDo" />
    <br />
    <button type="submit" @click="addTask">ajouter</button>
  </form>
</template>

<script>
export default {
  setup() {
    let taskToDo = "";

    const addTask = function () {
      console.log("Form | addTask() | taskToDo", taskToDo);
    };

    return {
      taskToDo,
      addTask,
    };
  },
};
</script>

<style></style>
