<template lang="">
    <input type="text" @change="addToList" v-model="text">
    <ul>
        <li v-for="(item, index) in list" ::key="index">
           <span>{{item}}</span> 
           <span @click="deleteFromList(index)"> || delete</span>
        </li>
    </ul>
</template>

<script>
export default {
    data() {
        return {
            list: [],
            text: ''
        }
    },

    created() {
        this.list = JSON.parse(localStorage.getItem('list')) || []; // JSON.parse -> string para array
    },
    methods: {
        addToList() {
            this.list.unshift(this.text); //adiciona como primeiro elemento da lista
            this.updateLocalStorage();
            this.text = '';
        },
        deleteFromList(index) {
            this.list.splice(index, 1);
            this.updateLocalStorage();
           
        },
        updateLocalStorage() {
            localStorage.setItem('list', JSON.stringify(this.list));  // JSON.stringfy -> array para string
        }
    }
}
</script>

<style lang="">
    
</style>