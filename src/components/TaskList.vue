<template>
  <h3>Toutes les tâches à faire</h3>
  {{ tasks.length }} tâche{{ tasks.length > 1 ? "s" : "" }}
  <ul>
    <li v-for="item in tasks" :key="item.id">
      <button @click="editTask(item)">Modifier</button>
      <button @click="deleteTask(item)">Supprimer</button>
      <span v-if="taskToEdit !== null && taskToEdit.id === item.id">
        <input type="text" v-model="taskToEdit.task" @keypress.enter="save" />
        <button @click="save">Sauvegarder</button>
      </span>
      <span v-else>
        {{ item.task }}
      </span>
    </li>
  </ul>
</template>

<script>
import { ref } from "@vue/reactivity";
export default {
  emits: ["delete-task", "edit-task"],
  props: {
    tasks: {
      type: Array,
      required: true,
    },
  },
  setup(props, { emit }) {
    let taskToEdit = ref(null);

    let deleteTask = function (item) {
      emit("delete-task", item);
    };

    let editTask = function (item) {
      taskToEdit.value = item;
    };

    let save = function () {
      emit("edit-task", taskToEdit.value);
      taskToEdit.value = null;
    };
    return {
      deleteTask,
      editTask,
      save,
      taskToEdit,
    };
  },
};
</script>

<style></style>
