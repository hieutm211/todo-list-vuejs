<template>
  <header>
    <div class="date-and-input">
      <div class="date">
        {{ date }}
      </div>

      <div class="number-of-tasks">
        <span class="blue"> {{ numberOfActiveTasks }} Active Tasks </span>
      </div>

      <TaskForm v-on="$listeners" :getErrorMessage="getErrorMessage" />
    </div>

    <nav>
      <button
        :class="getClassName('incomplete')"
        @click="setCurrentCategory('incomplete')"
      >
        Incomplete Tasks
      </button>
      <button
        :class="getClassName('completed')"
        @click="setCurrentCategory('completed')"
      >
        Completed Tasks
      </button>
    </nav>
  </header>
</template>

<script>
import TaskForm from "./TaskForm.vue";

export default {
  name: "Header",
  props: {
    setCurrentCategory: {
      type: Function,
      required: true,
    },
    numberOfActiveTasks: {
      type: Number,
      required: true,
    },
    currentCategory: {
      type: String,
      required: true,
    },
    getErrorMessage: {
      type: Function,
      required: true,
    },
  },
  components: {
    TaskForm,
  },
  data() {
    return {};
  },
  methods: {
    getClassName(category) {
      if (this.currentCategory === category) {
        return "active";
      }
      return null;
    },
  },
  computed: {
    date() {
      const dayNames = [
        "Sunday",
        "Monday",
        "Tuesday",
        "Wednesday",
        "Thursday",
        "Friday",
        "Saturday",
      ];
      const monthNames = [
        "January",
        "February",
        "March",
        "April",
        "May",
        "June",
        "July",
        "August",
        "September",
        "October",
        "November",
        "December",
      ];

      const today = new Date();

      return (
        dayNames[today.getDay()] +
        ", " +
        monthNames[today.getMonth()] +
        " " +
        today.getDate()
      );
    },
  },
};
</script>
