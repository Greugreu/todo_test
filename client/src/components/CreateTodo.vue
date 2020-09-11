<template>
  <div>
    <div class="d-flex justify-center">
      <h1 id="addTodo">Ajouter une tache</h1>
    </div>
    <div class="d-flex justify-center">
      <v-col cols="6" style="margin: 0px auto;">
        <v-text-field v-model="newTodo" label="Nom de la tâche" solo></v-text-field>
      </v-col>
    </div>
    <div class="d-flex justify-center">
      <v-btn @click="addToDo()" color="primary">Ajouter</v-btn>
      <v-btn @click="reloadPage()" color="primary" style="margin-left: 1%">Actualiser</v-btn>
    </div>
  </div>
</template>

<script>

import axios from "axios";

export default {
  data: () => ({
    newToDo: "",
  }),

  methods: {

    addToDo() {
      axios.post("http://localhost:3000/todo/add", {
        todo: this.newTodo })
          .then(response => {
            this.message = response.data;
          });
    },
    reloadPage(){
      window.location.reload()
    },
  }
}
</script>

<style scoped>

</style>