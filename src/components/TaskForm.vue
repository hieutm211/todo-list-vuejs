<template>
    <div>
        <form class="task-form" @submit.prevent="handleSubmit">
            <input v-model="inputValue" placeholder="Enter a task...">
            <button>Add Task</button>
        </form>
        <div v-show="errorMessage" class="error-message">{{errorMessage}}</div>
    </div>
</template>

<script>
    export default {
        name: 'TaskForm',
        props: {
            getErrorMessage: {
                type: Function
            },
        },
        data() {
            return {
                inputValue: '',
                errorMessage: null
            }
        },
        methods: {
            handleSubmit() {
                this.errorMessage = this.getErrorMessage(this.inputValue);
                if (!this.errorMessage) {
                    this.$emit('add-task', this.inputValue);
                    this.inputValue = '';
                }
            }
        }
    }
</script>