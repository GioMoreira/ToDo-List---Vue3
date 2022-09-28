<template lang="">
    <input type="text" @change="addToList" v-model="text">
    <ul>
        <li v-for="(item, index) in list" ::key="index">
            {{item}}
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
    methods: {
        addToList() {
            this.list.unshift(this.text);
            this.text = '';
        }
    }
}
</script>

<style lang="">
    
</style>