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
            <button :class="getClassName(0)">Incomplete Tasks</button>
            <button :class="getClassName(1)">Completed Tasks</button>
        </nav>
    </header>
</template>

<script>
    import TaskForm from './TaskForm.vue';

    export default {
        name: 'Header',
        props: ['currentList'],
        components: {
            TaskForm
        },
        data() {
            return {
            }
        },
        methods: {
            getClassName(id) {
                if (this.currentList === id) {
                     return 'active';
                }
                return null;
            },
        },
        computed: {
        }
    }
</script>