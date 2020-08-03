<template>
  <header>
    <div class="date-and-input">
      <div class="date">
        Friday, July 31
      </div>

      <div class="number-of-tasks">
        <span class="blue"> {{ numberOfActiveTasks }} Active Tasks </span>
      </div>

      <TaskForm v-on="$listeners" :getErrorMessage="getErrorMessage" />
    </div>

    <nav>
      <button :class="getClassName(0)" @click="$emit('switch-list', 0)">
        Incomplete Tasks
      </button>
      <button :class="getClassName(1)" @click="$emit('switch-list', 1)">
        Completed Tasks
      </button>
    </nav>
  </header>
</template>

<script>
import TaskForm from './TaskForm.vue';

export default {
  name: 'Header',
  props: {
    numberOfActiveTasks: {
      type: Number,
    },
    currentList: {
      type: Number,
    },
    getErrorMessage: {
      type: Function,
    },
  },
  components: {
    TaskForm,
  },
  data() {
    return {};
  },
  methods: {
    getClassName(id) {
      if (this.currentList === id) {
        return 'active';
      }
      return null;
    },
  },
};
</script>
