<!--
Task: {
  id,
  category,
  description
}

data: array of Task
-->

<template>
  <div id="app">
    <Header
      :setCurrentCategory="setCurrentCategory"
      :getErrorMessage="getErrorMessage"
      :currentCategory="currentCategory"
      :numberOfActiveTasks="getTaskList('incomplete').length"
      @add-task="addTask"
    />
    <List
      :currentCategory="currentCategory"
      :taskList="getTaskList(currentCategory)"
      @move-task="moveTask"
      @remove-task="removeTask"
    />
  </div>
</template>

<script>
import "./App.css"
import Header from "./components/Header.vue"
import List from "./components/List"

export default {
  name: "App",
  components: {
    Header,
    List,
  },

  data() {
    return {
      data: [],
      currentCategory: "incomplete",
      currentId: 0,
    }
  },
  watch: {
    data: function () {
      localStorage.setItem("data", JSON.stringify(this.data))
    },
    currentId: function () {
      localStorage.setItem("currentId", JSON.stringify(this.currentId))
    },
  },

  methods: {
    Task(id, category, description) {
      this.id = id
      this.category = category
      this.description = description
    },

    getTaskList(category) {
      return this.data.filter((item) => item.category === category)
    },

    setCurrentCategory(category) {
      this.currentCategory = category
    },

    getErrorMessage(description) {
      //check empty
      if (!description) {
        return "Please enter in a task"
      }

      //check duplicate
      if (this.data.find((item) => item.description === description)) {
        return "This task already exists"
      }

      //error is not found
      return null
    },

    addTask(description) {
      this.data = [
        ...this.data,
        new this.Task(this.currentId, "incomplete", description),
      ]
      this.currentId++
    },

    removeTask(id) {
      this.data = this.data.filter((item) => item.id !== id)
    },

    moveTask(id) {
      let task = this.data.find((item) => item.id === id)
      task.category =
        task.category === "incomplete" ? "completed" : "incomplete"
    },
  },

  created() {
    this.data = JSON.parse(localStorage.getItem("data")) || this.data
    this.currentId =
      JSON.parse(localStorage.getItem("currentId")) || this.currentId
  },
}
</script>
