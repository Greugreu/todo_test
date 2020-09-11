<template>
  <div>
    <h2 class="d-flex justify-center">Non terminé</h2>
    <div v-for="todo in uncompletedTodos" :key="todo._id">
      <v-card class="mx-auto" color="white" dark max-width="800">
        <v-card-text class="font-weight-bold title blue--text"> {{ todo.title }}
          <v-list-item id="todo-list-item" class="grow">
            <v-btn @click="completeTodo(todo._id)" class="mx-2" small color="green"> Terminer </v-btn>
            <v-btn @click="deleteTodo(todo._id)" class="mx-2" small color="red"> Supprimer </v-btn>
          </v-list-item>
        </v-card-text>
      </v-card>


    <!-- completed todos -->
    </div>
    <h2 class="d-flex justify-center">Terminé </h2>
    <div v-for="todo in completedTodos" :key="todo._id">
      <v-card class="mx-auto" color="blue" dark max-width="800">
        <v-card-text class="font-weight-bold title white--text"> {{ todo.title }}
          <v-list-item id="todo-list-item2" class="grow">
            <v-btn @click="deleteTodo(todo._id)" class="mx-2" small color="red"> Supprimer </v-btn>
          </v-list-item>
        </v-card-text>
      </v-card>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "ListTodo",
  data: () => ({
    newToDo: "",
    uncompletedTodos: [],
    completedTodos: []
  }),
  methods: {
    completeTodo(todoID) {
      axios
          .post("http://localhost:3000/todo/complete/" + todoID)
          .then(response => {
            console.log(response.data);
          });
    },
    deleteTodo(todoID) {
      axios.delete("http://localhost:3000/todo/" + todoID).then(response => {
        console.log(response.data);
      });
    }
  },
  created() {
    // fetch uncompleted task
    axios
        .get("http://localhost:3000/todo/uncompleted")
        .then(response => (this.uncompletedTodos = response.data))
        .catch(error => console.log(error));
    // fetch completed task
    axios
        .get("http://localhost:3000/todo/completed")
        .then(response => (this.completedTodos = response.data))
        .catch(error => console.log(error));
  }
}
</script>

<style scoped>

</style>