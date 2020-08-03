<template>
  <div id="app">
    <Header
      :currentList="currentList"
      :getErrorMessage="getErrorMessage"
      :numberOfActiveTasks="list[0].length"
      @switch-list="switchList"
      @add-task="addTask"
    />
    <List
      :currentList="currentList"
      :list="getList()"
      @move-task="moveTask"
      @remove-task="removeTask"
    />
  </div>
</template>

<script>
import './App.css';
import Header from './components/Header.vue';
import List from './components/List';

export default {
  name: 'App',
  components: {
    Header,
    List,
  },

  data() {
    return {
      list: [[], []],
      currentList: 0,
      currentId: 0,
    };
  },
  watch: {
    list: function() {
      localStorage.setItem('list', JSON.stringify(this.list));
    },
    currentId: function() {
      localStorage.setItem('currentId', JSON.stringify(this.currentId));
    },
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

    addTask(description) {
      this.list[0].push({
        id: this.currentId++,
        description: description,
      });
    },

    removeTask(listIndex, taskIndex) {
      let newList = [];

      this.list[listIndex].forEach((task, index) => {
        if (index !== taskIndex) {
          newList.push({ ...task });
        }
      });

      this.$set(this.list, listIndex, newList);
    },

    moveTask(listIndex, taskIndex) {
      let task = { ...this.list[listIndex][taskIndex] };
      this.removeTask(listIndex, taskIndex);
      this.list[listIndex ^ 1].push(task);
    },
  },
  created() {
    this.list = JSON.parse(localStorage.getItem('list')) || this.list;
    this.currentId =
      JSON.parse(localStorage.getItem('currentId')) || this.currentId;
  },
};
</script>
