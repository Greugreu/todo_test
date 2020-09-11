<template>
  <v-app>
    <CreateTodo></CreateTodo>
    <ListTodo></ListTodo>
  </v-app>
</template>

<script>

import CreateTodo from "./components/CreateTodo.vue";
import ListTodo from "./components/ListTodo.vue";

export default {
  name: "App",
  components: { CreateTodo, ListTodo }
};
</script>