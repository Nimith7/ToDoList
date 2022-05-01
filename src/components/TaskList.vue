<template>
  <h3>Toutes les tâches à faire</h3>
  {{ tasks.length }} tâche{{ tasks.length > 1 ? "s" : "" }}
  <ul>
    <li v-for="item in tasks" :key="item.id">
      <button @click="deleteTask(item)">Supprimer</button>
      {{ item.task }}
    </li>
  </ul>
</template>

<script>
export default {
  emits: ["delete-task"],
  props: {
    tasks: {
      type: Array,
      required: true,
    },
  },
  setup(props, { emit }) {
    let deleteTask = function (item) {
      emit("delete-task", item);
    };
    return {
      deleteTask,
    };
  },
};
</script>

<style></style>
