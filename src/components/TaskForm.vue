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
        props: ['errorMessage'],
        data() {
            return {
                inputValue: '',
            }
        },
        methods: {
            handleSubmit() {
                this.$emit('check-error', this.inputValue);
                this.$nextTick(() => {
                    if (!this.errorMessage) {
                        this.$emit('add-task', this.inputValue);
                        this.inputValue = ''
                    }
                });
            }
        }
    }
</script>