<template>
    <div>
        <form class="task-form" @submit.prevent="">
            <input placeholder="Enter a task...">
            <button>Add Task</button>
        </form>
        <div class="error-message">Error message</div>
    </div>
</template>

<script>
    export default {
        name: 'TaskForm'
    }
</script>