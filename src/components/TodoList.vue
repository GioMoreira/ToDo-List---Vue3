<template lang="">
  <div class="todo-list">
    <h1>ToDo-List</h1>
    <input class="text-field" type="text" @change="addToList" v-model="text" />
    <ul>
      <li v-for="(item, index) in list" ::key="index">
        <span @click="toggleCheckbox(item)">
          <input type="checkbox" :checked="item.done">
          {{ item.label }}
        </span>
        <span class="delete-btn material-symbols-outlined" @click="deleteFromList(index)"> 
          X
        </span>
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
      this.list.unshift({label: this.text, done:false}); //adiciona como primeiro elemento da lista
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
    toggleCheckbox(item) {
      item.done = !item.done;
      this.updateLocalStorage();
    }
  },
};
</script>

<style>
    .todo-list{
        max-width: 500px;
        padding: 10px;
        margin: auto;
        background: #f9dcc4 ;
        border-radius: 10px;
        border: 1px solid #b5838d;
        
    }

    h1 {
        text-align: center;
        
        
    }

    .text-field {
        width: 100%;
        height: 35px;
        margin: 10px 0 30px 0;;
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
        font-size: 16px;
        font-family: 'Lato', sans-serif;
    }

    .delete-btn {
        background: #b5838d;
        border: 1px solid white;
        width: 20px;
        padding: 2px;
        border-radius: 3px;
        display: flex;
        justify-content: center;
        font-weight: bold;
        margin-left: 8px ;
        color: #fff;
        cursor: pointer;
    }

</style>
