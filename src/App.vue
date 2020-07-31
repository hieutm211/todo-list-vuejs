<template>
  <div id="app">
    <Header :currentList="currentList" :errorMessage="errorMessage" :numberOfActiveTasks="list[0].length" @switch-list="switchList" @check-error="checkError" @add-task="addTask" />
    <List :list="getList()"/>
  </div>
</template>

<script>
import './App.css'
import Header from './components/Header.vue'
import List from './components/List'

export default {
  name: 'App',
  components: {
    Header,
    List
  }, 
  data() {
    return {
      list: [
        [], 
        []
      ],
      currentList: 0,
      currentId: 0,
      errorMessage: null
    };
  },
  methods: {
    getList() {
      return this.list[this.currentList];
    },
    switchList(id) {
      this.currentList = id;
    }, 
    checkError(description) {
      //check empty
      if (!description) {
        this.errorMessage = 'Please enter in a task';
        return;
      }

      //check duplicate
      for (let li of this.list) {
        for (let task of li) {
          if (task.description === description) {
            this.errorMessage = 'This task already exists';
            return;
          }
        }
      }

      //error is not found
      this.errorMessage = null;
    },
    addTask(description) {
      this.list[0].push({
        id: this.currentId++,
        description: description
      })
      console.log(this.list);
    }
  }
}
</script>

