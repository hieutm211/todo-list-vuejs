<template>
    <header>
        <div class="date-and-input">
            <div class="date">
                Friday, July 31
            </div>

            <div class="number-of-tasks">
                <span class="blue">
                    x Active Tasks
                </span>
            </div>

            <TaskForm/>
        </div>

        <nav>
            <button>Incomplete Tasks</button>
            <button>Completed Tasks</button>
        </nav>
    </header>
</template>

<script>
    import TaskForm from './TaskForm.vue';

    export default {
        name: 'Header',
        components: {
            TaskForm
        }
    }
</script>