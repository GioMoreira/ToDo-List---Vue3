<template lang="">
  <div class="todo-list">
    <h1>ToDo-List</h1>
    <input class="text-field" type="text" @change="addToList" v-model="text" />
    <ul>
      <li v-for="(item, index) in list" ::key="index">
        <span>{{ item }}</span>
        <span class="delete-btn" @click="deleteFromList(index)"> X </span>
      </li>
    </ul>
  </div>
</template>


<script>
     
export default {
  data() {
    return {
      list: [],
      text: "",
    };
  },

  created() {
    this.list = JSON.parse(localStorage.getItem("list")) || []; // JSON.parse -> string para array
  },
  methods: {
    addToList() {
      this.list.unshift(this.text); //adiciona como primeiro elemento da lista
      this.updateLocalStorage();
      this.text = "";
    },
    deleteFromList(index) {
      this.list.splice(index, 1);
      this.updateLocalStorage();
    },
    updateLocalStorage() {
      localStorage.setItem("list", JSON.stringify(this.list)); // JSON.stringfy -> array para string
    },
  },
};
</script>

<style>
    .todo-list{
        max-width: 500px;
        margin: auto;
        
    }

    h1 {
        text-align: center;
        font-family: 'Cinzel', serif;
    }

    .text-field {
        width: 100%;
        height: 35px;
        margin-bottom: 15px;
        border-radius: 5px;
    }

    ul {
        list-style: none;
        padding: 0;
    }

    li {
        display: flex;
        justify-content: space-between;
        margin-bottom: 5px;
        font-family: sans-serif;
    }

    .delete-btn {
        background: grey;
        border: 1px solid white;
        width: 18px;
        padding: 2px;
        border-radius: 3px;
        display: flex;
        justify-content: center;
        font-weight: bold;
        margin-left: 8px ;
    }

</style>
