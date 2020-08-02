<template>
  <div id="app">
    <Header :currentList="currentList" :getErrorMessage="getErrorMessage" :numberOfActiveTasks="list[0].length" @switch-list="switchList" @add-task="addTask" />
    <List :currentList="currentList" :list="getList()" @move-task="moveTask" @remove-task="removeTask"/>
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
    };
  },
  methods: {
    getList() {
      return this.list[this.currentList];
    },
    switchList(id) {
      this.currentList = id;
    }, 
    getErrorMessage(description) {
      //check empty
      if (!description) {
        return 'Please enter in a task';
      }

      //check duplicate
      for (let li of this.list) {
        for (let task of li) {
          if (task.description === description) {
            return 'This task already exists';
          }
        }
      }

      //error is not found
      return null;
    },
    // findTask(id) {
    //   let result;
    //   this.list.forEach((li, listIndex) => {
    //     li.forEach((task, taskIndex) => {
    //       if (task.id === id) {
    //         result = [listIndex, taskIndex];
    //       }
    //     });
    //   });
    //   return result;
    // },
    addTask(description) {
      this.list[0].push({
        id: this.currentId++,
        description: description
      });
    },

    removeTask(listIndex, taskIndex) {
      let newList = [];

      this.list[listIndex].forEach((task, index) => {
        if (index !== taskIndex) {
          newList.push({...task});
        }
      });

      this.$set(this.list, listIndex, newList);
    },

    moveTask(listIndex, taskIndex) {
      let task = {...this.list[listIndex][taskIndex]};
      this.removeTask(listIndex, taskIndex);
      this.list[listIndex ^ 1].push(task);
    }
  }
}
</script>

