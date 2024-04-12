<script setup>
import Card from './Card.vue'
import DocumentationIcon from './icons/IconDocumentation.vue'
import ToolingIcon from './icons/IconTooling.vue'
import axios from 'axios'
import IconAdd from './icons/IconAdd.vue'
import { VueTable  } from "@harv46/vue-table"
import "@harv46/vue-table/dist/style.css"
</script>

<template>
  <div class="main">

    <div class="flex relative p-6">
      <Card style="width: 250px" v-for="status of statuses" :number="getDataByStatus(status.value)" :title="status.title" />
    </div>

    <div class="add">
      <button @click="$router.push('/about')" class="flex">
        <IconAdd class="flex justify-center items-center mr-2" />
      </button>
    </div>

    <VueTable :headers="headers" :keys="keyValue" :data="todos" class="">
        <template #th>
            <th> Actions</th>
        </template>
        <template #td="{ item }">
            <td class="flex actions">
                <IconUpdate @click="$router.push('/about/' + item.id)"  class="update"/>
                <IconDelete @click="deleteItem(item.id)" />
            </td>
        </template>
    </VueTable>

  </div>

</template>


<script>
import { VueTable  } from "@harv46/vue-table"
import "@harv46/vue-table/dist/style.css"
import IconUpdate from './icons/IconUpdate.vue'
import IconDelete from './icons/IconDelete.vue'

export default {
  data () {
    return {
      todos: [],
      headers: ["id", "title", "description", "status"],
      keyValue: [
        "id",
        "title",
        "description",
        "status",
      ],
      statuses: [
        {value:'pending', title: "En attente"},
        {value:'in progress', title: "En cours"}, 
        {value:'closed', title: "Terminé"},
        {value:'archived', title: "Archivé"}]
    }
  },
  beforeMount () {
    this.getData()
  },
  methods: {
    getDataByStatus (status) {
      return this.todos.filter(p => p.status === status).length
    },
    deleteItem (id) {
      axios.delete('http://localhost:3000/todos/' + id)
      .then((response) => {
        this.todos = response.data;
        this.getData();
      })
      .catch(function (error) {
        console.log(error);
      });
    },
    getData () {
      axios.get('http://localhost:3000/todos')
      .then( (response) => {
        this.todos = response.data;
      })
      .catch(function (error) {
        console.log(error);
      });
    }
  }
}
</script>

<style>
.add{
  width: 50px;
  display: flex;
  justify-content: end;
  padding: 10px;
  border-radius: 10px;
  margin-bottom: 20px;
  margin-left: 15px;
  background-color: rgb(199, 199, 255);
}
.flex{
  display: flex;
}

.main{
  padding-top: 40px;
  padding-left: 20px;
  padding-right: 20px;
  padding-bottom: 140px;
}

.update{
  margin-right: 20px;
}

.actions{
  margin-top: 20px;
}
</style>




