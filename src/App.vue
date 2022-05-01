<script>
import { ref } from "@vue/reactivity";
import Form from "./components/Form.vue";
export default {
  name: "App",
  components: {
    Form,
  },
  setup() {
    let tasks = ref([]);

    const saveTask = function (data) {
      console.log("App | saveTask() | data", data);
      tasks.value = [...tasks.value, { task: data, id: Date.now() }];
      console.log("App | saveTask() | tasks.value", tasks.value);
    };
    return {
      saveTask,
      tasks,
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
    <ul>
      <li v-for="item in tasks" :key="item.id">{{ item.task }}</li>
    </ul>
    {{ tasks.length }} tâche{{ tasks.length > 1 ? "s" : "" }}
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

@media (min-width: 1024px) {
  body {
    display: flex;
    place-items: center;
  }

  #app {
    display: grid;
    grid-template-columns: 1fr 1fr;
    padding: 0 2rem;
  }

  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }

  .logo {
    margin: 0 2rem 0 0;
  }
}
</style>
